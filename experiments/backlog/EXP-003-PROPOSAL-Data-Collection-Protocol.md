# EXP-003 Proposal: Vibration Data Collection & Labelling Protocol

**Proposed By:** MJ  
**Date Proposed:** 2026-05-07  
**Assigned To:** [Student 1 / TBD]  
**Estimated Duration:** 3 weeks  
**Track:** Data Collection  
**Status:** Proposed

## Hypothesis

We believe that establishing a **standardised data collection and labelling protocol** for vibration sensor data will enable reproducible, high-quality datasets that can be reused across multiple ML experiments, because ad-hoc data collection (as in the POC) leads to inconsistent data quality and undocumented collection conditions.

## Background

Before any ML model can be trained, the data must be collected under documented, repeatable conditions with proper labelling. This experiment creates the data collection SOP that all future experiments will reference.

Depends on: EXP-002 (KS Test Design defines what conditions to collect under)

## Method

1. Define data collection parameters:
   - Sampling rate per sensor type
   - Recording duration per condition
   - Number of repetitions per fault type
2. Define labelling schema:
   - Fault type tags (healthy, friction, obstruction, etc.)
   - Severity levels (mild, moderate, severe)
   - Condition metadata (speed, load, temperature, date, setup ID)
3. Create a Data Card template for each dataset
4. Run a pilot collection (1 healthy + 1 fault condition) to validate the protocol
5. Document the complete protocol as a Technique Note (TN-001)

## Success Criteria

- Protocol can be followed by someone who did not design it (tested by having another team member run it)
- Pilot dataset passes basic quality checks (no gaps, correct sampling rate, correct labels)
- Data Card is complete and the dataset is trackable via DVC

## Failure Criteria & Exit Conditions

- If sensor hardware cannot achieve required sampling rate, escalate to hardware team
- If labelling schema cannot distinguish between fault types, redesign schema based on EXP-002 findings

## Resources Required

- Lab access: 1 week (pilot data collection)
- Compute: Minimal
- Data: New collection (pilot)
- Supervisor review: Review protocol document before pilot

## Risk & Mitigation

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Protocol too complex for students to follow | Medium | Medium | Test with someone unfamiliar; simplify if needed |
| Pilot data reveals hardware issues | Low | High | Run quick sensor check before committing to full protocol |
