# EXP-005 Proposal: 1D-CNN Fault Classification

**Proposed By:** MJ  
**Date Proposed:** 2026-05-07  
**Assigned To:** [Student 2 / TBD]  
**Estimated Duration:** 6 weeks  
**Track:** ML Diagnosis  
**Status:** Proposed

## Hypothesis

We believe that a 1D Convolutional Neural Network (1D-CNN) trained on raw or minimally-processed vibration time-series data will achieve **higher fault classification accuracy than traditional feature-based methods** (FFT + k-NN/SVM from EXP-004), because CNNs can learn hierarchical features automatically and have shown strong results in vibration-based fault diagnosis literature.

## Background

This experiment is the first deep learning approach in FORGE. It tests whether end-to-end learning on raw vibration signals outperforms manually-engineered FFT features. If successful, this becomes the primary fault classification approach; if not, it provides valuable evidence for the Architecture Decision Record on model selection.

Depends on: EXP-002, EXP-003 (labelled data), EXP-004 (baseline performance to beat)

References:
- Technology Radar: 1D-CNN currently at "Assess"
- Zotero library: [assign relevant papers on 1D-CNN for fault classification]

## Method

1. Prepare dataset: split labelled vibration data into train/validation/test sets (70/15/15)
2. Preprocess: normalisation, windowing, augmentation (if dataset is small)
3. Design 1D-CNN architecture (start simple: 2–3 conv layers + dense head)
4. Train with cross-validation
5. Evaluate: accuracy, precision, recall, confusion matrix per fault type
6. Compare against EXP-004 baseline performance
7. If performance is superior, run transferability test (data from a different gantry setup if available)

## Success Criteria

- Classification accuracy > EXP-004 baseline by at least 5 percentage points
- Confusion matrix shows acceptable performance across all fault types (no single fault type below 60% recall)
- Model trains in reasonable time (< 2 hours per fold on available hardware)

## Failure Criteria & Exit Conditions

- If accuracy ≤ EXP-004 baseline: the added complexity of deep learning is not justified → create ADR recommending simpler methods
- If model overfits severely (train acc > 95%, test acc < 60%): dataset is too small → create DE entry with "dataset size" as the condition that might change this
- If training takes > 24 hours: hardware is insufficient → escalate compute requirements

## Resources Required

- Lab access: None (using existing datasets)
- Compute: GPU access recommended (Google Colab free tier or PBA workstation)
- Data: Labelled datasets from EXP-002/EXP-003
- Supervisor review: Checkpoints at architecture design and after first training run

## Risk & Mitigation

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Insufficient training data for deep learning | High | High | Data augmentation; consider transfer learning from public datasets |
| Hyperparameter tuning takes too long | Medium | Medium | Use systematic search (Optuna/Ray Tune) with early stopping |
| Overfitting | High | Medium | Dropout, regularisation, cross-validation, early stopping |
| Results not transferable across setups | Medium | High | Plan T-Test (Transferability Test) as follow-on experiment |
