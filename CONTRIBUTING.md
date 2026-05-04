# Contributing to FORGE

> **FORGE** — Foundation for Organized Research Groups and Enterprise

This guide covers how to contribute to a FORGE-managed R&D project. Whether you are a university student, an internal team member, or a future collaborator, follow these procedures to ensure your work compounds into the shared knowledge base.

---

## Onboarding (SOP-001)

### Day 1 — Orientation

- [ ] Obtain access to the GitHub repository
- [ ] Obtain access to the Zotero group library (for academic references)
- [ ] Obtain access to the DVC data storage (for datasets and model checkpoints)
- [ ] Walk through the repository structure (30-minute session with the Research Coordinator)
- [ ] Read: `README.md`, this `CONTRIBUTING.md`, and `knowledge-commons/domain-glossary.md`
- [ ] Read: 3 completed Experiment Reports most relevant to your assigned track

### Week 1 — Shadowing

- [ ] Attend one active experiment review session
- [ ] Read 5 papers from the Zotero library (assigned by supervisor)
- [ ] Review the Technology Radar current state (`technology-radar/radar.md`)
- [ ] Identify one existing Technique Note and verify you can reproduce it

### Week 2 — First Contribution

- [ ] Write your first Experiment Proposal (even if small) using the template in `experiments/`
- [ ] Get it reviewed via GitHub Pull Request
- [ ] Execute the experiment
- [ ] Write the Experiment Report

### Ongoing Expectations

- All work must be documented in FORGE **before** presenting results in any meeting
- Monthly contribution of at least one document (Technique Note, ADR, Dead-End entry, or Experiment Report)
- Any decision made in a meeting or chat must be captured in a document within 48 hours

---

## Running an Experiment (SOP-002)

### Before You Start

- [ ] Your Experiment Proposal exists in `experiments/active/` and is approved
- [ ] Required data is accessible (`dvc pull` confirmed, if applicable)
- [ ] Required hardware or lab access is confirmed

### During Execution

- [ ] Maintain a running Experiment Log (informal daily notes in the experiment folder)
- [ ] If your method deviates from the proposal, document the change and reason immediately
- [ ] If results suggest the experiment should stop early (failure confirmed or success exceeded), flag to your supervisor before stopping

### On Completion

- [ ] Write the Experiment Report within **5 working days** of completion
- [ ] Move your proposal from `experiments/active/` to `experiments/complete/`
- [ ] Commit all data with DVC and push
- [ ] Commit all code and push
- [ ] Update the Technology Radar if a technique was newly assessed
- [ ] Create a Dead-End entry (`DE-XXX`) if a dead end was reached
- [ ] Create a Technique Note (`TN-XXX`) if a reusable technique was established
- [ ] Post a 3-sentence summary in the team communication channel

---

## Document Types at a Glance

| Type | Code | When to Create | Template Location |
|---|---|---|---|
| Technique Note | `TN-XXX` | After a method has been successfully applied at least once | `knowledge-commons/technique-notes/_TEMPLATE_technique_note.md` |
| Architecture Decision Record | `ADR-XXX` | When a significant design or technical choice is made | `knowledge-commons/decision-records/_TEMPLATE_adr.md` |
| Dead-End Entry | `DE-XXX` | When an approach is tried and confirmed not to work | `knowledge-commons/dead-end-registry/_TEMPLATE_dead_end.md` |
| Experiment Proposal | `EXP-XXX-PROPOSAL` | Before any experiment begins | `experiments/_TEMPLATE_experiment_proposal.md` |
| Experiment Report | `EXP-XXX-REPORT` | After any experiment ends (win or lose) | `experiments/_TEMPLATE_experiment_report.md` |

---

## Git Workflow

1. Create a branch: `git checkout -b feat/short-description` or `git checkout -b exp/EXP-XXX-short-title`
2. Make small, focused commits with clear messages
3. Push and open a Pull Request against the `main` branch
4. Request at least one reviewer
5. Merge after approval

---

## Key Rules

1. **Document first, present second** — No work is "done" until it is in the repository.
2. **Dead ends are mandatory** — No approach may be declared "we already tried that" without a `DE-XXX` entry to prove it.
3. **Templates are not optional** — Use the provided templates. They exist to ensure consistency and completeness.
4. **Conversations are ephemeral; documents are permanent** — Any decision from a meeting or chat must be captured in a document within 48 hours.

---

*Questions? Open an issue in the repository or contact the Research Coordinator.*
