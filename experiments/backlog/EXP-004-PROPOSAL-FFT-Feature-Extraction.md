# EXP-004 Proposal: FFT Feature Extraction from Vibration Data

**Proposed By:** MJ  
**Date Proposed:** 2026-05-07  
**Assigned To:** [Student 2 / TBD]  
**Estimated Duration:** 3 weeks  
**Track:** ML Diagnosis  
**Status:** Proposed

## Hypothesis

We believe that applying FFT (Fast Fourier Transform) to vibration sensor data will extract **frequency-domain features that differentiate between healthy and faulty gantry operation**, because vibration-based fault detection literature consistently shows that mechanical faults produce characteristic frequency patterns.

## Background

FFT is the standard first-pass technique for vibration analysis. This experiment applies it to FORGE's labelled datasets to determine whether frequency-domain features are sufficient for basic fault classification, or whether more advanced techniques (wavelet, STFT) are needed.

Depends on: EXP-002 (labelled data) and EXP-003 (data quality)

References:
- Technology Radar: FFT currently at "Assess"
- Zotero library: [assign relevant papers]

## Method

1. Load labelled vibration data from DVC (healthy + fault conditions)
2. Apply FFT to each recording (window size TBD based on signal length)
3. Extract features: dominant frequencies, spectral energy distribution, peak amplitude ratios
4. Visualise: compare frequency spectra for healthy vs. each fault type
5. Apply basic statistical tests (t-test, KS test) to determine if features are statistically distinct
6. If features are distinct, evaluate basic classifiers (k-NN, SVM) as a baseline

## Success Criteria

- At least 2 fault types show statistically significant (p < 0.05) frequency-domain differences vs. healthy baseline
- Feature extraction pipeline runs end-to-end and is reproducible
- If classifier applied: baseline accuracy > 70% on held-out test set

## Failure Criteria & Exit Conditions

- If no frequency-domain differences are found: record as DE entry, consider time-frequency methods (wavelet, STFT) as alternatives
- If data quality is insufficient: defer to EXP-003 for improved collection

## Resources Required

- Lab access: None (data already collected)
- Compute: Moderate (Python, NumPy, SciPy, matplotlib)
- Data: Existing labelled datasets from EXP-002/EXP-003
- Supervisor review: Checkpoint after feature visualization (before classifier)

## Risk & Mitigation

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| FFT insufficient for non-stationary signals | Medium | Medium | Plan wavelet/STFT as fallback (EXP-005) |
| Sampling rate too low for relevant frequencies | Low | High | Verify Nyquist criterion against expected fault frequencies |
| Overfitting on small dataset | Medium | Medium | Use leave-one-out or k-fold cross-validation |
