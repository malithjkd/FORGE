# SOP-013: ML Model Development

> **Source:** Adapted from AI-001 (ML Model Development SOP)  
> **Scope:** All ML model development, experimentation, and deployment within FORGE projects  
> **Owner:** Technical Lead  
> **Standards Basis:** ISO/IEC/IEEE 12207:2017 (§6.4.5 Implementation, §6.4.7 Transition), FAIR4RS Principles

---

## 1. Purpose

This SOP defines how FORGE projects develop, evaluate, deploy, and maintain machine learning models. It establishes a repeatable process that enables research students to produce work that can be taken into production without losing reproducibility, quality, or IP clarity.

---

## 2. MLOps Philosophy

### 2.1 Three Pillars

**Reproducibility** — Any experiment run today must be exactly reproducible six months later by a different team member. Every experiment is logged: data version, code version, hyperparameters, random seeds, and results.

**Traceability** — Every model in production must be traceable back to the exact training data, training code, and experiment log that produced it.

**Automated quality gates** — No model reaches production through a manual process. There is a defined set of criteria (metrics, tests, review) that every model must pass.

### 2.2 Offline-First Architecture

All deployed models must be packaged as self-contained Docker images:
- All dependencies bundled — no `pip install` at runtime
- No dependency on external network connectivity
- Model updates deployed as new Docker images, not live swaps
- Inference server must start within 30 seconds

---

## 3. Tooling Stack

| Tool | Purpose | Why |
|------|---------|-----|
| **MLflow** | Experiment tracking, model registry | Self-hosted, no data leaves infrastructure |
| **DVC** | Data version control | Git-integrated, works with any storage backend |
| **FastAPI** | Model serving (inference API) | Python-native, automatic OpenAPI docs |
| **Docker** | Model packaging and deployment | Self-contained, reproducible images |
| **Prometheus + Grafana** | Production monitoring | Self-hosted, works offline |
| **pytest** | ML-specific testing | Consistent with rest of codebase |

---

## 4. Data Collection Protocol

Before collecting any data:

- [ ] Sensor specification document written and approved
- [ ] Data storage location set up on server (DVC backend)
- [ ] Data schema defined — column names, units, data types
- [ ] Machine identifier convention agreed
- [ ] At least 2 weeks of normal operation baseline data collected
- [ ] Data collection logged: who, which machine, which date, what activity

### Data Schema Template

```python
from dataclasses import dataclass
from datetime import datetime
from enum import Enum

class MachineState(Enum):
    OPERATING  = "operating"
    IDLE       = "idle"
    CALIBRATING = "calibrating"
    FAULT      = "fault"
    UNKNOWN    = "unknown"

@dataclass
class SensorReading:
    """One time-stamped reading from a single machine sensor."""
    machine_id:       str       # e.g. "MACHINE-001"
    sensor_id:        str       # e.g. "vib-spindle-x"
    timestamp:        datetime  # UTC always
    value:            float     # raw sensor value in SI units
    unit:             str       # e.g. "m/s2", "A", "degC"
    machine_state:    MachineState
    operator_id:      str
    collection_version: str
```

---

## 5. Data Pipeline

```
Raw sensor files (DVC-tracked)
        ↓
  data/raw/          (never modified after collection)
        ↓
  [preprocessing pipeline]
        ↓
  data/processed/    (cleaned, resampled, aligned)
        ↓
  [feature engineering pipeline]
        ↓
  data/features/     (feature matrix ready for training)
        ↓
  [train/val/test split]
        ↓
  data/splits/       (fixed splits, versioned)
```

Each step is a tested Python script in `src/data/`. DVC tracks every file at every stage.

### Data Versioning

```bash
# Adding a new dataset
dvc add data/processed/dataset_v1/
git add data/processed/dataset_v1.dvc
git commit -m "feat(data): add processed dataset v1"
dvc push
```

### Referencing in Experiments

```python
# At the top of every training script:
import subprocess
data_version = subprocess.check_output(
    ["git", "log", "--oneline", "-1", "data/processed/dataset_v1.dvc"]
).decode().strip()
mlflow.log_param("data_version", data_version)
```

---

## 6. Experimentation

### 6.1 Mandatory Experiment Logging

Every training run must log:

```python
with mlflow.start_run(run_name="experiment-name") as run:

    # Parameters (what went in)
    mlflow.log_params({
        "data_version":        data_version,
        "train_samples":       len(X_train),
        "val_samples":         len(X_val),
        "test_samples":        len(X_test),
        "model_type":          "LSTM",
        "learning_rate":       0.001,
        "random_seed":         42,
        "git_commit":          git_commit_hash,
    })

    # Metrics (what came out)
    mlflow.log_metrics({
        "val_f1":              f1_val,
        "val_recall":          recall_val,
        "val_precision":       precision_val,
        "test_f1":             f1_test,
        "inference_latency_ms": latency,
        "model_size_mb":       size,
    })

    # Artefacts
    mlflow.log_artifact("reports/experiment_notes.md")
    mlflow.log_artifact("reports/confusion_matrix.png")

    # Model
    mlflow.sklearn.log_model(model, "model",
        registered_model_name="fault-detector")
```

### 6.2 Experiment Notes Template

Every run must have an `experiment_notes.md`:

```markdown
# Experiment Notes
Run name:    [name]
Run ID:      [MLflow run ID]
Date:        [YYYY-MM-DD]
Author:      [name]

## What I Tried
[1–3 paragraphs]

## What I Found
[Key results with interpretation, not just numbers]

## Comparison with Previous Experiments
| Run | Model | Val F1 | Test AUC | Notes |
|-----|-------|--------|----------|-------|

## What I Would Try Next
[Concrete next experiments]

## Open Questions
[Things needing domain expert input]
```

### 6.3 Rules for Research Students

- **Notebooks** (`*.ipynb`) are for exploration only; never used in production
- **Random seeds** must be set at entry point of every script
- **Test set** used **once** — at the very end, after all tuning is complete
- **Class imbalance:** Do not use accuracy as primary metric; use F1, PR-AUC, or MCC

---

## 7. Evaluation Criteria

A model is a **candidate for production** when it meets:

| Criterion | Threshold |
|-----------|-----------|
| Test set F1 | ≥ 0.80 |
| Test set Recall | ≥ 0.85 |
| Test set Precision | ≥ 0.70 |
| Inference latency | ≤ 200 ms |
| Model file size | ≤ 500 MB |
| Reproducibility | 100% (same seed + data = identical output) |

### Reproducibility Check (Mandatory)

Before production approval, the Team Lead independently reproduces results:

```bash
git checkout <commit_hash>
dvc checkout
python src/train.py --config experiments/candidate_config.yaml
python src/evaluate.py --run-id <original> --run-id <reproduction>
```

---

## 8. Productionisation

### Research Code → Production Code

| Research Code | Production Code |
|--------------|----------------|
| Jupyter notebook or script | Importable Python module |
| No type hints | Full type hints |
| No docstrings | Google-style docstrings |
| Hardcoded paths | Config file or env variables |
| No error handling | Specific exception handling |
| No tests | Unit + shape + determinism + regression tests |
| Imports training code | Zero dependency on training code |
| `print()` | `logging` module |

### Production Module Structure

```
src/
├── inference/              ← Production (Developer owns)
│   ├── predictor.py
│   ├── feature_extractor.py
│   └── model_loader.py
├── api/                    ← FastAPI serving
│   ├── main.py
│   ├── routes/
│   └── schemas.py
├── data/                   ← Shared pipeline
│   ├── schema.py
│   └── preprocessor.py
└── training/               ← Research (Students own)
    ├── train.py
    ├── evaluate.py
    └── features.py
```

### Standard Predictor Interface

```python
@dataclass
class PredictionResult:
    machine_id:          str
    timestamp:           datetime
    fault_probability:   float
    fault_predicted:     bool
    confidence:          str
    model_version:       str
    inference_latency_ms: float

class FaultPredictor:
    def __init__(self, model_uri: str, threshold: float = 0.5):
        self._model = mlflow.pyfunc.load_model(model_uri)
        self._threshold = threshold

    def predict(self, sensor_data: np.ndarray, machine_id: str) -> PredictionResult:
        ...
```

---

## Cross-References

| Document | Relationship |
|----------|-------------|
| [SOP-010](./SOP-010-software-development.md) | General development workflow |
| [SOP-007](./SOP-007-FAIR-data-compliance.md) | FAIR data principles for datasets |
| [SOP-014](./SOP-014-coding-standards.md) | ML-specific coding standards |
| [10_data_governance.md](../00_system_design/10_data_governance.md) | Data classification and access control |

---

*Adapted for FORGE from industry MLOps practices. Review every 6 months or when ML tooling changes.*
