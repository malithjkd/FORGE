# EXP-002 Proposal: Key Signature Test (KS Test) Design

**Proposed By:** MJ  
**Date Proposed:** 2026-05-07  
**Assigned To:** [Student 1 / TBD]  
**Estimated Duration:** 4 weeks  
**Track:** Data Collection  
**Status:** Proposed

## Hypothesis

We believe that operating the gantry under controlled healthy and fault conditions while collecting high-resolution sensor data will produce **identifiable, repeatable fault signatures** in the vibration and position error signals, because prior POC work (EXP-001) showed preliminary evidence of distinguishable patterns.

## Background

The Key Signature Test is a foundational experiment for FORGE. Its purpose is to establish whether specific fault types produce unique, detectable signatures in the sensor data. Without this, no downstream ML model or RUL estimation is possible.

This experiment builds on:
- EXP-001 (POC results)
- Domain knowledge from ACS DPM functions
- Literature on vibration-based fault detection (see Zotero library)

## Method

1. **Define fault types** to be simulated (friction, obstruction, bearing degradation, misalignment)
2. **Establish healthy baseline** — run gantry under normal conditions and record all sensor channels
3. **Introduce each fault type** individually under controlled conditions
4. **Record data** from: CTCOnline accelerometers, ACS PE readings, motor current, PT100 temperature
5. **Repeat each condition** at least 3 times for statistical validity
6. **Compare** fault vs. healthy signals across time-domain and frequency-domain representations

### Variables
- **Independent:** Fault type (healthy, friction, obstruction, bearing degradation, misalignment)
- **Dependent:** Sensor signals (vibration amplitude, PE deviation, motor current, temperature)
- **Controlled:** Motion profile, speed, load, ambient temperature

## Success Criteria

- At least 2 out of 4 fault types produce visually and statistically distinguishable signatures compared to healthy baseline
- Signatures are repeatable across at least 3 trials per condition
- Data quality is sufficient for downstream feature extraction

## Failure Criteria & Exit Conditions

- If no fault type produces a distinguishable signature after all conditions are tested, this is a dead end → create DE entry
- If data quality issues prevent analysis (sensor noise, sampling rate too low), stop and address hardware setup first

## Resources Required

- Lab access: 2 weeks of gantry time (shared with production schedule)
- Compute: Minimal (data collection and basic visualization only)
- Data: New collection required — this IS the data collection
- Supervisor review: Checkpoint at end of Week 2 (healthy baseline + first fault type)

## Risk & Mitigation

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Gantry not available for testing | Medium | High | Book lab time in advance; align with production schedule |
| Simulated faults not representative of real faults | Medium | Medium | Consult with service engineers on realistic fault conditions |
| Sensor placement affects signal quality | Low | High | Document exact sensor positions; verify signal quality before full test |
| Data volume exceeds storage capacity | Low | Medium | Estimate data size per test; configure DVC before starting |
