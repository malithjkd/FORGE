# SOP-014: Coding Standards

> **Source:** Adapted from TS-001 (Coding Standards)  
> **Scope:** All code in all FORGE project repositories, all languages  
> **Owner:** Team Lead  
> **Standards Basis:** ISO/IEC 25010:2023 (Maintainability), Clean Code (Robert C. Martin)

---

## 1. Purpose

This SOP is the team-wide coding standards reference. It consolidates language-specific standards and extends the code quality rules defined in SOP-010 and SOP-011.

---

## 2. General Principles (All Languages)

### 2.1 Readability Over Cleverness

```python
# Bad — clever but unreadable
result = [x for x in (y.strip() for y in f.readlines()) if x and not x.startswith('#')]

# Good — clear and maintainable
lines = f.readlines()
stripped_lines = [line.strip() for line in lines]
result = [line for line in stripped_lines if line and not line.startswith('#')]
```

### 2.2 Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Variables | `snake_case` (Python), `camelCase` (JS/TS, Dart, C#) | `sensor_reading` |
| Constants | `UPPER_SNAKE_CASE` | `MAX_SAFE_TEMP_C = 85.0` |
| Functions | `snake_case` (Python), `camelCase` (JS/TS) | `compute_error_map()` |
| Classes | `PascalCase` | `CalibrationGrid` |
| Files | `snake_case.py`, `kebab-case.ts`, `PascalCase.cs` | Per language |
| Booleans | Phrased as questions | `is_calibrated`, `has_data` |

### 2.3 Function Design

| Rule | Standard |
|------|----------|
| Max length | 50 lines (hard limit) |
| Max parameters | 4 (use config object for more) |
| Single responsibility | One function does one thing |
| Command-Query Separation | A function either does something OR returns something |

### 2.4 Error Handling

```python
# Bad
try:
    result = process(data)
except:
    print("Error")

# Good
try:
    result = process(data)
except FileNotFoundError as e:
    logger.error(
        "Sensor data file not found: %s. Expected at: %s.",
        e.filename, expected_path
    )
    raise
except ValueError as e:
    logger.error("Invalid data format for machine %s: %s", machine_id, e)
    raise
```

### 2.5 Comments

| Type | Rule |
|------|------|
| **Why comments** | Always explain *why*, never *what* |
| **Domain comments** | Explain physical/business constants |
| **TODO comments** | Must include GitHub Issue reference |
| **Commented-out code** | **Forbidden** — use Git history |
| **Docstrings** | Required on all public functions/classes |

### 2.6 File Organisation

| Rule | Standard |
|------|----------|
| Max file length | 500 lines |
| Import ordering | stdlib → third-party → local |
| One class per file | For non-trivial classes |
| No circular imports | Restructure if A↔B |

### 2.7 Forbidden Practices (PR Blockers)

- ❌ Hardcoded credentials, API keys, passwords, or secrets
- ❌ Commented-out code blocks
- ❌ `TODO` without a GitHub Issue reference
- ❌ `print()` / `console.log()` debugging in production
- ❌ Functions exceeding 50 lines
- ❌ Files exceeding 500 lines
- ❌ `any` type in TypeScript without justification
- ❌ Mutable default arguments in Python
- ❌ Bare `except:` clauses
- ❌ Hardcoded file paths to local machines

---

## 3. Python Standards

> Python is the primary language for AI/ML, data pipelines, and API development.

### 3.1 Tooling

| Tool | Purpose | Config |
|------|---------|--------|
| `black` | Formatter | Line length 88 |
| `ruff` | Linter | See `pyproject.toml` |
| `isort` | Import sorter | `profile = "black"` |
| `mypy` | Type checker | `--strict` for production |

### 3.2 Type Hints (Required)

```python
def compute_error_map(
    measurements: np.ndarray,
    reference: np.ndarray,
    resolution: float = 0.01,
) -> np.ndarray:
    """Compute a 2D error map from measurement and reference arrays."""
    ...
```

### 3.3 Docstrings (Google Style)

```python
def predict_failure(
    sensor_data: np.ndarray,
    machine_id: str,
    threshold: float = 0.5,
) -> PredictionResult:
    """Predict bearing failure probability from sensor readings.

    Args:
        sensor_data: Array of shape (n_samples, n_features).
        machine_id: Identifier for the machine.
        threshold: Probability threshold. Default 0.5.

    Returns:
        PredictionResult with fault probability and metadata.

    Raises:
        ValueError: If sensor_data shape is unexpected.
    """
```

### 3.4 Python-Specific Rules

| Rule | Standard |
|------|----------|
| String formatting | f-strings only |
| File handling | Context managers (`with`) |
| File paths | `pathlib.Path` |
| Exceptions | Specific types only |
| Mutable defaults | `def fn(items=None):` pattern |
| Data containers | `@dataclass` for data classes |
| Enums | `enum.Enum` for fixed sets |
| Logging | `logging` module, not `print()` |

---

## 4. C++ Standards

> C++ is used for machine control and vision system code. Safety is paramount.

### 4.1 Safety-Critical Rules (Mandatory)

| Rule | Standard | Rationale |
|------|----------|-----------|
| No raw pointers | `std::unique_ptr` / `std::shared_ptr` | Prevent memory leaks |
| RAII everywhere | Acquire in constructor, release in destructor | Prevent resource leaks |
| Bounds checking | Check indices before array access | Prevent undefined behaviour |
| `const` correctness | Mark immutable values as `const` | Prevent accidental mutation |
| Thread safety | `std::mutex` or `std::atomic` for shared state | Prevent race conditions |
| Motion safety | Check machine state before every command | Prevent physical damage |

### 4.2 Physical Constants

All physical constants must be named, documented with source, and in a constants file:

```cpp
namespace project::constants {
// Maximum safe operating temperature for spindle motor
// Source: Machine Service Manual, Section 4.2.1
constexpr double MAX_SAFE_SPINDLE_TEMP_C = 85.0;
}
```

---

## 5. TypeScript / JavaScript Standards

> TypeScript is required for all new web code.

| Rule | Standard |
|------|----------|
| No `any` | Forbidden without justification |
| Strict mode | `"strict": true` in `tsconfig.json` |
| Null checks | Use `?.` and `??` |
| Components | Function components + hooks only |

---

## 6. AI/ML Code Standards

### 6.1 Reproducibility

| Rule | Standard |
|------|----------|
| Random seeds | Set at entry point |
| Data versioning | DVC for all datasets |
| Code versioning | Git commit hash in MLflow |
| Environment | Pinned dependency versions |

### 6.2 Data Leakage Prevention

```python
# BAD — leaks test data into preprocessing
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)  # fits on ALL data
X_train, X_test = train_test_split(X_scaled, y)

# GOOD — no leakage
X_train, X_test = train_test_split(X, y)
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)  # fit on train ONLY
X_test = scaler.transform(X_test)        # transform with train params
```

### 6.3 Separation of Concerns

```
src/
├── training/      ← Training code (students own)
├── inference/     ← Inference code (developer owns) — NO imports from training/
└── data/          ← Shared data pipeline
```

**Rule:** Inference module must work with **zero dependency** on training module.

---

## 7. Secrets Management

**Secrets must never enter the repository.**

| Method | When |
|--------|------|
| Environment variables | Local development (`.env` in `.gitignore`) |
| GitHub Secrets | CI/CD pipelines |
| Secrets manager | Production |

If a secret is accidentally committed: treat as compromised immediately, rotate, and notify leads.

---

## Cross-References

| Document | Relationship |
|----------|-------------|
| [SOP-010](./SOP-010-software-development.md) | Development workflow |
| [SOP-011](./SOP-011-code-review.md) | Review checklists referencing these standards |
| [SOP-013](./SOP-013-ml-model-development.md) | ML-specific lifecycle |
| [11_software_engineering_standards.md](../00_system_design/11_software_engineering_standards.md) | ISO 25010 quality model |

---

*Adapted for FORGE from industry coding standards. Review every 6 months.*
