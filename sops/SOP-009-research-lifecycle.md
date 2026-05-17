# SOP-009: Research Lifecycle Navigation

> **Source:** [Research Lifecycle](../00_system_design/08_research_lifecycle.md)  
> **Trigger:** Starting any new research activity or onboarding a new contributor  
> **Owner:** Every researcher

---

## How to Use the Research Lifecycle

The FORGE research lifecycle has 15 stages organised into phases. You don't need to follow them rigidly — but you must know **where you are** and **what outputs are expected** at each stage.

---

## Quick Reference: Where Am I?

```
Stages 1-2:   EXPLORE      → Search literature, identify gaps
Stages 3-4:   DEFINE       → Form hypothesis, write EXP Proposal
Stages 5-6:   DESIGN       → Test design, simulation, feasibility
Stages 7-8:   COLLECT      → Setup equipment, acquire data
Stages 9-10:  DOCUMENT     → Metadata, version control, backup
Stages 11-12: ANALYSE      → Features, models, interpretation
Stages 13-14: VALIDATE     → Reproducibility, evaluation, go/no-go
Stage 15:     PUBLISH      → Thesis, papers, Zenodo release
```

---

## Stage-Gate Checkpoints

Before crossing a gate, verify you have the required deliverables:

| Gate | Between Stages | Required Before Proceeding |
|------|---------------|---------------------------|
| **Gate 0** | Before Stage 1 | GitHub access, DVC configured, ORCID registered |
| **Gate 1** | After Stage 2 | ≥30 papers reviewed, gap analysis written |
| **Gate 2** | After Stage 6 | Test protocol approved, feasibility confirmed |
| **Gate 3** | After Stage 10 | All datasets collected, FAIR compliance verified |
| **Gate 4** | After Stage 14 | Model evaluation complete, `dvc repro` passes |
| **Gate 5** | After Stage 15 | Thesis submitted, data published with DOI |

---

## Sprint Mapping Guide

| Sprint Type | Research Stages | Duration | Key Output |
|-------------|----------------|----------|------------|
| Literature Sprint | 1–2 | 2 weeks | Annotated bibliography, gap analysis |
| Design Sprint | 3–6 | 2 weeks | EXP Proposal, test protocol |
| Experiment Sprint | 7–8 | 2 weeks | Raw datasets (DVC-tracked) |
| Analysis Sprint | 9–13 | 2 weeks | EXP Report, trained models |
| Review Sprint | 14 | 1 week | Go/No-Go decision, Radar update |
| Writing Sprint | 15 | 2 weeks | Thesis chapter or paper draft |

---

## ISO 13374 Layer Tagging

When working on Stages 7–14, tag your experiment with the applicable ISO 13374 layer(s):

| Your Activity | ISO 13374 Layer |
|---------------|----------------|
| Collecting raw signals | ISO Layer 1: Data Acquisition |
| Filtering, resampling | ISO Layer 2: Data Manipulation |
| Extracting features (FFT, RMS) | ISO Layer 3: State Detection |
| Classifying wear states | ISO Layer 4: Health Assessment |
| Predicting remaining life | ISO Layer 5: Prognostics |
| Generating recommendations | ISO Layer 6: Advisory |

---

## Checklist: Starting a New Research Activity

- [ ] Search Dead-End Registry (SOP-006) — has this been tried?
- [ ] Search Technique Notes — is there an existing method?
- [ ] Check Technology Radar — what's the current assessment?
- [ ] Write Experiment Proposal using template
- [ ] Get proposal reviewed (Gate 2 if scoring required)
- [ ] Begin execution per SOP-002

---

*See [08_research_lifecycle.md](../00_system_design/08_research_lifecycle.md) for the full lifecycle model with diagrams and detailed stage descriptions.*
