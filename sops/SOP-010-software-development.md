# SOP-010: Software Development

> **Source:** Adapted from DEV-001 (Software Development SOP)  
> **Scope:** All code in FORGE project repositories  
> **Owner:** Software Team Lead  
> **Standards Basis:** ISO/IEC/IEEE 12207:2017 (§6.4.5 Implementation), ISO/IEC 25010:2023 (Maintainability)

---

## 1. Purpose

This SOP defines how the software development team writes, reviews, tests, and ships code across all FORGE project types. It establishes a shared standard that all team members follow regardless of project, role, or location.

---

## 2. Scope

**Applies to:**
- All new software development (AI/ML, web applications, automation, internal tools)
- All legacy system modifications and maintenance
- All team members: leads, developers, QA engineers, research students, and interns
- All code hosted in the project GitHub organisation

**Does not cover:**
- Data collection procedures (see SOP-013)
- Model training and evaluation (see SOP-013)
- Client communication (see SOP-008)

---

## 3. Roles and Responsibilities

| Role | Development Responsibility |
|------|---------------------------|
| **Technical Lead** | Defines technical direction, reviews architecture decisions, approves major design changes, final approver for production deployments |
| **Team Lead** | Owns day-to-day code quality, conducts code reviews, ensures SOP compliance, runs sprint ceremonies |
| **Developer** | Implements features, writes unit tests, maintains code documentation |
| **QA + DevOps** | Writes and maintains automated tests, manages CI/CD pipelines, owns the test environment |
| **Research Students** | Develop algorithms and models in assigned research branches; code must meet the same standards before merging to main |
| **Intern** | Completes supervised tasks in clearly scoped branches; all code requires Team Lead sign-off before merge |

---

## 4. Distributed Team Working Agreements

For teams spanning multiple timezones:

### 4.1 Overlap Window
Identify and enforce a guaranteed daily overlap window. Schedule all real-time meetings and pair programming sessions within this window.

### 4.2 Async-First Communication
Outside the overlap window, all communication about code must be async-first:
- Use GitHub PR comments and Issues for code-specific discussion — never email or chat for code decisions
- All decisions made in chat must be summarised in the relevant GitHub Issue or PR within the same working day
- Do not block progress waiting for a reply — raise a flag in the PR and continue on another task

### 4.3 Daily Written Update
Every remote team member posts a brief written update at end of day:

```
[Date] [Name]
Done: [what was completed]
Next: [what I will work on tomorrow]
Blocked: [anything blocking me — or "none"]
```

---

## 5. Repository Structure

### 5.1 GitHub Organisation
All code lives in the project GitHub organisation. Each project has its own repository. Naming convention:

```
[org]-[project-name]-[type]

Examples:
  org-predictive-maintenance-ml
  org-field-agent-app
  org-internal-tooling-utils
```

### 5.2 Repository Contents

Every repository must have:

```
repo-root/
├── README.md              ← Project overview, setup instructions, usage
├── CONTRIBUTING.md        ← How to contribute (link to this SOP)
├── .gitignore             ← Language-appropriate ignore file
├── requirements.txt       ← (Python) or package.json (Node) or equivalent
├── src/                   ← All source code
├── tests/                 ← All test files (mirrors src/ structure)
├── docs/                  ← Technical documentation
├── scripts/               ← Build, deployment, utility scripts
└── .github/
    ├── PULL_REQUEST_TEMPLATE.md
    └── workflows/         ← CI/CD GitHub Actions workflows
```

For ML/AI repositories, also include:
```
├── notebooks/             ← Jupyter notebooks (exploration only, not production)
├── models/                ← Model configs and metadata (not weights — use DVC or S3)
├── data/                  ← Data schemas and sample data only (never raw datasets)
└── experiments/           ← Experiment configs and result logs
```

---

## 6. Development Workflow

### 6.1 Standard Feature Development Flow

```
1. Pick up story from sprint board (move to "In Progress")
2. Create branch from develop: git checkout -b feature/TICKET-NNN-description
3. Develop the feature in small, frequent commits
4. Write or update tests as you go (not at the end)
5. Run tests locally and confirm they pass
6. Push branch and open a Pull Request against develop
7. Fill in the PR template completely
8. Assign reviewer (Team Lead, or Technical Lead for architecture changes)
9. Respond to review comments; update the PR
10. Once approved: reviewer merges the PR
11. Delete the feature branch
12. Update the sprint board (move story to "In Review" then "Done")
```

### 6.2 Code Review Expectations

**For the reviewer:**
- Review within **1 business day** of PR assignment
- Check logic correctness, not just style (linting handles style)
- Leave constructive comments with suggested fixes
- Approve only when you would be comfortable owning the code yourself
- If a PR is too large to review in one sitting, ask the author to split it

**For the author:**
- PRs must not exceed **400 lines changed** (excluding tests and auto-generated code)
- Respond to all review comments before re-requesting review
- Do not merge your own PR — always wait for reviewer approval

### 6.3 Hotfix Process

```
1. Technical Lead is notified and approves a hotfix
2. Create hotfix/* branch directly from main
3. Apply the minimal fix (no refactoring, no feature additions)
4. Emergency review by Team Lead and/or Technical Lead
5. Merge to main AND develop
6. Tag the release
7. Post an incident report within 24 hours
```

---

## 7. Code Quality Standards

### 7.1 Language-Specific Standards

**Python (primary language for AI/ML):**
- Formatter: `black` (line length 88)
- Linter: `ruff` or `flake8`
- Type hints: required for all function signatures
- Docstrings: required for all public functions and classes (Google style)

**JavaScript / TypeScript (for UI/web components):**
- Formatter: `prettier`
- Linter: `eslint`
- TypeScript preferred over plain JavaScript for all new code
- No `any` type without an accompanying comment explaining why

### 7.2 Forbidden Practices

The following will block a PR from being merged:

- Hardcoded credentials, passwords, API keys, or secrets in any file
- Commented-out code blocks (use `git stash` or a separate branch instead)
- `TODO` comments without an associated GitHub Issue number
- `print()` / `console.log()` debugging statements left in production code
- Functions exceeding 50 lines (split into smaller functions)
- Files exceeding 500 lines (split into modules)

### 7.3 Secrets Management

**Secrets must never enter the repository.** This is an absolute rule.

- Use environment variables for all credentials
- Use `.env` files locally (`.env` must be in `.gitignore`)
- Use GitHub Secrets for CI/CD pipelines
- Use a secrets manager (AWS Secrets Manager, HashiCorp Vault) for production
- If a secret is accidentally committed, treat it as compromised immediately and rotate it

---

## 8. Testing Requirements

| Type | What it Tests | Tool | Required? | Minimum Coverage |
|------|--------------|------|-----------|--------------------|
| Unit | Individual functions and classes | pytest (Python), Jest (JS) | Yes | 80% line coverage |
| Integration | Interaction between modules | pytest + fixtures | Yes for APIs | Key paths covered |
| System / E2E | Full user workflow | Playwright, pytest | Yes for client features | Happy path + 2 edge cases |
| Performance | Response time, throughput | locust, k6 | For high-traffic endpoints | Meet agreed SLA |

### ML-Specific Testing Requirements

- **Determinism test**: Set random seeds and verify output is reproducible across runs
- **Data shape test**: Test that model accepts and rejects inputs of correct/incorrect shapes
- **Regression test**: After any model change, compare inference output against a saved baseline
- **Edge case test**: Test with empty input, single sample, maximum expected input size

---

## 9. Definition of Done

A story is **Done** when ALL of the following are true:

- [ ] All tasks completed and code merged via PR
- [ ] All CI/CD checks pass
- [ ] Unit tests written and passing (coverage maintained ≥80%)
- [ ] Code reviewed and approved by at least one team member
- [ ] No known bugs or regressions introduced
- [ ] Acceptance criteria verified
- [ ] Feature tested on staging environment
- [ ] Documentation updated if public API changed

### Additional for AI/ML Features

- [ ] Experiment logged with: dataset version, hyperparameters, evaluation metrics
- [ ] Model performance compared against baseline and documented
- [ ] Inference code is separate from training code
- [ ] Model artefacts stored correctly (not in Git repository)

---

## 10. CI/CD Pipeline Requirements

### Minimum Required Pipeline Stages

```
On every push to any branch:
  1. Lint check (ruff / eslint)
  2. Format check (black / prettier)
  3. Unit tests
  4. Code coverage report (fail if coverage drops below threshold)

On PR to develop:
  All of the above, plus:
  5. Integration tests
  6. Security scan (e.g., bandit for Python, npm audit for Node)
  7. Build artefact (confirm the project builds successfully)

On merge to main:
  All of the above, plus:
  8. Deploy to staging environment
  9. Smoke tests on staging
  10. Notify team on success/failure
```

---

## Cross-References

| Document | Relationship |
|----------|-------------|
| [SOP-011](./SOP-011-code-review.md) | Detailed code review process |
| [SOP-012](./SOP-012-git-workflow.md) | Git workflow, branching, and commits |
| [SOP-013](./SOP-013-ml-model-development.md) | ML-specific development lifecycle |
| [SOP-014](./SOP-014-coding-standards.md) | Language-specific coding conventions |
| [SOP-015](./SOP-015-architecture-design.md) | Architecture documentation standards |
| [11_software_engineering_standards.md](../00_system_design/11_software_engineering_standards.md) | Standards traceability |

---

*Adapted for FORGE from industry software development practices. Review every 6 months or when team structure changes significantly.*
