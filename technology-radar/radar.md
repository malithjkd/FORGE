# Technology Radar

> **Last Updated:** [YYYY-MM-DD]  
> **Next Review:** [YYYY-MM-DD] (quarterly)

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

| Technique | Ring | Notes | Related Docs |
|---|---|---|---|
| FFT (Fast Fourier Transform) | Assess | Standard first-pass frequency analysis | — |
| Wavelet Transform | Assess | Better temporal resolution than FFT for non-stationary signals | — |
| SVD (Singular Value Decomposition) | Assess | For feature extraction from multi-sensor data | — |
| STFT (Short-Time Fourier Transform) | Assess | Time-frequency representation | — |

## ML / Classification Methods

| Technique | Ring | Notes | Related Docs |
|---|---|---|---|
| k-NN | Assess | Simple baseline classifier | — |
| 1D-CNN | Assess | Promising for time-series fault classification | — |
| Autoencoder | Assess | For anomaly detection (deviation from healthy baseline) | — |
| SVM | Assess | Classical approach, good for smaller datasets | — |

## Prognostics (RUL Estimation)

| Technique | Ring | Notes | Related Docs |
|---|---|---|---|
| Effects-based models (Type III RUL) | Assess | Track degradation from initial fault to failure threshold | — |

## Tools & Platforms

| Tool | Ring | Notes | Related Docs |
|---|---|---|---|
| ACS DPM Functions | Assess | Built-in diagnostics on the motion controller | — |
| Python + SciPy | Adopt | Core data processing stack | — |
| DVC | Assess | Data version control for large datasets | — |
| Zotero | Assess | Reference management for academic papers | — |

---

## Change Log

| Date | Change | Rationale |
|---|---|---|
| *Initial* | All techniques set to Assess | Radar created; no experiments completed yet |

---

*Update this file after each quarterly Radar Review (SOP-003) or when an experiment produces a conclusive result about a technique.*
