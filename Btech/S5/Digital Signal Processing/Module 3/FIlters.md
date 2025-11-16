---
id: Filters
aliases: 
tags:
  - academics
  - btech
  - s5
  - digital_signal_processing
  - filters
  - linear_phase
  - fir_filters
dg-publish: true
updated: 2025-11-14
source: "Digital Signal Processing by Proakis and Manolakis"
---

# 🔊 Linear Phase Filters

![[Pasted image 20251114113902.png]]


## 📖 What is a Linear Phase Filter?

A **linear phase filter** is a digital filter whose phase response is a straight line with frequency. In simple terms: The output is just a delayed version of the input, not a warped version. Shapes stay intact. 

Mathematically:

$$ \angle H(e^{j\omega}) = -\omega \tau $$

Where ($\tau$) is the constant group delay → all frequencies are delayed equally.

The phase response of a linear phase filter is:

$$ \phi(\omega) = -\alpha \omega $$

Where \($\alpha$) is a constant (group delay).

## 🧮 Conditions for FIR Filters to Have Linear Phase

1. [[# Symmetric Impulse Response (Even Symmetry)]] For an FIR filter with impulse response \( h[n] \) of length N (order N-1), the condition for linear phase is that the impulse response must be **symmetric** or **antisymmetric** about its center.
2. [[# Antisymmetric Impulse Response (Odd Symmetry)]]
For an FIR filter with impulse response \( h[n] \) of length N (order N-1), the condition for linear phase is that the impulse response must be **symmetric** or **antisymmetric** about its center.

>[!important]
>Both conditions **do not** need to be true simultaneously. A causal FIR has linear phase if its impulse response is either:

- Symmetric (even symmetry): h[n] = h[N−1−n] — applies to Type I & II linear‑phase FIRs.
- Antisymmetric (odd symmetry): h[n] = −h[N−1−n] — applies to Type III & IV linear‑phase FIRs.

Notes:
- The two are mutually exclusive except for the trivial all‑zero filter.
- For odd N (odd length), antisymmetry forces the center coefficient to be zero.
- Choice (symmetric vs antisymmetric) determines allowable behavior at ω=0 and ω=π and which filter types (I–IV) are possible.

Examples:
- Symmetric: h = [0.5, 1.0, 0.5] → linear phase (group delay (N−1)/2 = 1).
- Antisymmetric: h = [1, 0, −1] → linear phase (center = 0).


### 1. Symmetric Impulse Response (Even Symmetry)

For a causal FIR filter of length N:

$$ h[n] = h[N-1 - n] \quad \text{for } n = 0, 1, \dots, N-1 $$

This applies to **Type I & II** linear phase FIR filters.

- **Phase Response**: Linear with zero phase at ω=0 (low-pass) or ω=π (high-pass).
- **Group Delay**: Constant, equal to (N-1)/2 samples.

### 2. Antisymmetric Impulse Response (Odd Symmetry)

$$ h[n] = -h[N-1 - n] \quad \text{for } n = 0, 1, \dots, N-1 $$

This applies to **Type III & IV** linear phase FIR filters.

- **Phase Response**: Linear with phase shift of π/2 or -π/2.
- **Group Delay**: Constant, equal to (N-1)/2 samples.
- **Used for**: Hilbert transformers, differentiators.

### Types of Linear Phase FIR Filters

| Type | Symmetry | Phase at ω=0 | Applications                       |
| ---- | -------- | ------------ | ---------------------------------- |
| 1    | Even     | 0            | Low-pass, high-pass, band-pass     |
| 2    | Even     | π            | Band-stop, high-pass (alternative) |
| 3    | Odd      | π/2          | Hilbert transformers               |
| 4    | Odd      | -π/2         | Differentiators                    |

### Mathematical Derivation

The frequency response of an FIR filter is:

$$ H(e^{j\omega}) = \sum_{n=0}^{N-1} h[n] e^{-j\omega n} $$

For linear phase, the phase must be linear. Substituting the symmetry condition leads to the phase being proportional to ω.

For even symmetry:

$$ H(e^{j\omega}) = e^{-j\omega (N-1)/2} \sum_{n=0}^{(N-1)/2} a[n] \cos(\omega (n - (N-1)/2)) $$

Where a[n] are the coefficients.

The phase is: \( \phi(\omega) = -\omega (N-1)/2 \)

Thus, group delay = (N-1)/2.

## 📊 Example

Consider a 3-tap FIR filter (N=3): h = [0.5, 1, 0.5]

Check symmetry: h[0] = h[2] = 0.5, h[1] = 1 → Symmetric!

This is a linear phase filter with group delay of 1 sample.

## 💻 Python Example: Checking Linear Phase

```python
import numpy as np
import matplotlib.pyplot as plt

# Example FIR filter coefficients (symmetric)
h = np.array([0.5, 1.0, 0.5])

# Check symmetry
N = len(h)
is_symmetric = all(h[n] == h[N-1-n] for n in range(N//2))
print(f"Is symmetric: {is_symmetric}")

# Frequency response
w, H = plt.freqz(h, 1, worN=512)
phase = np.angle(H)

# Plot phase
plt.plot(w, phase)
plt.title('Phase Response')
plt.xlabel('Frequency (rad/sample)')
plt.ylabel('Phase (rad)')
plt.grid(True)
plt.show()

# Group delay should be constant
group_delay = -np.diff(phase) / np.diff(w)
plt.plot(w[:-1], group_delay)
plt.title('Group Delay')
plt.xlabel('Frequency (rad/sample)')
plt.ylabel('Group Delay (samples)')
plt.grid(True)
plt.show()
```

## 🎯 Applications

- **Audio Equalizers**: Preserve transients and attack in music.
- **Image Processing**: Avoid ringing artifacts in filtering.
- **Communications**: Maintain signal integrity in modems.
- **Biomedical**: ECG filtering without distorting waveforms.

## 📚 Key Points for Exams

- **Definition**: Phase ∝ -ω (constant group delay).
- **FIR Condition**: Symmetric or antisymmetric impulse response.
- **Group Delay**: (N-1)/2 for causal FIR.
- **IIR Filters**: Cannot have exact linear phase (only approximate).

> [!tip] Remember
> Linear phase = constant group delay = symmetric FIR coefficients.

> [!flashcard] What is the group delay of a linear phase FIR filter of length N?
> (N-1)/2 samples

> [!question] Is the filter h = [1, -1, 1] linear phase? Why?
> No, because h[0] ≠ h[2] (not symmetric).

> [!resources] Further Reading
> - Proakis & Manolakis, Chapter 7
> - Oppenheim & Schafer, Discrete-Time Signal Processing
> - MATLAB: fir1, firpm functions for linear phase design