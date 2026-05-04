# Domain Glossary

> Shared vocabulary for all FORGE contributors. Update this document whenever a new domain-specific term is introduced.

---

## Project-Specific Terms

| Term | Definition |
|---|---|
| **PE (Position Error)** | The primary performance metric for the gantry system. The target specification is maintaining PE < 0.5 microns upon stopping. Deviations from this baseline indicate performance degradation. |
| **KS Test (Key Signature Test)** | A structured experiment to identify fault signatures under normal and fault conditions. The gantry is operated under both healthy and simulated-fault states while high-resolution sensor data is collected. |
| **T Test (Transferability Test)** | A validation experiment to confirm that fault signatures identified on one motor setup can reliably detect and predict failures on a different, independent setup. |
| **RUL (Remaining Useful Life)** | The estimated time or cycles remaining before a component reaches its failure threshold. |
| **DPM (Diagnostics and Preventive Maintenance)** | ACS controller built-in functions for monitoring machine health criteria (current, PE, temperature, settle time). |

## Hardware & Infrastructure

| Term | Definition |
|---|---|
| **Gantry** | A precision X/Y linear motor stage used in AOI (Automated Optical Inspection), lithography, and metrology tools. The primary testbed for this project. |
| **ACS Controller** | The SPiiPlus motion controller that manages the gantry's linear motors. Provides motion data, PE readings, and motor current. |
| **CTCOnline Accelerometer** | Vibration sensors placed at strategic locations on the gantry to capture fault-indicative vibration patterns. |
| **PT100** | Temperature sensors placed on motors and bearings. |

## Signal Processing & ML

| Term | Definition |
|---|---|
| **FFT (Fast Fourier Transform)** | A technique for converting time-domain signals to frequency-domain, enabling identification of frequency-based fault signatures. |
| **Wavelet Transform** | A time-frequency analysis technique that provides both frequency and temporal information, useful for non-stationary signals. |
| **1D-CNN (1D Convolutional Neural Network)** | A deep learning architecture for processing sequential/time-series data, used for fault classification. |
| **Autoencoder** | A neural network trained to reconstruct its input, useful for anomaly detection (deviations from healthy baseline). |
| **SPC (Statistical Process Control)** | Classical statistical methods for monitoring process stability and detecting out-of-control conditions. |

## FORGE System Terms

| Term | Definition |
|---|---|
| **Technique Note (TN)** | A reusable reference document describing how to perform a specific method or procedure. |
| **Architecture Decision Record (ADR)** | A document recording why a significant design or technical choice was made. |
| **Dead-End Registry (DE)** | A catalogue of approaches that were tried and confirmed not to work, with root cause analysis. |
| **Technology Radar** | A living map of techniques and tools organised by adoption status: Adopt, Trial, Assess, Hold. |
| **Research Track** | An independent line of investigation (e.g., "Data Collection", "ML Diagnosis", "RUL Estimation"). |
| **Knowledge Commons** | The shared body of written knowledge: TNs, ADRs, DEs, and the domain glossary. |
| **Research Coordinator** | The role responsible for maintaining FORGE system health (documentation quality, monthly reviews, onboarding). |
| **Compounding Knowledge** | The property of a knowledge system where each new piece of work builds on and amplifies prior work, rather than starting from scratch. |
| **DVC (Data Version Control)** | An open-source tool for versioning large datasets and model files alongside Git, storing actual data in a separate backend. |

---

*Add new terms as they arise. Keep definitions concise and accessible to someone joining the project for the first time.*
