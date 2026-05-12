# Technology Radar

> **Last Updated:** 2026-05-12  
> **Next Review:** 2026-08-12 (quarterly)

This radar maps the current assessment of techniques, tools, and methods relevant to this project. Updated quarterly per SOP-003, or after any experiment that produces a clear verdict.

---

## How to Read the Radar

| Ring | Meaning |
|---|---|
| **Adopt** | Validated and recommended for use. The default choice. |
| **Trial** | Promising early results. Actively experimenting. |
| **Assess** | Worth investigating. No hands-on experience yet. |
| **Hold** | Tried and paused, or superseded by a better approach. |

---

## Signal Processing Techniques

| Technique | Ring | ISO 13374 Layer | Notes | Related Docs |
|---|---|---|---|---|
| FFT (Fast Fourier Transform) | Assess | Layer 2–3 | Standard first-pass frequency analysis | — |
| Wavelet Transform | Assess | Layer 2–3 | Better temporal resolution than FFT for non-stationary signals | — |
| SVD (Singular Value Decomposition) | Assess | Layer 3 | For feature extraction from multi-sensor data | — |
| STFT (Short-Time Fourier Transform) | Assess | Layer 2 | Time-frequency representation | — |
| RMS / Kurtosis / Crest Factor | Assess | Layer 2 | Time-domain statistical features | [TN-001](../knowledge-commons/technique-notes/TN-001-ISO-Feature-Extraction.md) |
| Envelope Analysis | Assess | Layer 3 | Bearing fault harmonics via Hilbert transform | — |

## ML / Classification Methods

| Technique | Ring | ISO 13374 Layer | Notes | Related Docs |
|---|---|---|---|---|
| k-NN | Assess | Layer 4 | Simple baseline classifier | — |
| 1D-CNN | Assess | Layer 4 | Promising for time-series fault classification | — |
| Autoencoder | Assess | Layer 4 | For anomaly detection (deviation from healthy baseline) | — |
| SVM | Assess | Layer 4 | Classical approach, good for smaller datasets | — |
| Random Forest | Assess | Layer 4 | Ensemble method, interpretable feature importance | — |

## Prognostics (RUL Estimation)

| Technique | Ring | ISO 13374 Layer | Notes | Related Docs |
|---|---|---|---|---|
| Effects-based models (Type III RUL) | Assess | Layer 5 | Track degradation from initial fault to failure threshold | — |
| LSTM for time-series | Assess | Layer 5 | Sequential degradation modelling | — |
| Degradation trend fitting | Assess | Layer 5 | Curve fitting for health indicator trends | — |

## Tools & Platforms

| Tool | Ring | Notes | Related Docs |
|---|---|---|---|
| ACS DPM Functions | Assess | Built-in diagnostics on the motion controller | — |
| Python + SciPy | Adopt | Core data processing stack | — |
| DVC | Adopt | Data version control for large datasets | [SOP-007](../sops/SOP-007-FAIR-data-compliance.md) |
| Mendeley | Adopt | Reference management for academic papers | — |
| GitHub Projects | Adopt | Task tracking and portfolio management | — |
| MLflow | Assess | Experiment tracking and model registry | — |
| Zenodo | Assess | FAIR-compliant data archival with DOI | [SOP-007](../sops/SOP-007-FAIR-data-compliance.md) |

---

## Change Log

| Date | Change | Rationale |
|---|---|---|
| *2026-05-12* | Added ISO 13374 layer column, expanded techniques, added tools | Standards integration (Module 5) |
| *Initial* | All techniques set to Assess | Radar created; no experiments completed yet |

---

*Update this file after each quarterly Radar Review (SOP-003) or when an experiment produces a conclusive result about a technique.*
