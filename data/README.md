# Data Catalogue

> This folder contains **metadata, labels, and data cards** — not raw data files. Actual sensor data and model weights are stored externally and managed via [DVC (Data Version Control)](https://dvc.org/).

---

## Setup

### Prerequisites

- Git repository cloned
- DVC installed (`pip install dvc`)
- Access to the configured DVC remote backend (Google Drive, NAS, or S3)

### Fetching Data

```bash
# Pull all tracked data files
dvc pull

# Pull a specific dataset
dvc pull data/datasets/<dataset-name>.dvc
```

---

## Folder Structure

```
data/
├── datasets/          # Dataset metadata and DVC pointer files
│   └── .gitkeep
├── models/            # Model cards and checkpoint references
│   └── .gitkeep
└── README.md          # This file
```

---

## Data Card Template

When adding a new dataset, create a data card in `datasets/` with the following structure:

```markdown
# Dataset: [Name]

**Created:** [YYYY-MM-DD]  
**Created By:** [Name]  
**Related Experiment:** [EXP-XXX]  
**DVC File:** [filename.dvc]

## Description
What does this dataset contain? How was it collected?

## Collection Parameters
- Sensor(s): [e.g., CTCOnline accelerometer, PT100, ACS PE]
- Sampling rate: [e.g., 10 kHz]
- Duration: [e.g., 2 hours]
- Conditions: [e.g., normal operation, simulated friction fault]

## Schema
| Column | Type | Unit | Description |
|--------|------|------|-------------|
| ... | ... | ... | ... |

## Known Limitations
- [e.g., "Collected on Setup A only — transferability not validated"]
```

---

*Keep this catalogue updated. Every dataset must have a data card before it can be referenced in Experiment Reports.*
