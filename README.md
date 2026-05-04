# FORGE — Foundation for Organized Research Groups and Enterprise

> A knowledge architecture and compound learning system for managing R&D projects that outlive any single person, idea, or technology choice.

---

## What Is FORGE?

FORGE is a **reusable blueprint** for organizing R&D knowledge so that it compounds over time. Instead of treating research as a linear project with a fixed endpoint, FORGE treats **knowledge as the primary output** — products, prototypes, and tools are valuable byproducts of accumulated understanding.

FORGE was created at [PBA Systems](https://www.pbasystems.com/) to support predictive maintenance research on precision gantry systems, but the architecture is **project-agnostic** — it can be instantiated for any R&D initiative.

### Core Principles

- **Knowledge compounds** — each experiment builds on prior ones
- **Failure is documented** — dead ends are first-class knowledge, not hidden shame
- **No single point of failure** — the system does not depend on one person, path, or technology
- **Multiple contributors** — universities, internal teams, and future hires all feed the same system
- **LLM-native** — Markdown + Git is natively queryable by AI tools

---

## Repository Structure

```
FORGE/
├── 00_system_design/              → FORGE's own design documents (vision, architecture)
├── knowledge-commons/             → Documented understanding (Layer 2)
│   ├── technique-notes/           → TN-XXX: How to do specific tasks
│   ├── decision-records/          → ADR-XXX: Why design choices were made
│   ├── dead-end-registry/         → DE-XXX: What was tried and didn't work
│   └── domain-glossary.md         → Shared vocabulary
├── experiments/                   → Operational heartbeat (Layer 3)
│   ├── active/                    → In-progress experiments
│   ├── complete/                  → Completed experiment reports
│   └── backlog/                   → Proposed but not yet started
├── data/                          → Data foundation (Layer 1)
│   ├── datasets/                  → Metadata & data cards (actual data via DVC)
│   └── models/                    → Model cards & checkpoint references
├── technology-radar/              → Portfolio intelligence (Layer 4)
│   ├── radar.md                   → Current assessment of techniques & tools
│   └── history/                   → Past snapshots
└── reports/                       → Formal summaries for management
    └── monthly/
```

---

## How to Use This Blueprint

### For a New Project

1. Clone or fork this repository
2. Update `knowledge-commons/domain-glossary.md` with your project-specific terms
3. Write your first Experiment Proposal using the template in `experiments/`
4. Populate the Technology Radar with your current landscape
5. Follow `CONTRIBUTING.md` for onboarding new team members

### For Contributors

See [CONTRIBUTING.md](./CONTRIBUTING.md) for onboarding steps and standard operating procedures.

---

## Key Documents

| Document | Description |
|---|---|
| [Vision & Motivation](./00_system_design/01_vision_and_motivation.md) | Why FORGE exists — the founding thinking |
| [Knowledge Architecture](./00_system_design/02_knowledge_architecture.md) | Full system design — layers, templates, SOPs, tooling, rollout plan |
| [Domain Glossary](./knowledge-commons/domain-glossary.md) | Shared vocabulary across all contributors |
| [Technology Radar](./technology-radar/radar.md) | Current state of technique and tool assessment |
| [Contributing Guide](./CONTRIBUTING.md) | How to contribute to this FORGE instance |

---

## Future Modules (Planned)

| Module | Status | Description |
|---|---|---|
| Module 1: Knowledge Architecture | ✅ Complete | This document and the system design folder |
| Module 2: Portfolio Architecture | 🔲 Planned | Multi-track parallel research management |
| Module 3: Collaboration Protocol | 🔲 Planned | University–industry working interface |
| Module 4: Failure Integration Loop | 🔲 Planned | Structured retrospectives and dead-end analysis |

---

*FORGE is a living system. This repository is subject to continuous improvement. Every significant change should be made via Pull Request with a brief rationale, so the history of the system's own evolution is preserved.*
