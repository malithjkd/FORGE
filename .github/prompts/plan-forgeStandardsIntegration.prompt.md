# Implementation Plan: FORGE + Industry Standards Integration

**TL;DR:** FORGE's foundation is strong. Add four modules to align with international standards (ISO 13374, FAIR data, portfolio architecture, collaboration governance) without new tools — just formalize what you're already doing via GitHub + DVC + Mendeley + W&B.

---

## Executive Summary: Current State & Gaps

### What FORGE Is Doing Well ✓
1. **Experiment lifecycle** — Proposal → Execution → Report → Retrospective is solid
2. **Knowledge capture** — Technique Notes, ADRs, Dead-End Registry structure is excellent
3. **Version control** — Git + DVC architecture is industry-standard
4. **Compound learning** — 5-layer architecture encourages knowledge accumulation

### What's Missing 🔴
1. **Standards alignment** — No explicit mapping to ISO 13374 (condition monitoring standard)
2. **FAIR data compliance** — No persistent identifiers (DOI), machine-readable metadata, formal licensing
3. **Portfolio architecture** — No stage-gate decision model, no go/no-go criteria for experiments
4. **Collaboration governance** — No documented roles, decision rights, or IP ownership framework

### Why This Matters (University Perspective)
- **University of Moratuwa** requires demonstrated research governance
- **Thesis publication** requires FAIR-compliant datasets with DOI
- **IP clarity** protects both PBA and UoM in joint ventures
- **Industry standards** (ISO 13374) legitimize the methodology for future customers

---

## Implementation Roadmap: 4 Phases

### PHASE 1: FAIR Data Compliance (Weeks 1-2) — Foundation Layer
**Goal:** Make FORGE datasets discoverable, reusable, and institution-compliant  
**Effort:** ~15 hours (mostly documentation templates, minimal code)  
**Enforcement:** Advisory (templates provided, adoption optional per your preference)

#### Phase 1 Tasks

**1.1 Establish Persistent Identifiers**
- [ ] Register FORGE project on Zenodo (zenodo.org) — creates institutional archival
- [ ] Create Zenodo community: "FORGE Predictive Maintenance Research"
- [ ] Connect GitHub repo to Zenodo for auto-DOI on releases
- [ ] Add ORCID profiles for all contributors (5 min/person)
- [ ] Document in: `SOP-007-FAIR-Data-Compliance.md` (new SOP)

**1.2 Formalize Metadata**
- [ ] Create `data/METADATA_TEMPLATE.md` using Dublin Core 15 elements
- [ ] Add JSON-LD snippet to each dataset card (template provided)
- [ ] Update `data/README.md` with license declarations (CC-BY-4.0 recommended)
- [ ] Add LICENSE file to repo root

**1.3 Create FAIR Checklist**
- [ ] Add to every experiment report: FAIR compliance tick-box
  ```markdown
  ## FAIR Compliance Checklist
  - [ ] Dataset has unique DOI/Zenodo handle
  - [ ] Rich metadata (title, creator, date, license)
  - [ ] Access restrictions documented
  - [ ] Provenance statement included
  - [ ] Contact info for reuse questions
  ```

**Deliverable:** 
- SOP-007 document (1000 words)
- Metadata templates (templates only, no data changes yet)
- FAIR checklist integration into Experiment Report template

**Tools Used:** Zenodo (free), GitHub, no new tools

---

### PHASE 2: ISO 13374 Standards Mapping (Weeks 3-4) — Domain Alignment
**Goal:** Align FORGE's Layer 3 (Experiment Engine) with condition monitoring standards  
**Effort:** ~12 hours (primarily documentation, no code changes)  
**Enforcement:** Advisory (reference model, not mandatory)

#### Phase 2 Tasks

**2.1 Map FORGE to ISO 13374**
- [ ] Create `00_system_design/08_ISO13374_mapping.md`
- [ ] Document how each FORGE layer aligns with ISO 13374-1's 6-layer chain:
  ```
  FORGE Layer 1 (Data) ↔ ISO Layer 1 (Data Acquisition)
  FORGE Layer 2 (Knowledge) ↔ ISO Layer 2 (Data Manipulation)  
  FORGE Layer 3 (Experiments) ↔ ISO Layers 3-4 (State Detection + Health)
  [Missing] ↔ ISO Layer 5 (Prognostics / RUL)
  [Missing] ↔ ISO Layer 6 (Advisory / Maintenance Recommendations)
  ```

**2.2 Create ISO 13374 Experiment Template**
- [ ] Add new optional section to Experiment Proposal:
  ```markdown
  ## ISO 13374 Compliance
  - Which layer(s) does this experiment target? (1-6)
  - What signals/features map to that layer?
  - What is the output at each layer?
  ```

**2.3 Document Condition Monitoring Features**
- [ ] Create `knowledge-commons/technique-notes/TN-ISO-FEATURE-EXTRACTION.md`
- [ ] Table of standard signal features for gantry systems:
  | Feature | Domain | ISO Layer | Tool |
  |---|---|---|---|
  | RMS (Root Mean Square) | Time | Layer 2 | Python scipy |
  | FFT (Fast Fourier Transform) | Frequency | Layer 2 | NumPy/scipy |
  | Kurtosis | Statistical | Layer 2 | scipy.stats |
  | Envelope Analysis | Time-Frequency | Layer 2 | PyEMD |
  | Wavelet Coefficients | Time-Frequency | Layer 2 | PyWavelets |

**2.4 Add ISO 13374 to Technology Radar**
- [ ] Update `technology-radar/radar.md`
- [ ] For each ML technique, document which ISO layer it's used for:
  ```
  **1D-CNN for Fault Classification**
  - ISO Layer: 4 (Health Assessment)
  - Status: TRIAL (validated on EXP-005 dataset)
  - Strengths: Captures spatial-temporal patterns
  - Limitations: Black-box, hard to interpret for domain experts
  ```

**Deliverable:**
- `08_ISO13374_mapping.md` (comprehensive reference)
- Updated Experiment Proposal template (1-2 new sections)
- ISO 13374 feature extraction TN (technique note)
- Technology Radar ISO mapping

**Tools Used:** Markdown editor, no new tools

---

### PHASE 3: Portfolio Architecture & Decision Framework (Weeks 5-8) — Strategic Layer
**Goal:** Define go/no-go criteria, track prioritization, and metrics for Layer 4  
**Effort:** ~20 hours (mostly framework design, can be iterative)  
**Enforcement:** Advisory (framework provided, teams adopt as suits their culture)

#### Phase 3 Tasks

**3.1 Design Stage-Gate Model**
- [ ] Create `00_system_design/09_portfolio_architecture.md` 
- [ ] Define 5 decision gates for FORGE experiments:
  ```
  Gate 0: Discovery (Is this aligned with research questions?)
  Gate 1: Scoping (Is it technically feasible in 2-4 weeks?)
  Gate 2: Go/No-Go Decision (Does it pass weighted scoring?)
  Gate 3: Mid-Execution Review (On track for milestones?)
  Gate 4: Completion Review (Did we learn what we expected?)
  ```

**3.2 Create Go/No-Go Scoring Rubric**
- [ ] Template: `knowledge-commons/decision-records/ADR-EXPERIMENT-SCORING.md`
- [ ] Weighted scoring model:
  ```
  Strategic Alignment (30%)      [0-10 scale]
  Technical Feasibility (25%)    [0-10 scale]
  Resource Efficiency (25%)      [0-10 scale]
  Expected Impact (20%)          [0-10 scale]
  ────────────────────────────
  PASS threshold: ≥ 65 points
  ```

**3.3 Map Experiment Dependencies**
- [ ] Create `experiments/DEPENDENCY_GRAPH.md`
- [ ] Document which experiments are:
  - Sequential (EXP-001 → EXP-002)
  - Parallel (EXP-003 || EXP-004)
  - Convergent (EXP-005A + EXP-005B → decision)
- [ ] Use Mermaid diagram (already used in CONTRIBUTING.md)

**3.4 Define Portfolio KPIs**
- [ ] Add to `technology-radar/radar.md` quarterly section:
  ```
  ## Q2 2026 Portfolio Metrics
  - Experiments completed: 3 / 5 planned (60%)
  - Average time-to-insight: 4 weeks
  - Technique transition rate: 1/3 in Trial → Adopt
  - Dead-end discovery rate: 20% (learning velocity)
  - Resource utilization: 85%
  ```

**3.5 Create Layer 4 Experiment Dashboard**
- [ ] Update GitHub Projects with "Portfolio View"
  - Milestone: "Portfolio Quarterly Review"
  - Custom fields: Experiment stage, Track, Priority score
- [ ] Configure W&B (if used for ML tracking) to report portfolio-level metrics

**Deliverable:**
- `09_portfolio_architecture.md` (10-15 pages)
- Go/No-Go scoring templates
- Experiment dependency map
- Updated GitHub Projects with portfolio-level tracking
- Portfolio KPI specification (for future dashboard)

**Tools Used:** GitHub Projects, W&B (optional for ML experiments), Markdown

---

### PHASE 4: Collaboration Protocol & Governance (Weeks 9-12) — Institutional Layer
**Goal:** Formalize roles, decision rights, and IP framework for university-industry partnership  
**Effort:** ~25 hours (high-impact, requires stakeholder alignment)  
**Enforcement:** Advisory (protocol documented, adoption varies by team)

#### Phase 4 Tasks

**4.1 Define Collaboration Module (Module 4)**
- [ ] Create `00_system_design/04_collaboration_protocol.md`
- [ ] Document:
  - Stakeholder roles & decision matrix (PBA, University, Students, Support)
  - Steering committee structure (monthly + biweekly sync)
  - Escalation pathways (who decides what, when to escalate)

**4.2 Create IP Ownership Framework**
- [ ] Template: `knowledge-commons/decision-records/ADR-IP-OWNERSHIP.md`
- [ ] Build ownership matrix for work products:
  ```
  | Work Product | Owner | Publication Rights | Notes |
  | Raw Data | Shared | UoM thesis use, PBA product | DOI + access control |
  | Code | PBA | Methodology publishable | Proprietary implementation |
  | Models | PBA | Architecture publishable | Weights proprietary |
  | Datasets | Shared | Joint publication only | Hold-out test set protected |
  | Thesis | UoM | Student decides | 30-day PBA review |
  ```

**4.3 Establish Communication Protocol**
- [ ] Create `SOP-008-collaboration-communication.md`
- [ ] Define meeting cadence:
  ```
  Weekly (Monday 10am):  Lab standup (30 min)
  Biweekly (Tuesday):    Technical sync (60 min)
  Monthly (Fridays):     Steering committee (120 min)
  ```
- [ ] Decision logging: All steering decisions logged in GitHub discussions

**4.4 Create Student Onboarding for Collaboration**
- [ ] Update `SOP-001-onboarding.md` with:
  - IP awareness training (1-hour)
  - Publication review process (timeline)
  - Escalation path for disagreements
  - Decision log access

**4.5 Approval Gates**
- [ ] Decision points requiring both signatures:
  ```
  [ ] Publication submissions (30-day review window)
  [ ] Dataset release decisions (Zenodo/public)
  [ ] Thesis scope changes (major)
  [ ] IP classification changes
  ```

**Deliverable:**
- `04_collaboration_protocol.md` (comprehensive module)
- IP ownership framework & decision matrix
- Meeting templates & decision log structure
- Updated SOP-001 with collaboration awareness
- Communication protocol SOP-008

**Tools Used:** GitHub Discussions (for decision logging), Markdown, no new tools

---

## Implementation Timeline & Dependencies

```
Week 1-2:  PHASE 1 (FAIR) ──────────────────────────────┐
             [SOP-007, Metadata templates, Checklist]   │
                                                         │
Week 3-4:  PHASE 2 (ISO 13374) ─────────────────────────┤── Can run in parallel
             [Mapping, Feature TN, Radar update]        │
                                                         │
Week 5-8:  PHASE 3 (Portfolio) ────────────────────────── (depends on clarity)
             [Stage-gates, Scoring, KPIs]               │
                                                         │
Week 9-12: PHASE 4 (Governance) ────────────────────────── (can overlap Phase 3)
             [IP framework, Protocol, Comms SOP]        │
                                                         │
RESULT:    Complete FORGE v1.0 ────────────────────────┘
           (Standards-aligned, University-ready)
```

**Critical Path:** Phase 1 (FAIR) should start immediately — it's foundational.  
**Parallel Opportunity:** Phases 2 & 3 can overlap if you have 2+ people.  
**Gating:** Phase 4 requires stakeholder input, so schedule University meeting early (Week 1).

---

## What's NOT Changing (Keep Current Approach)

✓ **Git + DVC architecture** — Stay with current model  
✓ **Experiment lifecycle** (Proposal → Report) — Already aligned  
✓ **Knowledge Commons structure** — Already strong  
✓ **Technology Radar** — Expand, don't replace  
✓ **Tool stack:** GitHub + Mendeley + W&B (no additions)

---

## What Gets Added (Without New Tools)

📝 **Documentation** (Markdown in FORGE repo):
- SOP-007 (FAIR compliance)
- SOP-008 (Collaboration communication)
- 08_ISO13374_mapping.md
- 09_portfolio_architecture.md
- 04_collaboration_protocol.md

🎯 **Templates** (in knowledge-commons/):
- FAIR metadata checklist
- ISO 13374 feature extraction guide
- Go/No-Go scoring rubric
- IP ownership matrix

🛠️ **Configuration** (GitHub Projects):
- Portfolio-level views
- Custom fields for experiment staging
- KPI metrics

---

## Success Criteria: How You'll Know It's Working

### Phase 1 (FAIR)
- [ ] First dataset published to Zenodo with DOI
- [ ] All new experiment reports include FAIR checklist
- [ ] University approves data governance approach

### Phase 2 (ISO 13374)
- [ ] All experiments reference their ISO 13374 layer
- [ ] Technology Radar documents techniques against ISO standard
- [ ] New technique notes include layer mapping

### Phase 3 (Portfolio)
- [ ] Go/No-Go decisions documented in GitHub Issues
- [ ] Monthly portfolio KPI review in steering meeting
- [ ] Experiments have priority scores tied to gate decisions

### Phase 4 (Governance)
- [ ] First publication submitted with clear authorship (PBA/UoM alignment)
- [ ] No IP disputes or clarification requests
- [ ] Steering committee decisions logged & approved

---

## Remaining Questions to Resolve with University

1. **FAIR Compliance Audit** — Does UoM have a formal audit process? When should we trigger it?
2. **Publication Timeline** — What's the expected timeline for thesis + conference papers?
3. **Data Embargo** — Are there any embargo periods before datasets can be released?
4. **Collaboration Model** — Is PM.UIC (academic framework) already adopted by UoM, or do they have their own?
5. **Steering Committee Composition** — Who should be UoM's representative (advisor vs. researcher vs. admin)?

---

## Risk Mitigation

| Risk | Mitigation |
|---|---|
| Tool proliferation creep | Stay with GitHub Projects for portfolio tracking; no new software |
| Documentation overhead | Keep templates simple; advisory, not mandatory |
| University bureaucracy | Clarify governance early (Week 1) to avoid rework |
| Student resistance | Frame standards as "thesis publication requirement," not compliance burden |
| IP disputes | Resolve ownership matrix NOW before first publication attempt |

---

## Next Steps (Immediate)

1. **Review this plan** with your team (30 min)
2. **Schedule University meeting** (Week 1) to discuss Phases 1 & 4
3. **Assign Phase leads:**
   - Phase 1 (FAIR): [someone comfortable with metadata/publishing]
   - Phase 2 (ISO 13374): [domain expert, likely you]
   - Phase 3 (Portfolio): [PM-minded team member]
   - Phase 4 (Governance): [you + University liaison]
4. **Create GitHub milestone** "FORGE v1.0 Standards Integration" with 4 sub-milestones
5. **Start Phase 1** immediately (FAIR is foundational, takes 2 weeks)

---

## Key Takeaways

### Why This Plan Works
1. **No tool proliferation** — Stays with GitHub + Mendeley + W&B
2. **Standards-aligned** — ISO 13374 + FAIR + PM.UIC frameworks
3. **Advisory, not mandatory** — Templates provided; adoption optional
4. **University-ready** — Addresses governance + publishing requirements
5. **Layered rollout** — 12 weeks to full implementation, can be phased

### What Gets Better
- 📊 **Data governance** — FAIR compliance enables publication & reproducibility
- 🎯 **Decision-making** — Portfolio model enables parallel track management
- 👥 **Collaboration** — Governance framework prevents IP disputes
- 📈 **Scalability** — Framework replicable for future projects & partnerships

### Competitive Advantage
Your competitors can copy your product. They cannot copy your system for generating, documenting, and protecting knowledge. FORGE + standards = your moat.

---

## Appendix: Gap Analysis Summary

| Dimension | Current State | Gap | Priority | Solution Phase |
|---|---|---|---|---|
| Data compliance | Partial (Git/DVC) | FAIR formalization | High | Phase 1 |
| Standards alignment | Implicit | ISO 13374 explicit mapping | High | Phase 2 |
| Portfolio management | Not implemented | Decision framework | Medium | Phase 3 |
| Collaboration governance | Not documented | Role/decision matrix | High | Phase 4 |
| Tool complexity | 4 tools (GitHub, Mendeley, W&B, DVC) | No new tools | ✓ Met | N/A |
| Enforcement model | Not specified | Advisory (optional) | ✓ Met | N/A |
