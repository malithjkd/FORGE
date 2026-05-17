# TN-001: ISO 13374 Feature Extraction Reference

**Status:** Stable  
**Author:** Research Operations  
**Date:** 2026-05-12  
**Related Experiments:** —  
**Tags:** feature-extraction, ISO-13374, signal-processing, condition-monitoring

## Purpose

This technique note provides a reference catalogue of standard signal features used in condition monitoring, mapped to the ISO 13374-1 data processing chain. Use this as a starting point when designing feature extraction for any FORGE experiment targeting ISO Layers 2–4.

## Background

ISO 13374-1:2003 defines a six-layer data processing chain for condition monitoring. Feature extraction spans Layers 2 (Data Manipulation) and 3 (State Detection). Choosing the right features is critical for downstream classification (Layer 4) and prognostics (Layer 5).

For the full ISO mapping, see [09_ISO13374_mapping.md](../../00_system_design/09_ISO13374_mapping.md).

## Prerequisites

- Python 3.9+
- Libraries: `numpy`, `scipy`, `pywt`, `librosa`, `tsfresh`
- Data in HDF5 format (per FORGE standard)
- Install: `pip install numpy scipy PyWavelets librosa tsfresh`

## Feature Catalogue

### Time-Domain (ISO Layer 2)

| Feature | Formula | Python | When to Use |
|---------|---------|--------|-------------|
| **RMS** | √(Σxᵢ²/N) | `np.sqrt(np.mean(x**2))` | Overall vibration energy |
| **Peak** | max(\|x\|) | `np.max(np.abs(x))` | Maximum amplitude |
| **Peak-to-Peak** | max(x) - min(x) | `np.ptp(x)` | Signal range |
| **Crest Factor** | Peak / RMS | `np.max(np.abs(x)) / rms` | Impulsiveness |
| **Kurtosis** | 4th moment (normalised) | `scipy.stats.kurtosis(x)` | Fault spikiness |
| **Skewness** | 3rd moment (normalised) | `scipy.stats.skew(x)` | Asymmetric faults |
| **Standard Deviation** | σ | `np.std(x)` | Spread of signal |

### Frequency-Domain (ISO Layer 2–3)

| Feature | Method | Python | When to Use |
|---------|--------|--------|-------------|
| **FFT Magnitude** | Fast Fourier Transform | `np.abs(np.fft.rfft(x))` | Frequency content |
| **PSD** | Welch's method | `scipy.signal.welch(x, fs)` | Power distribution |
| **Spectral Centroid** | Weighted mean freq. | `librosa.feature.spectral_centroid(y=x, sr=fs)` | Dominant frequency shift |
| **Spectral Bandwidth** | Weighted std of freq. | `librosa.feature.spectral_bandwidth(y=x, sr=fs)` | Frequency spread |
| **Dominant Frequency** | argmax of FFT | `freqs[np.argmax(np.abs(fft))]` | Primary oscillation |

### Time-Frequency (ISO Layer 2–3)

| Feature | Method | Python | When to Use |
|---------|--------|--------|-------------|
| **STFT** | Short-Time FFT | `scipy.signal.stft(x, fs)` | Time-varying frequency |
| **Wavelet Coefficients** | DWT decomposition | `pywt.wavedec(x, 'db4', level=5)` | Multi-resolution analysis |
| **Envelope (Hilbert)** | Analytic signal | `np.abs(scipy.signal.hilbert(x))` | Bearing fault harmonics |
| **MFCC** | Mel cepstral coeffs | `librosa.feature.mfcc(y=x, sr=fs)` | Spectral shape |

## Worked Example

```python
import numpy as np
import h5py
from scipy import signal, stats

# Load a FORGE dataset
with h5py.File('data/raw/20260601_G01_W3_SpeedSweep_R01.h5', 'r') as f:
    vib_x = f['external_sensors/vibration_x'][:]
    fs = f['metadata'].attrs['sampling_rate_hz']

# Time-domain features
rms = np.sqrt(np.mean(vib_x**2))
kurtosis = stats.kurtosis(vib_x)
crest = np.max(np.abs(vib_x)) / rms

# Frequency-domain features
freqs, psd = signal.welch(vib_x, fs=fs, nperseg=1024)
dominant_freq = freqs[np.argmax(psd)]

# Print results
print(f"RMS: {rms:.4f}, Kurtosis: {kurtosis:.4f}, Crest: {crest:.4f}")
print(f"Dominant frequency: {dominant_freq:.1f} Hz")
```

## Validation

Correct feature extraction shows:
- RMS increases with wear level (higher vibration energy)
- Kurtosis spikes with impulsive faults (bearing damage)
- Dominant frequency shifts when mechanical properties change
- If RMS is near-zero, check sensor connection and calibration

## Limitations & Known Issues

- Time-domain features alone may not discriminate between wear levels 2–3 (see DE entries if applicable)
- FFT assumes stationarity — use STFT or wavelets for non-stationary signals
- Feature values are equipment-specific — do not transfer thresholds between different gantry setups without recalibration
- MFCC was designed for audio; effectiveness for vibration signals varies

## See Also

- [09_ISO13374_mapping.md](../../00_system_design/09_ISO13374_mapping.md) — Full ISO mapping
- [07_indusy_standard.md](../../00_system_design/07_indusy_standard.md), Section 4.8 — Signal analysis tools
- `tsfresh` documentation: [tsfresh.readthedocs.io](https://tsfresh.readthedocs.io/) — Automated feature extraction
