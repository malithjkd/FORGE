# Platform — Internal Software Components

> This folder contains the internal software team code. It is the Layer 5 (Product & Delivery) implementation, built using knowledge from FORGE's lower layers.

---

## Structure

```
platform/
├── data-ingestion/       → Scripts and services for collecting sensor data from ACS controllers and accelerometers
├── feature-extraction/   → Signal processing pipelines (FFT, wavelet, etc.) for extracting fault-indicative features
└── dashboard/            → Internal health monitoring dashboard and alert system
```

## Relationship to FORGE

- **Input:** Technique Notes (TN-XXX) define validated signal processing and ML methods
- **Input:** Experiment Reports (EXP-XXX) provide validated approaches and performance benchmarks
- **Input:** Architecture Decision Records (ADR-XXX) capture why specific design choices were made
- **Output:** Customer-facing prototypes, fault diagnosis modules, RUL estimation tools

## Development Guidelines

1. Every significant design choice in this codebase should have a corresponding ADR in `knowledge-commons/decision-records/`
2. Follow the Git workflow defined in `CONTRIBUTING.md` (branch → PR → review → merge)
3. Reference relevant Experiment Reports when implementing features based on validated research
4. Use `data/` folder and DVC for any large datasets or model checkpoints

---

*This folder will be populated as the internal software team begins building on FORGE's research outputs.*
