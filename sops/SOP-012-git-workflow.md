# SOP-012: Git Workflow, GitHub Issues & Projects

> **Source:** Adapted from DEV-003 (Git Workflow SOP)  
> **Scope:** All code repositories in the FORGE project GitHub organisation  
> **Owner:** Team Lead  
> **Standards Basis:** ISO 10007:2017 (Configuration Management), Conventional Commits 1.0.0, Semantic Versioning 2.0.0

---

## 1. Purpose

This SOP defines how FORGE projects use Git, GitHub Issues, and GitHub Projects to plan, track, and deliver software work. Every rule here is enforceable — branch protection and CI checks are configured to reject non-compliant work automatically.

---

## 2. Repository Structure

### 2.1 One Repository Per Project

Each project has its own repository. Shared utility code lives in a shared tools repository and is imported as a versioned package — never copy-pasted between repos.

### 2.2 Repository Contents

See [SOP-010](./SOP-010-software-development.md) §5.2 for the standard repository structure.

---

## 3. Branch Strategy

### 3.1 Permanent Branches

| Branch | Purpose | Who Can Merge | Direct Push |
|--------|---------|---------------|-------------|
| `main` | Production-ready code. Every commit is deployable. | Team Lead + Technical Lead | Never |
| `develop` | Integration and staging. Features merge here first. | Team Lead | Never |

Both `main` and `develop` are **protected branches** with branch protection rules enabled.

### 3.2 Short-Lived Branches

| Pattern | Created From | Merges Into | Who Creates | Lifetime |
|---------|-------------|------------|-------------|----------|
| `feature/#NNN-description` | `develop` | `develop` | Developer, Team Lead | Until story done |
| `fix/#NNN-description` | `develop` | `develop` | Developer, Team Lead | Until bug fixed |
| `hotfix/#NNN-description` | `main` | `main` AND `develop` | Team Lead + Technical Lead | Until emergency resolved |
| `research/#NNN-description` | `develop` | `develop` | Research Students | Until research task done |
| `docs/#NNN-description` | `develop` | `develop` | Any team member | Until docs update complete |

### 3.3 Branch Naming Rules

```
Pattern:   <type>/#<issue-number>-<short-description>
Separator: hyphens only — no spaces, no underscores, no capitals
Length:    3–6 words for the description

Examples (correct):
  feature/#42-thermal-grid-calibration
  fix/#67-null-pointer-csv-export
  research/#88-lstm-anomaly-detection
  docs/#15-update-readme-setup-steps

Examples (wrong):
  Feature_42_Thermal_Grid          ← capitals and underscores
  feature/thermal-calibration      ← missing issue number
  feature/#42                      ← missing description
  my-branch                        ← no type, no issue number
```

### 3.4 The `develop` → `main` Promotion

`develop` is promoted to `main` at the end of each sprint, after review and Technical Lead approval:

```
Sprint ends → Sprint Review passed → Technical Lead reviews develop → 
Tag release → Merge develop → main → Deploy
```

---

## 4. Conventional Commits

All commits must follow the **Conventional Commits 1.0.0** specification. CI rejects non-compliant messages.

### 4.1 Format

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### 4.2 Commit Types

| Type | When to Use | Version Bump |
|------|-------------|--------------|
| `feat` | New feature or capability | Minor (1.x.0) |
| `fix` | A bug fix | Patch (1.0.x) |
| `docs` | Documentation only | None |
| `test` | Adding or updating tests | None |
| `refactor` | Restructuring without behaviour change | None |
| `perf` | Performance improvement | Patch |
| `build` | Build system or dependency changes | None |
| `ci` | CI/CD pipeline changes | None |
| `chore` | Maintenance tasks | None |
| `research` | Experimental work on `research/*` branches only | None |

### 4.3 Description Rules

- Imperative mood: "add calibration" not "added calibration"
- No capital letter at the start
- No period at the end
- Maximum 72 characters total
- Must complete: "This commit will ___"

### 4.4 Breaking Changes

Mark with `!` after type/scope:

```
feat(api)!: change response format for inference endpoint
```

Or use `BREAKING CHANGE:` footer:

```
refactor(data): rename preprocessing module

BREAKING CHANGE: PreprocessorV1 class renamed to DataPreprocessor.
Update all imports.
```

### 4.5 Issue References

Always link commits to Issues:

```
Closes #42       ← closes issue on merge
Fixes #42        ← same
Refs #42         ← links without closing (partial work)
```

### 4.6 Full Examples

```
feat(pipeline): add automated data validation on ingest

Validates schema, checks for null sensor readings, and flags
samples where vibration exceeds 3σ from rolling 24-hour mean.
Invalid samples are quarantined, not dropped.

Closes #91
Refs #85
```

```
fix(inference): correct feature normalization for batch predictions

The scaler was being re-fitted per batch instead of using the
training-time parameters. This caused inconsistent predictions.

Fixes #67
```

---

## 5. GitHub Issues

### 5.1 Issue Types and Labels

| Label | When to Use |
|-------|------------|
| `type: user-story` | Feature from the user's perspective |
| `type: bug` | Something is broken |
| `type: research` | Exploratory or ML research task |
| `type: tech-debt` | Refactor with no new user behaviour |
| `type: docs` | Documentation only |
| `type: epic` | Large body of work grouping other issues |
| `type: incident` | Production failure requiring immediate response |
| `priority: critical` | Blocking production or deadline |
| `priority: high` | Important for current sprint |
| `priority: medium` | Planned for near future |
| `priority: low` | Parking lot |

### 5.2 User Story Template

```markdown
## User Story

**As a** [persona],
**I want to** [action],
**so that** [benefit].

## Acceptance Criteria

- [ ] **GIVEN** [context], **WHEN** [action], **THEN** [expected result]

## Story Points: [1/2/3/5/8]
## Priority: [Critical/High/Medium/Low]
## Epic: #[issue number or "none"]
```

### 5.3 Research Task Template

```markdown
## Research Question
[State a specific question, not a task]

## Approach
**Dataset:** [Which dataset, version, size]
**Method:** [What you will try]
**Baseline:** [What "good" means]

## Success Criteria
- [ ] [Metric] exceeds [threshold] on [test set]
- [ ] Results reproducible with fixed random seed
- [ ] Experiment logged with all hyperparameters

## Time Box: [maximum time before stopping]
```

---

## 6. GitHub Projects (Sprint Board)

### 6.1 Board Columns

| Column | What Goes Here |
|--------|---------------|
| **Backlog** | All prioritised issues not yet in a sprint |
| **Sprint — To Do** | Committed to current sprint, not started |
| **In Progress** | Actively being worked on (max 2 per person) |
| **In Review** | PR open, waiting for review |
| **Done** | All DoD criteria met, merged |
| **Blocked** | Cannot proceed — annotate with blocker |

### 6.2 Sprint Workflow

```
Sprint Planning:
  1. Open Backlog view
  2. Drag top-priority issues into current Sprint
  3. Set Story Points
  4. Issues move to "Sprint — To Do"

During Sprint:
  1. Developer picks up issue → "In Progress"
  2. Creates branch: feature/#NNN-description
  3. PR opened → "In Review"
  4. PR merged → issue auto-closes → "Done"

Sprint Review:
  1. Filter Done column by current sprint
  2. Demo each closed issue
  3. Undone items return to Backlog
```

---

## Cross-References

| Document | Relationship |
|----------|-------------|
| [SOP-010](./SOP-010-software-development.md) | Development workflow and repository structure |
| [SOP-011](./SOP-011-code-review.md) | Code review process for PRs |
| [11_software_engineering_standards.md](../00_system_design/11_software_engineering_standards.md) | ISO 10007, Conventional Commits standards basis |

---

*Adapted for FORGE from industry Git workflow practices. Review every 6 months.*
