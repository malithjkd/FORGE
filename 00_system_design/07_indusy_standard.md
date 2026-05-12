# R&D Project Management Reference Guide
## High-Precision Gantry System Predictive Maintenance — Master's Project

> **Status:** Living Document — v1.0 (Draft for Team Review)
> **Last Updated:** 2025-05-11
> **Maintainers:** Research Team + Industry Partner
> **Licence:** Internal use — not for public distribution until IP clearance

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [International Standards & Frameworks](#2-international-standards--frameworks)
   - 2.1 [Project Management Standards](#21-project-management-standards)
   - 2.2 [Research & Documentation Standards](#22-research--documentation-standards)
   - 2.3 [Predictive Maintenance Domain Standards](#23-predictive-maintenance-domain-standards)
   - 2.4 [Software Engineering Standards](#24-software-engineering-standards)
3. [Research Lifecycle — All 10 Phases](#3-research-lifecycle--all-10-phases)
4. [Software Tools — Complete Reference](#4-software-tools--complete-reference)
   - 4.1 [Project Management & Task Tracking](#41-project-management--task-tracking)
   - 4.2 [Electronic Lab Notebook (ELN)](#42-electronic-lab-notebook-eln)
   - 4.3 [Literature Management](#43-literature-management)
   - 4.4 [Code Version Control](#44-code-version-control)
   - 4.5 [Data Version Control](#45-data-version-control)
   - 4.6 [Experiment Tracking](#46-experiment-tracking)
   - 4.7 [Documentation & Wiki](#47-documentation--wiki)
   - 4.8 [Signal Analysis & Computing](#48-signal-analysis--computing)
5. [Recommended Integrated Stack](#5-recommended-integrated-stack)
6. [Signal Data Management](#6-signal-data-management)
   - 6.1 [Data Architecture & Lineage](#61-data-architecture--lineage)
   - 6.2 [File Formats](#62-file-formats)
   - 6.3 [HDF5 Structure for Gantry PdM](#63-hdf5-structure-for-gantry-pdm)
   - 6.4 [Folder Structure](#64-folder-structure)
   - 6.5 [File Naming Convention](#65-file-naming-convention)
   - 6.6 [Metadata Schema (FAIR-compliant)](#66-metadata-schema-fair-compliant)
7. [Compliance Checklist](#7-compliance-checklist)
8. [Team Roles & Responsibilities](#8-team-roles--responsibilities)
9. [Open Questions & Items to Refine](#9-open-questions--items-to-refine)
10. [References & Further Reading](#10-references--further-reading)

---

## 1. Project Overview

### Research Topic

**Predictive Maintenance (PdM) of a High-Precision Gantry System using Motion Control and External Signals to Identify Aging, Wear, and Tear**

This project investigates condition monitoring of an electromechanical gantry system by fusing:
- **Motion control signals** — position (encoder), velocity, motor current, torque commands
- **External sensor signals** — vibration (accelerometer), temperature, acoustic emission

The goal is to develop signal-processing and machine-learning pipelines that detect and classify degradation states before failure occurs, enabling predictive (rather than reactive or scheduled) maintenance.

### Project Type

| Parameter | Value |
|---|---|
| Degree Level | Master's (Research) |
| Collaboration | University + Industry Partner |
| Team Size | 2–5 people |
| Duration | ~18–24 months (adjust as needed) |
| Domain | Engineering — Electromechanical Systems |
| Methodology | Hybrid Agile + Stage-Gate |

### Key Research Questions *(to be refined)*

> **Note for team:** Define these before any experiments begin. Pre-register on OSF for IP protection.

- [ ] RQ1: Which signal features (time-domain, frequency-domain, time-frequency) most reliably discriminate between wear states in a high-precision gantry?
- [ ] RQ2: At what wear level do signal signatures become statistically distinguishable from a healthy baseline?
- [ ] RQ3: Which supervised/unsupervised ML model architecture achieves the best generalisation across different operating conditions?
- [ ] RQ4: What is the minimum sensor set required for effective PdM in this system?

---

## 2. International Standards & Frameworks

### 2.1 Project Management Standards

#### PMI PMBOK® Guide — 7th Edition (2021)
**Scope:** Global gold standard for project management  
**Key elements:** 12 performance principles covering stewardship, team, stakeholders, value, systems thinking, leadership, tailoring, quality, complexity, risk, adaptability, and change. Supports both predictive (Waterfall) and Agile approaches.  
**Relevance:** The framework to cite when justifying your PM methodology to supervisors and industry partners. PMP certification is the most globally recognised PM credential.

#### PRINCE2® 7th Edition (2023)
**Scope:** Process-driven PM framework, popular in UK, Europe, and Asia-Pacific  
**Key elements:** 7 Principles, 7 Themes, 7 Processes. Structured around stage gates (Decision Points), business justification, and defined product delivery.  
**Relevance:** If your industry partner operates in UK/Europe, they likely use PRINCE2. Aligning milestone gates to PRINCE2 stages will resonate with their internal governance.

#### ISO 21500:2021 — Project Management Guidance
**Scope:** International Standard (neutral, non-commercial)  
**Key elements:** Project management concepts and processes aligned with PMBOK. Used when a neutral standard reference is needed for academic publications or cross-border collaborations.  
**Relevance:** Cite in your thesis Methods section when describing your project management approach.

#### PM.UIC Framework (Fernandes et al., 2019–2022)
**Scope:** Peer-reviewed framework specifically for **University–Industry Collaboration (UIC)** R&D  
**Key elements:** Lifecycle PM practices (initiation → planning → execution → monitoring → closure) plus transversal governance practices (risk, communication, stakeholder, knowledge management). Validated in the Bosch–University of Minho collaboration (60M€ investment, 2013–2024).  
**Relevance:** **Most directly applicable framework to your project.** Cite: Fernandes, G. et al. (2022). *Project management practices in major university-industry R&D collaboration programs.* PMC.

#### Agile / Scrum
**Scope:** Iterative, sprint-based development — now part of PMBOK 7 and widely adopted in R&D  
**Key elements:** 2-week sprints, sprint planning, daily standups, sprint review, retrospective. Backlog = ordered list of research tasks.  
**Relevance:** Use Scrum for the day-to-day research execution. Each sprint = one experiment cycle, one analysis step, or one documentation milestone.

#### Recommended Hybrid Approach

```
STAGE GATE 0      STAGE GATE 1        STAGE GATE 2         STAGE GATE 3
   |                    |                   |                    |
[Setup]---[Sprint 1-3]--[Design]--[Sprint 4-8]--[Validate]--[Sprint 9-12]--[Report]
Literature,           Experimental        Data analysis,       Thesis,
planning              design, testing     findings             publication
```

**Stage Gates** = formal milestones reviewed by both university supervisor and industry partner.  
**Sprints** = 2-week iterative cycles of research work between gates.

---

### 2.2 Research & Documentation Standards

#### FAIR Data Principles
**Authority:** Wilkinson et al. (2016), *Nature Scientific Data*. Adopted by EU Horizon, NIH, UKRI, and most major journals.  
**Mandatory for publication** in IEEE Transactions, Elsevier, and Springer journals.

| Principle | Meaning | How to implement |
|---|---|---|
| **F — Findable** | Data has unique persistent identifier, rich metadata, indexed in searchable resource | Publish dataset on Zenodo → get DOI → add to OSF project page |
| **A — Accessible** | Data retrievable by identifier via open standard protocol | Zenodo/figshare public access OR controlled access with documented conditions |
| **I — Interoperable** | Uses standard formats, vocabularies, ontologies | HDF5 for signals, CSV/Parquet for features, Dublin Core metadata schema |
| **R — Reusable** | Clear usage license, detailed provenance, community standards | CC-BY-4.0 license, README with context, link code version to data version |

#### ISO 9001:2015 — Quality Management Systems
**Relevance:** Your industry partner almost certainly operates under ISO 9001. Structuring your research documentation to include: document control (version numbers), review and approval records, and non-conformance logging will align with their quality culture and strengthen the collaboration.

#### Open Science Framework (OSF) Pre-registration
**Why it matters:** Pre-registering your research questions, hypotheses, and methodology *before* running experiments creates a timestamped public record. This:
1. Protects your intellectual property (proves conception date)
2. Prevents accusation of HARKing (Hypothesising After Results are Known)
3. Is increasingly required or encouraged by journals

**Action:** Create a private OSF project, draft your pre-registration, and register it before the first data collection session.

---

### 2.3 Predictive Maintenance Domain Standards

> **These are the standards you MUST cite in your thesis literature review and Methods section.**

| Standard | Full Title | Key Relevance to Your Project |
|---|---|---|
| **ISO 13374-1:2003** | Condition monitoring and diagnostics of machines — Data processing, communication and presentation — Part 1: General guidelines | Governs how condition monitoring data is processed and structured. Directly applicable to your signal acquisition and processing pipeline. |
| **ISO 13374-2:2007** | Condition monitoring — Part 2: Data processing | Defines processing layers: Data Acquisition → Data Manipulation → State Detection → Health Assessment → Prognostics Assessment → Advisory Generation |
| **ISO 17359:2018** | Condition monitoring and diagnostics of machines — General guidelines | Guides selection of monitoring parameters, measurement types, and monitoring intervals. Use when justifying your choice of signals (vibration, current, encoder). |
| **ISO 13379-1:2012** | Condition monitoring — Data interpretation and diagnostics techniques — Part 1: General guidelines | Frameworks for interpreting signal features to identify fault modes. Informs your feature engineering and classification methodology. |
| **ISO 10816-1 / ISO 20816** | Mechanical vibration — Evaluation of machine vibration | Vibration threshold standards. Use to contextualise your vibration signal levels against established severity criteria. |
| **IEEE PdM White Paper 2024** | Predictive Maintenance in the Context of Functional Safety | Latest IEEE guidance on PdM methodology. Documents current gaps in standards and best practices for PdM in safety-critical systems. Cite for contemporary standards context. |
| **ISO 55000:2014** | Asset management — Overview, principles and terminology | Frames PdM within the broader asset management lifecycle. Useful when contextualising the industry benefit of your research. |
| **IEC 61800-series** | Adjustable speed electrical power drive systems | Standards for the motion control drive system in your gantry. Relevant to signal characterisation and documentation of your hardware. |

#### ISO 13374 Data Processing Chain (your pipeline maps to this)

```
Layer 1: Data Acquisition         → Raw HDF5 files (position, velocity, current, vibration)
Layer 2: Data Manipulation        → Preprocessing: resampling, filtering, segmentation
Layer 3: State Detection          → Feature extraction: FFT, RMS, kurtosis, wavelet coefficients
Layer 4: Health Assessment        → Classification: wear level 0–5
Layer 5: Prognostics Assessment   → Remaining Useful Life (RUL) estimation
Layer 6: Advisory Generation      → Maintenance recommendations
```

---

### 2.4 Software Engineering Standards

| Standard | Relevance |
|---|---|
| **ISO/IEC/IEEE 29148:2018** — Requirements Engineering | Documents your system requirements: what signals are acquired, at what rate, with what accuracy. Write a brief SRS (Software Requirements Specification) for your DAQ and analysis pipeline. |
| **ISO/IEC/IEEE 12207:2017** — Software Lifecycle Processes | Governs development of your signal processing and ML code: planning, requirements, design, implementation, verification, maintenance. |
| **IEEE 1012** — Software Verification & Validation | Relevant for validating your feature extraction functions and ML model — defines V&V levels and activities. |
| **ISO/IEC/IEEE 24748** — Lifecycle Management | Broader systems engineering lifecycle context for your electromechanical + software system. |

---

## 3. Research Lifecycle — All 10 Phases

> **How to use this section:** Each phase has a description, key outputs, recommended tools, and action items. Work through each phase sequentially, but expect iteration — particularly between Phases 4–8.

---

### Phase 1 — Literature Study

**Objective:** Build a comprehensive, systematic understanding of the state of the art in gantry PdM, condition monitoring of electromechanical systems, and relevant ML methods.

**Key Outputs:**
- Annotated bibliography (Zotero library)
- Literature Review Matrix (Notion database)
- Literature Review chapter draft (Overleaf)
- Gap analysis: what is missing in current research that your project addresses

**Recommended Tools:**
- **Zotero** — primary reference manager. Use browser plugin for 1-click import from IEEE Xplore, Scopus, Google Scholar. Create a shared group library for the team.
- **Notion** — build a Literature Review Matrix table with columns: `Author`, `Year`, `Topic`, `Dataset used`, `Method`, `Key finding`, `Limitation/Gap`, `Relevance to our project`
- **Connected Papers** (connectedpapers.com) — visual citation graph to find related papers you might otherwise miss
- **JabRef** — if you prefer BibTeX-native management for Overleaf

**Key Databases to Search:**
- IEEE Xplore — primary source for PdM, signal processing, motion control
- Scopus / Web of Science — broader engineering literature
- Google Scholar — preprints and conference papers
- ScienceDirect (Elsevier) — Mechanical Systems and Signal Processing journal

**Search Terms to Use:**
```
"gantry system" + "predictive maintenance"
"electromechanical" + "condition monitoring" + "wear"
"motion control signals" + "fault detection"
"motor current signature analysis" + "wear"
"vibration analysis" + "bearing degradation"
"remaining useful life" + "linear axis"
"digital twin" + "gantry" + "maintenance"
```

**Action Items:**
- [ ] Set up Zotero group library with team members
- [ ] Build Literature Review Matrix template in Notion
- [ ] Complete systematic search across all databases (document search strings and result counts)
- [ ] Read and annotate minimum 30 key papers before Phase 2
- [ ] Produce one-page Gap Analysis document

---

### Phase 2 — Idea Development & Hypothesis Formation

**Objective:** Define precise research questions, hypotheses, experimental approach, and document them before any experiments begin.

**Key Outputs:**
- Research Questions document (OSF pre-registration)
- Conceptual framework diagram (draw.io)
- Feasibility assessment
- Industry partner briefing document

**Recommended Tools:**
- **OSF (Open Science Framework)** — pre-register research questions and methodology. Creates timestamped IP record.
- **eLabFTW** — begin ELN entries for all ideas and decisions. Timestamped and tamper-evident.
- **Notion/Confluence** — build the project wiki: background, hypotheses, experimental design rationale, stakeholder meeting notes.
- **Miro** — digital whiteboard for brainstorming sessions (especially useful for distributed teams)
- **draw.io** — system architecture diagram showing the gantry → sensors → DAQ → processing pipeline

> ⚠️ **IP Protection Rule:** Every new idea must be recorded in the ELN with a timestamp **before** it is discussed with the industry partner. The ELN entry is your legal record of conception date.

**Action Items:**
- [ ] Create OSF project (private) and complete pre-registration draft
- [ ] Set up eLabFTW instance (self-hosted or request from university IT)
- [ ] Document final research questions — agree with supervisor and industry partner
- [ ] Produce system overview diagram of the gantry + instrumentation
- [ ] Draft feasibility assessment: can we achieve the required wear states within project timeline?

---

### Phase 3 — Project Planning & Task Management

**Objective:** Create a full project plan with WBS (Work Breakdown Structure), milestones, deliverables, responsibilities, timeline, and risk register.

**Key Outputs:**
- Work Breakdown Structure
- Milestone schedule (aligned with Stage Gates)
- Risk Register
- Data Management Plan (DMP)
- Communication Plan (with industry partner)

**Recommended Tools:**
- **GitHub Projects** — primary task tracker. Create issues for each task, milestones for stage gates, use Kanban board for sprint management. Free with GitHub account.
- **Notion** — project wiki + meeting notes + decision log. Create a Timeline/Gantt view for milestone overview.
- **DMP Online** (dmponline.dcc.ac.uk) — write the formal Data Management Plan (often required by universities and funders)
- **Jira** (free ≤10 users) — if your industry partner prefers this. Pairs with Confluence for documentation.

**Sprint Structure (recommended):**

| Sprint Type | Duration | Content |
|---|---|---|
| Research Sprint | 2 weeks | Literature, analysis, writing |
| Experiment Sprint | 2 weeks | Test preparation + data collection |
| Analysis Sprint | 2 weeks | Data processing + feature engineering |
| Review Sprint | 1 week | Documentation + supervisor/industry meeting |

**Milestone Template:**

| Milestone | Description | Deliverable | Review By |
|---|---|---|---|
| M1 — Project Initiation | Setup complete, DMP approved | DMP + GitHub repo | Supervisor |
| M2 — Literature Review | Systematic review complete | Literature chapter draft | Supervisor + Industry |
| M3 — Experimental Design | Test protocols finalised | Test Plan document | Supervisor + Industry |
| M4 — Data Collection Complete | All wear-state datasets collected | Dataset v1.0 on DVC | Supervisor |
| M5 — Analysis Complete | Models trained and evaluated | Results notebook + report | Supervisor + Industry |
| M6 — Thesis Submission | Full thesis submitted | Thesis PDF | University |
| M7 — Publication | Paper submitted | Manuscript | Supervisor + Industry |

**Action Items:**
- [ ] Create GitHub repository (private) — add all team members
- [ ] Set up GitHub Projects board with all phases as milestones
- [ ] Write Data Management Plan — get supervisor approval
- [ ] Create Risk Register (minimum 10 risks with likelihood × impact scores)
- [ ] Schedule recurring meetings: weekly (internal team) + monthly (industry partner)

---

### Phase 4 — Experimental Design & Test Preparation

**Objective:** Design the full test matrix, document apparatus setup, configure DAQ systems, and write formal test protocols — before touching the equipment.

**Key Outputs:**
- Test Protocol document (version-controlled in Overleaf/Confluence)
- Sensor placement drawing (draw.io)
- DAQ configuration record (ELN)
- Safety assessment
- Calibration records for all sensors

**Recommended Tools:**
- **eLabFTW / OSF ELN** — document sensor placements, gantry configuration, sampling rates, DAQ settings, test matrix. Each setup decision becomes a timestamped ELN entry.
- **draw.io** — sensor placement schematics, signal flow diagrams, wiring diagrams. Export as SVG/PNG for reports.
- **MATLAB / Simulink** — system modelling and simulation before physical tests. Version `.m` and `.slx` files with Git.
- **Overleaf (LaTeX)** — write the formal Test Protocol using IEEE or university template.

**Test Matrix Design:**

Consider documenting your test matrix as a structured table:

| Run ID | Date | Gantry ID | Wear Level | Speed (mm/s) | Load (N) | Duration (s) | Operator | Notes |
|---|---|---|---|---|---|---|---|---|
| T001 | 2025-06-01 | G01 | W0 (new) | 100 | 0 | 120 | Name | Baseline |
| T002 | 2025-06-01 | G01 | W0 | 200 | 0 | 120 | Name | Speed sweep |
| ... | | | | | | | | |

**Signal Acquisition Checklist:**
- [ ] Sampling rate determined and documented (consider Nyquist — at least 2× highest frequency of interest)
- [ ] Anti-aliasing filter cutoff documented
- [ ] Sensor calibration certificates obtained and filed
- [ ] Synchronisation method for all channels documented (hardware trigger preferred)
- [ ] Baseline (healthy system) dataset collected and labelled first

---

### Phase 5 — Data Collection & Real-Time Logging

**Objective:** Execute the test plan, collect signal data under controlled conditions, and log all conditions and anomalies in the ELN in real time.

**Key Outputs:**
- Raw dataset (HDF5 files, DVC-tracked, immutable after collection)
- ELN entry for every collection session
- Anomaly log (unexpected events, equipment issues, deviations from protocol)

**Recommended Tools:**
- **HDF5 (.h5)** — primary data format. Hierarchical, compressed, supports embedded metadata. Use `h5py` (Python) or MATLAB HDF5 API.
- **Python NI-DAQmx** or **LabVIEW** — if using National Instruments hardware
- **eLabFTW** — ELN entry per session: date, operator, gantry state, any anomalies, equipment checklist
- **DVC** — immediately after collection, `dvc add data/raw/` + `dvc push` to remote storage

**Critical Rule:** Raw data files are **never modified** after collection. All processing creates new files in `data/processed/`. This is enforced by DVC tracking of the `data/raw/` directory.

**Pre-collection ELN Template:**
```
Date: YYYY-MM-DD
Operator: [name]
Gantry ID: G01
Wear Level: W[n]
Expected wear description: [e.g., "Linear guide, 500km cumulative travel"]
Equipment checklist: [sensors calibrated / connections checked / DAQ settings verified]
Test protocol version: v1.2
Deviations from protocol: [none / describe]
Post-collection notes: [anomalies, observations, next steps]
```

---

### Phase 6 — Code & Data Version Control

**Objective:** Maintain full, reproducible lineage between every result and the exact code version + dataset version that produced it.

**Key Outputs:**
- Git commit history for all code
- DVC commit history for all datasets and models
- Tagged releases for milestone versions

**Architecture:**

```
Git repository (GitHub)
├── Tracks: all .py, .ipynb, .yaml, .md, .tex files
├── Tracks: DVC metafiles (.dvc pointer files)
└── NOT: actual data files (handled by DVC)

DVC remote (Google Drive / S3)
├── Tracks: data/raw/ (HDF5 signal files)
├── Tracks: data/processed/ (cleaned data)
├── Tracks: data/features/ (extracted features)
└── Tracks: models/ (trained model files)
```

**Git Branching Strategy:**

```
main          ← stable, supervisor-reviewed, tagged at milestones
  └── develop ← active development, merged to main at sprint end
        ├── feature/signal-preprocessing
        ├── feature/fft-feature-extraction
        ├── experiment/wear-classifier-svm
        └── experiment/wear-classifier-cnn
```

**Key Commands:**
```bash
# Start new experiment
git checkout -b experiment/your-experiment-name

# After data collection — version the data
dvc add data/raw/20250601_G01_W3_SpeedSweep_R01.h5
git add data/raw/20250601_G01_W3_SpeedSweep_R01.h5.dvc .gitignore
git commit -m "data: add W3 speed sweep run 01"
dvc push

# Reproduce any past experiment
git checkout <commit-hash>
dvc checkout
dvc repro   # re-runs full pipeline from that point

# Tag a milestone
git tag -a v1.0-data-collection-complete -m "All wear states collected"
git push origin --tags
```

**Reproducibility Rule:** Before reporting any result, verify: `git checkout <tag> && dvc checkout && dvc repro` produces the same numbers.

---

### Phase 7 — Data Storage, Organisation & Backup

**Objective:** Ensure data is safely backed up, well-organised, and accessible to all team members throughout the project.

**3-2-1 Backup Rule:**
- **3** copies of all data
- **2** different storage media/services
- **1** offsite (cloud) backup

| Copy | Location | Who manages |
|---|---|---|
| Primary | DVC remote (Google Drive / S3) | Team (auto-push via DVC) |
| Secondary | University HPC / NAS | University IT |
| Offsite archive | Zenodo (for published datasets) | Principal researcher |

**Action Items:**
- [ ] University HPC/NAS storage allocated — confirm quota
- [ ] DVC remote configured and tested by all team members
- [ ] Backup verification scheduled (monthly: confirm all DVC remotes are current)

---

### Phase 8 — Data Analysis & Experiment Tracking

**Objective:** Extract meaningful signal features, train and evaluate predictive models, and track every experiment run so results are reproducible and comparable.

**Key Outputs:**
- Feature engineering pipeline (Python + DVC)
- Trained and evaluated ML models
- MLflow experiment dashboard
- Analysis notebooks (Jupyter, version-controlled)

**Recommended Python Stack:**

| Library | Purpose |
|---|---|
| `h5py` | Read/write HDF5 signal files |
| `numpy`, `pandas` | Numerical computing and tabular data |
| `scipy.signal` | Filtering, FFT, spectral analysis |
| `tsfresh` | Automated time-series feature extraction (hundreds of features automatically) |
| `librosa` | Audio/vibration spectral features (MFCC, spectral centroid, etc.) |
| `scikit-learn` | Classical ML: SVM, Random Forest, kNN, evaluation metrics |
| `PyTorch` / `TensorFlow` | Deep learning models (CNN-1D, LSTM, Transformer for time-series) |
| `matplotlib`, `seaborn`, `plotly` | Visualisation |
| `mlflow` | Experiment tracking |
| `dvc` | Pipeline and data versioning |

**DVC Pipeline Definition (`dvc.yaml`):**

```yaml
stages:
  preprocess:
    cmd: python src/preprocess.py
    deps:
      - src/preprocess.py
      - data/raw/
    outs:
      - data/processed/

  extract_features:
    cmd: python src/features.py
    deps:
      - src/features.py
      - data/processed/
    outs:
      - data/features/

  train:
    cmd: python src/train.py
    deps:
      - src/train.py
      - data/features/
      - params.yaml
    outs:
      - models/
    metrics:
      - reports/metrics.json

  evaluate:
    cmd: python src/evaluate.py
    deps:
      - src/evaluate.py
      - models/
      - data/features/
    outs:
      - reports/figures/
```

Run the full pipeline with: `dvc repro`
Compare experiments: `dvc exp show` or `dvc plots show`

**MLflow Experiment Tracking:**
```python
import mlflow

with mlflow.start_run(run_name="SVM_wear_classifier_v3"):
    mlflow.log_param("kernel", "rbf")
    mlflow.log_param("C", 1.0)
    mlflow.log_param("features", "fft_rms_kurtosis")
    mlflow.log_param("data_version", "v1.2")
    mlflow.log_param("git_commit", "abc1234")

    # ... train model ...

    mlflow.log_metric("accuracy", 0.934)
    mlflow.log_metric("f1_macro", 0.921)
    mlflow.sklearn.log_model(model, "model")
```

**Notebook Organisation:**

| Notebook | Purpose |
|---|---|
| `01_data_exploration.ipynb` | Initial signal visualisation and statistics |
| `02_preprocessing.ipynb` | Filtering, resampling, segmentation development |
| `03_feature_engineering.ipynb` | Feature extraction development and selection |
| `04_baseline_models.ipynb` | Simple classifiers (Logistic Regression, kNN) |
| `05_advanced_models.ipynb` | SVM, Random Forest, neural networks |
| `06_results_summary.ipynb` | Final results, figures for report/paper |

---

### Phase 9 — Findings Documentation & Internal Reporting

**Objective:** Communicate progress and findings clearly to supervisors and industry partners. Document intermediate results before memories fade.

**Key Outputs:**
- Monthly progress reports (PDF from Overleaf or Notion → PDF)
- Industry partner milestone briefing
- Internal wiki updates (Notion/Confluence)
- Sprint retrospective notes

**Recommended Tools:**
- **Notion/Confluence** — team wiki for living documentation. Industry partner can be given view/comment access.
- **Overleaf** — formal reports using university or IEEE template. Collaborative with supervisor.
- **Jupyter Book** — convert analysis notebooks into a professional, web-browsable report. Good for showing computational results.

**Report Template Structure:**
```
1. Executive Summary (1 page — for industry partner)
2. Progress Against Plan
3. Technical Results (this sprint/period)
4. Data Collected
5. Issues & Risks
6. Next Steps
7. Appendices (detailed data, code snippets)
```

---

### Phase 10 — Thesis Writing & Publication

**Objective:** Produce the final thesis, submit a conference or journal paper, and publish data and code openly (subject to IP clearance).

**Key Outputs:**
- Full thesis manuscript
- Journal paper (IEEE Transactions target — see below)
- Published dataset on Zenodo (with DOI)
- Published code on GitHub with Zenodo DOI
- Zenodo/ORCID linked to published outputs

**Recommended Tools:**
- **Overleaf (LaTeX)** — free collaborative LaTeX editor. University thesis template and IEEE template both available. Git-sync enables backup and versioning.
- **Zotero + BetterBibTeX** — auto-export `.bib` file from Zotero library. Seamless Overleaf integration for citations.
- **Zenodo** — publish dataset and code before or at paper submission. Cite the DOI in the paper.
- **ORCID** (orcid.org) — register a researcher ID. Required by most journals. Links all publications, datasets, and affiliations.

**Target Journals and Conferences:**

| Venue | Type | Scope | Impact Factor |
|---|---|---|---|
| IEEE Trans. on Industrial Electronics | Journal | PdM, motion control, sensors | ~7.5 |
| IEEE Trans. on Industrial Informatics | Journal | Industrial AI, data-driven maintenance | ~11.7 |
| Mechanical Systems & Signal Processing | Journal | Vibration, condition monitoring | ~8.4 |
| Reliability Engineering & System Safety | Journal | System reliability, maintenance | ~9.4 |
| PHM Society Annual Conference | Conference | Prognostics and health management | — |
| IEEE IECON | Conference | Industrial electronics and control | — |

**Pre-Publication IP Checklist:**
- [ ] Industry partner has reviewed all materials to be made public
- [ ] Any proprietary test parameters/equipment details anonymised or approved for disclosure
- [ ] Joint authorship and acknowledgement agreed
- [ ] Open-access funding confirmed (check university OA agreement)

---

## 4. Software Tools — Complete Reference

### 4.1 Project Management & Task Tracking

| Tool | Type | Best For | Free Tier | Recommend |
|---|---|---|---|---|
| **GitHub Projects** | Cloud | Code-linked Kanban, milestones, roadmap. Native integration with issues/PRs. | Free (academic Pro) | ⭐ Primary |
| **Notion** | Cloud | All-in-one: tasks + docs + wiki + database + timeline. Very flexible. | Free (generous) | ⭐ Primary |
| **Jira** | Cloud | Industry standard, sprints, advanced reporting, roadmaps | Free ≤10 users | Optional |
| **Linear** | Cloud | Fast, clean issue tracking, Git integration, keyboard-first | Free ≤250 issues | Optional |
| **Trello** | Cloud | Simple Kanban, low learning curve | Free (limited) | Fallback |
| **Microsoft Project** | Desktop | Formal Gantt, resource management | Paid (Office 365) | No |

### 4.2 Electronic Lab Notebook (ELN)

| Tool | Type | Best For | Free Tier | Recommend |
|---|---|---|---|---|
| **OSF** | Cloud | Full research lifecycle management, pre-registration, FAIR compliance, public-facing project page | Free (unlimited) | ⭐ Primary |
| **eLabFTW** | Self-hosted | Timestamped, tamper-evident ELN. IP protection. Legally defensible record. Open source. | Free (self-host) | ⭐ Primary |
| **Jupyter Notebooks** | Local/Cloud | Computational experiment records: code + results + narrative in one document | Free (open source) | ⭐ Essential |
| **SciNote** | Cloud | ELN + project structure + templates | Free basic tier | Optional |
| **LabArchives** | Cloud | Cloud ELN, FDA 21 CFR Part 11 compliant, NIH-trusted | Paid (uni may license) | If required |

### 4.3 Literature Management

| Tool | Type | Best For | Free Tier | Recommend |
|---|---|---|---|---|
| **Zotero** | Desktop + Cloud | Browser plugin import, group libraries, Overleaf integration, open source | Free (open source) | ⭐ Primary |
| **Mendeley** | Desktop + Cloud | PDF annotation, Elsevier journal integration | Free (2GB) | Optional |
| **JabRef** | Desktop | BibTeX-native, perfect for LaTeX/Overleaf workflows | Free (open source) | Optional |
| **Connected Papers** | Web | Visual citation graph for discovering related literature | Free (5 papers/month) | Supplementary |

### 4.4 Code Version Control

| Tool | Type | Best For | Free Tier | Recommend |
|---|---|---|---|---|
| **Git** | Local | All source code, analysis scripts, config, notebooks | Free (open source) | ⭐ Essential |
| **GitHub** | Cloud | Hosting, collaboration, GitHub Projects, Actions CI/CD, Codespaces | Free (academic Pro) | ⭐ Primary |
| **GitLab** | Self-hosted | On-premise option for sensitive IP — full CI/CD built in | Free (self-host) | Alternative |
| **Bitbucket** | Cloud | Atlassian ecosystem (if using Jira + Confluence) | Free ≤5 users | Alternative |

### 4.5 Data Version Control

| Tool | Type | Best For | Free Tier | Recommend |
|---|---|---|---|---|
| **DVC** | Local + remote | Large dataset versioning alongside Git. Full pipeline DAG. ML experiment tracking. | Free (open source) | ⭐ Primary |
| **Git LFS** | Cloud | Simpler large file versioning, built into GitHub/GitLab | Free (1GB GitHub) | Fallback |
| **Zenodo** | Cloud | Archival-grade storage, persistent DOI, CERN infrastructure | Free (50GB/record) | ⭐ Archive |
| **lakeFS** | Self-hosted | Git-like branching for large data lakes (advanced, enterprise-scale) | Free (open source) | Advanced only |
| **figshare** | Cloud | Alternative to Zenodo, unlimited public storage | Free | Alternative |

### 4.6 Experiment Tracking

| Tool | Type | Best For | Free Tier | Recommend |
|---|---|---|---|---|
| **MLflow** | Local/Cloud | Parameters, metrics, artefacts, model registry. Self-hosted. Language agnostic. | Free (open source) | ⭐ Primary |
| **DVC Experiments** | Local | Experiment tracking built into DVC — no extra tool | Free (open source) | ⭐ With DVC |
| **Weights & Biases** | Cloud | Rich visualisations, excellent for deep learning, strong academic community | Free (academic) | Optional |
| **Neptune.ai** | Cloud | Metadata store, good collaboration features | Free (academic) | Optional |

### 4.7 Documentation & Wiki

| Tool | Type | Best For | Free Tier | Recommend |
|---|---|---|---|---|
| **Confluence** | Cloud | Team wiki, industry-partner-facing docs, structured knowledge base | Free ≤10 users | ⭐ Primary |
| **Notion** | Cloud | Flexible all-in-one, good for academic teams, databases + pages | Free (generous) | ⭐ Alternative |
| **Overleaf (LaTeX)** | Cloud | Formal reports, thesis, IEEE/Elsevier papers, collaborative editing | Free basic tier | ⭐ Writing |
| **Jupyter Book** | Local | Convert notebooks to professional HTML/PDF reports | Free (open source) | Supplementary |
| **Read the Docs** | Cloud | Auto-generated API documentation from code docstrings | Free (open source) | For code docs |

### 4.8 Signal Analysis & Computing

| Tool | Type | Best For | Recommend |
|---|---|---|---|
| **Python (Jupyter)** | Local | Full analysis stack — see library list in Phase 8 | ⭐ Primary |
| **MATLAB / Simulink** | Local | System modelling, signal processing toolbox, filter design | Strong if available |
| **SciPy / NumPy** | Library | FFT, filtering, signal processing — free, open source | ⭐ Essential |
| **tsfresh** | Library | Automated time-series feature extraction (hundreds of features) | ⭐ Recommended |
| **librosa** | Library | Spectral features, MFCC — originally audio but excellent for vibration | ⭐ Recommended |
| **scikit-learn** | Library | Classical ML: SVM, RF, evaluation, cross-validation | ⭐ Essential |
| **PyTorch** | Library | Deep learning for time-series (CNN, LSTM, Transformer) | If using DL |

---

## 5. Recommended Integrated Stack

### Core Toolchain (all free, all open-source or freemium academic)

```
┌─────────────────────────────────────────────────────────────────┐
│                        GITHUB (Central Hub)                     │
│  Code (Git) + Task tracking (Projects) + CI/CD (Actions)        │
└──────────────┬──────────────────────────────────┬──────────────┘
               │                                  │
       ┌───────▼──────┐                  ┌────────▼────────┐
       │     DVC       │                 │  GitHub Projects │
       │ (data + model │                 │  (task + sprint  │
       │  versioning)  │                 │   management)    │
       └───────┬───────┘                 └─────────────────┘
               │
       ┌───────▼──────────┐
       │  Google Drive /  │
       │  AWS S3 / NAS    │
       │  (DVC remote)    │
       └──────────────────┘

┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌────────────┐
│    Notion    │  │    Overleaf  │  │    Zotero    │  │   MLflow   │
│  (wiki +     │  │  (thesis +   │  │ (literature) │  │ (experiment│
│  ELN notes + │  │   papers +   │  │              │  │  tracking) │
│  meetings)   │  │   reports)   │  │              │  │            │
└──────────────┘  └──────────────┘  └──────────────┘  └────────────┘

┌──────────────────────────────────────────────────────────────────┐
│                   ZENODO (Archive & Publication)                  │
│         Data DOI + Code DOI + FAIR compliance + ORCID link       │
└──────────────────────────────────────────────────────────────────┘
```

### How the Tools Connect

| Connection | How it works |
|---|---|
| Zotero → Overleaf | BetterBibTeX plugin auto-exports `.bib` file; Overleaf syncs from Zotero. Add a citation with `\cite{key}`. |
| GitHub → Zenodo | Enable GitHub–Zenodo integration. On each GitHub Release, Zenodo auto-archives and mints a DOI. |
| DVC → GitHub | `.dvc` pointer files committed to Git. `dvc push` sends actual data to remote. `dvc pull` retrieves it. |
| MLflow → Jupyter | Log experiments inside notebooks with `mlflow.start_run()`. Dashboard accessible via browser at `mlflow ui`. |
| Notion → Overleaf | Copy/paste or export Notion pages to Overleaf for formal report writing. Notion for drafts, Overleaf for finals. |
| OSF → Zenodo | Link your OSF project to Zenodo for automatic archival and DOI minting of published outputs. |

---

## 6. Signal Data Management

### 6.1 Data Architecture & Lineage

Every result must be fully traceable back to its origin. The data lineage for your project:

```
[Gantry Hardware]
       ↓  (motion control: position, velocity, current)
       ↓  (external sensors: vibration, temp, acoustic)
[DAQ System + Acquisition Script]
       ↓
data/raw/          ← immutable HDF5 files, DVC-tracked
       ↓  preprocess.py  (filter, resample, segment)
data/processed/    ← cleaned data, DVC-tracked
       ↓  features.py   (FFT, RMS, kurtosis, wavelets, tsfresh)
data/features/     ← feature matrices, DVC-tracked
       ↓  train.py      (SVM / RF / CNN-1D / LSTM)
models/            ← trained models, DVC-tracked, logged in MLflow
       ↓  evaluate.py   (accuracy, F1, confusion matrix, RUL curve)
reports/results/   ← figures, metrics.json, Git-tracked
       ↓
[Overleaf — paper/thesis figures]
       ↓
[Zenodo — published dataset + code with DOI]
```

**Key principle:** Raw data is **append-only and immutable**. Never overwrite or modify raw files. Every processing step outputs to a new directory.

### 6.2 File Formats

| Data Type | Recommended Format | Reason |
|---|---|---|
| Raw time-series signals | `.h5` (HDF5) | Hierarchical, compressed, metadata-embedded, fast random access, widely supported in Python/MATLAB |
| Tabular features | `.parquet` (large) or `.csv` (small) | Parquet: columnar, compressed, 10× faster than CSV for pandas. CSV: human-readable for small datasets. |
| Experiment configuration | `.yaml` or `.json` | Human-readable, git-tracked, standard for ML config. Use `params.yaml` as DVC parameter file. |
| Trained models | `.pkl`/`.joblib` (sklearn) or `.pt` (PyTorch) | Or `.onnx` for cross-framework interoperability. |
| Metadata | `metadata.json` + `README.md` | Human + machine readable. One per dataset folder. |
| Analysis reports | `.ipynb` → rendered `.html` or `.pdf` | Notebook as living analysis document. |
| System diagrams | `.svg` or `.drawio` | Vector, version-controllable in Git. Export as `.png` for reports. |

### 6.3 HDF5 Structure for Gantry PdM

```
dataset.h5
│
├── /metadata                         (HDF5 group — attributes)
│   ├── gantry_id:         "G01"
│   ├── date:              "2025-06-01"
│   ├── wear_level:        3           # integer: 0=new, 1–5=progressive wear
│   ├── wear_description:  "500km cumulative travel on X-axis guide"
│   ├── operator:          "researcher_id"
│   ├── sampling_rate_hz:  10000
│   ├── duration_s:        120
│   ├── test_condition:    "speed_sweep_100_to_500mmps"
│   ├── protocol_version:  "v1.2"
│   └── equipment:         {"daq_model": "...", "sensor_ids": [...]}
│
├── /motion_control                   (HDF5 group)
│   ├── position_x         [N×1 float32] # μm, encoder feedback
│   ├── position_y         [N×1 float32] # μm
│   ├── velocity_x         [N×1 float32] # mm/s
│   ├── motor_current_x    [N×1 float32] # A, phase current
│   ├── motor_torque_cmd   [N×1 float32] # N·m, controller output
│   └── timestamp          [N×1 float64] # seconds since epoch
│
└── /external_sensors                 (HDF5 group)
    ├── vibration_x        [N×1 float32] # m/s², accelerometer
    ├── vibration_y        [N×1 float32] # m/s²
    ├── vibration_z        [N×1 float32] # m/s²
    ├── temperature_bearing [N×1 float32] # °C
    ├── acoustic_emission   [N×1 float32] # arbitrary units (normalised)
    └── timestamp           [N×1 float64] # seconds since epoch
```

**Python snippet to write:**
```python
import h5py
import numpy as np
from datetime import datetime

with h5py.File('20250601_G01_W3_SpeedSweep_R01.h5', 'w') as f:
    # Metadata as HDF5 attributes
    meta = f.create_group('metadata')
    meta.attrs['gantry_id'] = 'G01'
    meta.attrs['wear_level'] = 3
    meta.attrs['sampling_rate_hz'] = 10000
    meta.attrs['date'] = datetime.now().isoformat()

    # Motion control signals
    mc = f.create_group('motion_control')
    mc.create_dataset('position_x', data=pos_x, compression='gzip')
    mc.create_dataset('motor_current_x', data=current_x, compression='gzip')

    # External sensors
    ext = f.create_group('external_sensors')
    ext.create_dataset('vibration_x', data=vib_x, compression='gzip')
```

### 6.4 Folder Structure

```
project-root/
│
├── .dvc/                    ← DVC configuration (git-tracked)
├── .github/
│   └── workflows/           ← GitHub Actions CI/CD pipelines
│
├── data/
│   ├── raw/                 ← IMMUTABLE. HDF5 files. DVC-tracked. Never edited.
│   ├── processed/           ← Cleaned/resampled signals. DVC-tracked.
│   ├── features/            ← Extracted feature matrices. DVC-tracked.
│   └── README.md            ← Dataset description, column definitions, collection log
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_baseline_models.ipynb
│   ├── 05_advanced_models.ipynb
│   └── 06_results_summary.ipynb
│
├── src/
│   ├── __init__.py
│   ├── preprocess.py        ← Signal cleaning, filtering, resampling
│   ├── features.py          ← Feature extraction functions
│   ├── train.py             ← Model training
│   ├── evaluate.py          ← Evaluation metrics and plots
│   └── utils.py             ← Shared helper functions
│
├── models/                  ← Saved model files. DVC-tracked.
│
├── reports/
│   ├── figures/             ← Generated plots (git or DVC tracked)
│   ├── metrics.json         ← Model evaluation metrics (git-tracked)
│   └── paper/               ← Overleaf-synced or LaTeX source
│
├── tests/
│   └── test_features.py     ← Unit tests for processing code (pytest)
│
├── dvc.yaml                 ← DVC pipeline definition
├── params.yaml              ← Experiment parameters (DVC-tracked)
├── requirements.txt         ← Python dependencies
├── environment.yml          ← Conda environment
├── README.md                ← Project overview, how to reproduce, citation
└── LICENSE                  ← Project license
```

### 6.5 File Naming Convention

**Convention:** `YYYYMMDD_GantryID_WearLevel_TestCondition_RunNumber.extension`

**Examples:**
```
20250601_G01_W0_Baseline_R01.h5       ← healthy baseline, first run
20250601_G01_W0_Baseline_R02.h5       ← healthy baseline, second run (repeat)
20250615_G01_W1_SpeedSweep_R01.h5     ← light wear, speed variation test
20250630_G01_W3_LoadSweep_R01.h5      ← moderate wear, load variation test
20250715_G01_W5_RapidDegradation_R01.h5
```

**Wear Level Key:**

| Level | Code | Description |
|---|---|---|
| 0 | W0 | New / as-received baseline |
| 1 | W1 | Light wear — first observable change |
| 2 | W2 | Moderate-light wear |
| 3 | W3 | Moderate wear |
| 4 | W4 | Severe wear |
| 5 | W5 | Near-failure / end of life |

> **Document this convention in `data/README.md` on day one and do not change it.**

### 6.6 Metadata Schema (FAIR-compliant)

Every dataset directory must contain a `metadata.json` following Dublin Core + domain extensions:

```json
{
  "dc:title": "Gantry G01 Wear Level 3 — Speed Sweep Test, Run 01",
  "dc:creator": "Researcher Name",
  "dc:date": "2025-06-01",
  "dc:description": "Time-series motion control and vibration signals collected from gantry G01 at wear level 3 (moderate wear). Speed sweep from 100 to 500 mm/s under zero load. 120 seconds duration.",
  "dc:subject": ["predictive maintenance", "gantry", "wear detection", "condition monitoring", "vibration"],
  "dc:format": "HDF5 5.1.0",
  "dc:rights": "CC-BY-4.0",
  "dc:identifier": "https://doi.org/10.5281/zenodo.XXXXXXX",

  "equipment": {
    "gantry_model": "[model name — to fill]",
    "daq_model": "[model — to fill]",
    "accelerometer_model": "[model — to fill]",
    "calibration_date": "2025-05-30"
  },
  "acquisition": {
    "sampling_rate_hz": 10000,
    "duration_s": 120,
    "channels": ["position_x", "velocity_x", "motor_current_x", "vibration_x", "vibration_y", "vibration_z", "temperature_bearing"],
    "hardware_trigger": true
  },
  "wear_state": {
    "level": 3,
    "description": "Moderate wear on X-axis linear guide",
    "cumulative_travel_km": 500,
    "visual_inspection": "Visible scoring on rail surface"
  },
  "test_condition": {
    "speed_profile": "sweep_100_to_500_mmps",
    "load_n": 0,
    "ambient_temp_c": 22.5,
    "protocol_version": "v1.2"
  },
  "provenance": {
    "related_code_repo": "https://github.com/your-org/your-repo",
    "related_code_commit": "abc1234",
    "dvc_version": "3.x",
    "python_version": "3.11.x",
    "processing_pipeline": "dvc repro"
  },
  "version": "1.0.0"
}
```

---

## 7. Compliance Checklist

### Phase 0 — Project Setup

- [ ] **GitHub repository** created (private), README, `.gitignore`, `LICENSE` added
- [ ] **DVC initialised** (`dvc init`) with remote storage configured and tested
- [ ] **OSF project created** — research questions drafted and pre-registered before experiments
- [ ] **Data Management Plan (DMP)** written using DMPOnline, approved by supervisor
- [ ] **File naming convention** documented in `data/README.md`, agreed by all team members
- [ ] **IP agreement** with industry partner clarified in writing — data ownership, publication rights
- [ ] **ORCID ID** registered for all researchers (orcid.org — free, takes 5 minutes)
- [ ] **GitHub academic account** activated (education.github.com — free Pro + Copilot for students)
- [ ] **Zenodo account** created and linked to GitHub repository
- [ ] **Zotero group library** created and shared with team

### During Research — Every Experiment

- [ ] **ELN entry created before the session** — date, gantry state, equipment checklist, protocol version
- [ ] **ELN entry completed after the session** — anomalies, observations, data quality notes
- [ ] **Code committed** to Git before running analysis — result traceable to commit hash
- [ ] **DVC add + push** after each data collection — raw data immediately backed up
- [ ] **metadata.json** written for every new dataset directory
- [ ] **MLflow run started** before training any model — parameters, data version, git hash logged
- [ ] **Notebooks cleared and re-run** before committing — verify reproducibility

### During Research — Weekly

- [ ] **GitHub Projects** board updated — tasks completed, new tasks added, blockers flagged
- [ ] **Notion/Confluence** progress update for industry partner visibility
- [ ] **DVC remote** confirmed current (`dvc status`)
- [ ] **Meeting notes** added to wiki within 24 hours of each meeting

### Pre-Milestone / Pre-Publication

- [ ] **Dataset published on Zenodo** with DOI before paper submission
- [ ] **Code published on GitHub** with tagged release and Zenodo DOI
- [ ] **FAIR compliance verified** — data has metadata, unique DOI, open format, license statement
- [ ] **Full reproducibility verified** — fresh `git clone && dvc pull && dvc repro` produces identical results
- [ ] **Industry partner review** completed — no proprietary information disclosed without approval
- [ ] **Standards cited in Methods section** — ISO 13374, ISO 17359, and relevant IEEE standards
- [ ] **All authors have ORCID** linked to the submission

---

## 8. Team Roles & Responsibilities

> **Note:** Adjust based on actual team composition. This is a template for a 3-person team.

| Role | Responsibilities | Suggested Tools Owned |
|---|---|---|
| **Principal Researcher** (student) | All experimental work, analysis, primary writing | GitHub, DVC, Jupyter, MLflow, Overleaf |
| **Academic Supervisor** | Methodology guidance, thesis review, publication approval | Overleaf (reviewer), Notion (read access) |
| **Industry Partner** | Equipment access, domain context, application validation, IP review | Confluence/Notion (view/comment), Overleaf (comment) |
| **Co-researcher** (if applicable) | Specific sub-experiments, literature support, data collection | GitHub (contributor), Zotero (shared library) |

**Communication Protocol:**

| Meeting Type | Frequency | Attendees | Format | Notes location |
|---|---|---|---|---|
| Team standup | Weekly | Research team | 15 min video/in-person | Notion — Meeting Notes |
| Supervisor meeting | Bi-weekly | Student + supervisor | 1 hour | Notion — Supervisor Log |
| Industry partner review | Monthly | All + industry | 1–2 hours | Confluence — Industry Reports |
| Sprint review | End of each sprint | Research team | 30 min | GitHub Projects |

---

## 9. Open Questions & Items to Refine

> **This section is for the team to work through together. Add your comments and decisions below each item.**

### Research Design

- [ ] **What wear levels will we study?** How many distinct states (W0–W5)? How do we create/obtain them reliably?
  - *Comment:*

- [ ] **What is the minimum dataset size per class?** How many runs per wear level to ensure statistical significance?
  - *Comment:*

- [ ] **What operating conditions will we vary?** Speed profiles, load levels, direction changes?
  - *Comment:*

- [ ] **Will we include run-to-failure experiments?** These generate the most information-rich data but consume equipment.
  - *Comment:*

- [ ] **What is the target metric for a "useful" model?** Accuracy ≥ 90%? F1-score? False-negative rate < 5%?
  - *Comment:*

### Technical Decisions

- [ ] **HDF5 or NI TDMS for raw data format?** HDF5 is more portable; TDMS if using NI LabVIEW.
  - *Decision:*

- [ ] **DVC remote storage: Google Drive, AWS S3, or university NAS?** Depends on budget, data volume, and security requirements.
  - *Decision:*

- [ ] **Will MATLAB or Python be the primary analysis environment?** MATLAB for signal processing if licenses available; Python preferred for ML/open science.
  - *Decision:*

- [ ] **Self-host eLabFTW or use OSF as ELN?** eLabFTW gives more control; OSF is simpler to set up.
  - *Decision:*

- [ ] **GitHub or GitLab?** GitHub preferred unless data must stay on-premise (security requirement from industry partner).
  - *Decision:*

### Project Management

- [ ] **Notion or Confluence for team wiki?** Notion is free and flexible; Confluence integrates with Jira.
  - *Decision:*

- [ ] **Sprint length: 1 week or 2 weeks?** 2-week sprints are standard; 1-week may suit fast-moving experimental phases.
  - *Decision:*

- [ ] **How do we handle industry partner access to data?** Full raw data access, processed only, or reports only?
  - *Decision:*

### Standards & Compliance

- [ ] **Which ISO standards are most relevant to cite in our thesis?** Confirm with supervisor.
  - *Agreed list:*

- [ ] **Does our university require a formal DMP?** If yes, use DMPOnline.
  - *Status:*

- [ ] **What is the IP agreement with the industry partner?** Who owns the dataset? Who can publish what?
  - *Status: To be confirmed with university legal/tech-transfer office*

---

## 10. References & Further Reading

### Core Standards

- ISO 13374-1:2003 — *Condition monitoring and diagnostics of machines — Data processing, communication and presentation — Part 1: General guidelines*
- ISO 17359:2018 — *Condition monitoring and diagnostics of machines — General guidelines*
- ISO 13379-1:2012 — *Condition monitoring and diagnostics of machines — Data interpretation and diagnostics techniques*
- ISO 55000:2014 — *Asset management — Overview, principles and terminology*
- IEEE Predictive Maintenance White Paper (2024) — *Predictive Maintenance in the Context of Functional Safety*
- ISO/IEC/IEEE 12207:2017 — *Systems and software engineering — Software lifecycle processes*

### Project Management

- PMI (2021). *A Guide to the Project Management Body of Knowledge (PMBOK Guide) — 7th Edition.*
- Fernandes, G. et al. (2022). *Project management practices in major university-industry R&D collaboration programs — a case study.* PMC. Available: https://pmc.ncbi.nlm.nih.gov/articles/PMC8915151/
- Axelos (2023). *PRINCE2 7th Edition.*
- ISO 21500:2021 — *Project management — Guidance*

### Research Data Management

- Wilkinson, M.D. et al. (2016). *The FAIR Guiding Principles for scientific data management and stewardship.* Scientific Data, 3, 160018.
- UK Data Service (2024). *Research Data Management Guidelines.* Available: https://ukdataservice.ac.uk/
- The Turing Way (2022). *Guide for Reproducible Research.* Available: https://book.the-turing-way.org/

### Tools — Documentation

- DVC Documentation: https://dvc.org/doc/
- GitHub Projects Guide: https://docs.github.com/en/issues/planning-and-tracking-with-projects
- OSF Getting Started: https://help.osf.io/
- eLabFTW Documentation: https://doc.elabftw.net/
- MLflow Documentation: https://mlflow.org/docs/latest/
- Overleaf Learn: https://www.overleaf.com/learn
- Zenodo Help: https://help.zenodo.org/
- Zotero Documentation: https://www.zotero.org/support/

### Predictive Maintenance — Key Papers

> *To be populated during Phase 1 — Literature Study. Add 10–15 key papers here with short annotations.*

- [ ] Add foundational PdM survey paper
- [ ] Add gantry-specific condition monitoring paper
- [ ] Add motor current signature analysis review
- [ ] Add vibration-based wear detection paper
- [ ] Add ML for PdM benchmark paper

### Python Libraries — Documentation

- h5py: https://docs.h5py.org/
- tsfresh: https://tsfresh.readthedocs.io/
- scipy.signal: https://docs.scipy.org/doc/scipy/reference/signal.html
- scikit-learn: https://scikit-learn.org/stable/user_guide.html

---

## Document Change Log

| Version | Date | Author | Changes |
|---|---|---|---|
| v1.0 | 2025-05-11 | Research Team | Initial draft — full framework |
| | | | |
| | | | |

---

*This is a living document. Every team member is responsible for keeping it up to date. Review and update at the start of each sprint.*

> **Next Review Date:** *(set at project kickoff meeting)*
