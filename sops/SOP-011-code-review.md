# SOP-011: Code Review

> **Source:** Adapted from DEV-002 (Code Review SOP)  
> **Scope:** All Pull Requests in all FORGE project repositories  
> **Owner:** Team Lead  
> **Standards Basis:** ISO/IEC 25010:2023 (Quality Model), Clean Code (Robert C. Martin), Conventional Comments

---

## 1. Purpose

This SOP defines how code reviews are conducted — what to look for, how to write feedback, how fast to respond, and what the review must accomplish before code merges.

A code review is a shared responsibility: the author writes code worth reviewing, and the reviewer gives feedback worth acting on.

---

## 2. Principles

**Code review, in order of importance:**

1. **Catch correctness errors** — logic bugs, edge cases, incorrect assumptions
2. **Share knowledge** — every review is a teaching moment
3. **Maintain consistency** — the codebase should look like it was written by one person
4. **Improve design** — catch structural problems before they become permanent
5. **Find style issues** — lowest priority; automated linting handles most of this

---

## 3. Review SLA

| PR Type | Reviewer | SLA |
|---------|----------|-----|
| Standard feature / fix | Team Lead | Within 1 business day |
| Draft PR (design feedback) | Team Lead | Within 2 business days |
| Hotfix / incident | Team Lead + Technical Lead | Within 2 hours |
| Research PR (student) | Team Lead | Within 2 business days |

**If the SLA cannot be met:** The reviewer must leave a comment stating when they will complete the review. Silence is not acceptable.

---

## 4. PR Size Limits

| PR Size | Lines Changed | Status |
|---------|-------------|--------|
| Ideal | < 200 lines | Easy to review in under 30 minutes |
| Acceptable | 200–400 lines | Requires focused review; split if possible |
| Too large | 400–800 lines | Must be split before review |
| Rejected | > 800 lines | Return immediately; not reviewable |

**How to split a large PR:**
- Separate refactoring from feature work
- Separate data layer from presentation layer
- Separate tests from implementation if test setup is complex
- Separate infrastructure changes from logic changes

---

## 5. Conventional Comments

All review comments must use the **Conventional Comments** format:

| Label | Meaning | Blocks Merge? |
|-------|---------|---------------|
| `**praise:**` | Something done well | No |
| `**nit:**` | Tiny style preference | No |
| `**suggestion:**` | Improvement, optional | No |
| `**issue:**` | Correctness or design problem | **Yes** |
| `**question:**` | Reviewer needs clarification | **Yes** |
| `**thought:**` | Future idea, no action now | No |
| `**todo:**` | Must fix, can be follow-up issue | **Yes** (create issue) |
| `**blocked:**` | PR cannot proceed | **Yes** |

### Examples

**Correctness issue (must fix):**
```
**issue:** This will raise a `KeyError` if the sensor dictionary does not
contain `'temperature'`. In production, a missing sensor key is a realistic
failure mode. Suggest using `.get('temperature')` with a fallback, and
logging a warning when the key is absent.
```

**Minor style preference:**
```
**nit:** `ambient_temperature_reading_from_sensor` is descriptive but
quite long. `ambient_temp` carries the same meaning with less noise.
Up to you.
```

**Praising good work:**
```
**praise:** Clean separation between the sensor interface and the
calibration logic. This will make it easy to mock the sensor in tests.
```

---

## 6. Clean Code Review Checklist

### Tier 1 — Always Check (Blocks Merge)

**Correctness:**
- [ ] Does the code do what the acceptance criteria describe?
- [ ] Are all error paths handled?
- [ ] Are there off-by-one errors?
- [ ] Does the code handle boundary values (zero, empty, maximum)?

**Security:**
- [ ] No hardcoded credentials, API keys, or secrets
- [ ] No unsanitised user input passed to database, shell, or file path
- [ ] No sensitive data being logged

**Tests:**
- [ ] Is there a test for the new behaviour?
- [ ] Do tests actually test logic, not just invocation?
- [ ] Are failure cases tested?
- [ ] Are tests independent?

### Tier 2 — Check for PRs > 50 Lines (Blocks Merge)

**Naming:**
- [ ] Variable names express intent
- [ ] Function names describe what they return or do
- [ ] Boolean variables phrased as questions (`is_calibrated`, `has_data`)

**Functions:**
- [ ] Functions under 50 lines
- [ ] Functions take fewer than 4 parameters
- [ ] Single responsibility (no "and" in description)

**Comments:**
- [ ] No comments describing "what" — code should do that
- [ ] Constants explained with their origin
- [ ] No commented-out code

### Tier 3 — Architecture PRs and Refactors

- [ ] Single Responsibility Principle observed
- [ ] DRY — no duplicated logic
- [ ] YAGNI — no speculative code
- [ ] Dependency direction correct (depend on abstractions)

---

## 7. Language-Specific Review Additions

### Python
- [ ] Type hints on all function signatures
- [ ] f-strings for formatting (not `%` or `.format()`)
- [ ] Context managers for file/resource handling
- [ ] No mutable default arguments
- [ ] `pathlib.Path` for file paths
- [ ] Specific exceptions (not bare `except:`)

### AI/ML Code
- [ ] Random seeds set and logged
- [ ] No data leakage (preprocessing fitted on train only)
- [ ] Tensor/array shapes checked at module boundaries
- [ ] Inference code separate from training code
- [ ] Metrics logged to experiment tracker
- [ ] No hardcoded paths to local machines

---

## 8. Approval Decision

| Decision | When to Use |
|----------|-------------|
| **Approve** | All `issue` and `question` comments resolved |
| **Approve with nits** | All blocking issues resolved; minor suggestions remain |
| **Request changes** | One or more `issue` or `question` comments unresolved |

**The Google Standard:** Code does not need to be perfect to merge. It needs to be **good enough** — meaning it improves the codebase, does not introduce new problems, and meets acceptance criteria.

---

## 9. Review Anti-Patterns

| Anti-Pattern | Signal | Fix |
|---|---|---|
| **Rubber stamping** | Reviews under 5 min for 100+ line PRs | Say you're busy and give a realistic timeline |
| **Review by committee** | Multiple reviewers, no primary | Assign exactly one primary reviewer |
| **Scope creep** | Requesting unrelated fixes in review | Open a new GitHub Issue instead |
| **Ghost reviews** | Comments but no formal Approve/Request Changes | Always submit formal review decision |
| **Nit-only feedback** | No acknowledgement of good work | Add at least one `praise:` per PR |

---

## Cross-References

| Document | Relationship |
|----------|-------------|
| [SOP-010](./SOP-010-software-development.md) | Development workflow and PR template |
| [SOP-014](./SOP-014-coding-standards.md) | Language-specific standards to review against |
| [11_software_engineering_standards.md](../00_system_design/11_software_engineering_standards.md) | ISO 25010 quality model mapping |

---

*Adapted for FORGE from industry code review practices. Review every 6 months.*
