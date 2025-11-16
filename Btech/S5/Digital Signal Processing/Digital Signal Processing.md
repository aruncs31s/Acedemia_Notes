---
id: Digital Signal Processing
aliases: []
tags:
  - academics
  - btech
  - s5
  - digital_signal_processing
Attendance: 86%
ExamDate: 2025-11-15
Internal: 27
dg-publish: true
---
# Digital Signal Processing

```widgets
type: countdown
date: 2025-11-15 09:00:00
to: EXAM
completedLabel: Exam Started
```

```tasks
not done
path includes Digital Signal Processing
```

# Module 1


| HI                                 | Hello                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ==**Discrete Fourier Transform**== | ![[Discrete Fourier Tranform#^32d1f3]]<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ==**Inverse Fourier Transform**==  | ![[Discrete Fourier Tranform#^cf415f]]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ==**Unilateral Z-transform**==     | $H(z)=\sum_{n=0}^\infty h[n] z^{-n}$.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ==Linear transformation==          | <br>$$\begin{bmatrix}  <br>X(0)\\  <br>X(1)\\  <br>X(2)\\  <br>\vdots\\  <br>X(N-1)  <br>\end{bmatrix}  <br>=  <br>\begin{bmatrix}  <br>1 & 1 & 1 & \dots & 1 \\  <br>1 & W & W^2 & \dots & W^{N-1} \\  <br>1 & W^2 & W^4 & \dots & W^{2(N-1)} \\  <br>\vdots & \vdots & \vdots & \ddots & \vdots \\  <br>1 & W^{N-1} & W^{2(N-1)} & \dots & W^{(N-1)(N-1)}  <br>\end{bmatrix}  <br>\begin{bmatrix}  <br>x(0)\\  <br>x(1)\\  <br>x(2)\\  <br>\vdots\\  <br>x(N-1)  <br>\end{bmatrix}$$<br><br>with $W = e^{(−j2π/N)}$.<br><br> |





| **Module** | **Topic** | **Exam-Focused Explanation** | **Important Equations** |
| --- | --- | --- | --- |
| **1** | **DFT Definition** | Converts N-point time signal → frequency domain | $X[k]=\sum_{n=0}^{N-1} x[n]e^{-j2\pi kn/N}$ |
|  | **IDFT** | Frequency → time domain | $x[n]=\frac{1}{N}\sum_{k=0}^{N-1}X[k]e^{j2\pi kn/N}$ |
|  | **Key DFT Properties** | Used to solve PYQs quickly | Linearity; Time shift: $e^{-j2\pi k n_0/N}$; Freq shift: circular shift; Real sequence → conjugate symmetry |
|  | **Circular Convolution** | DFT-based filtering | $y[n]=\sum x[m]h[(n-m)\_N]$ |
|  | **Linear Convolution via DFT** | Zero-pad → DFT → Multiply → IDFT | Length ≥ M+L–1 |
|  | **Overlap-Add** | Block-wise linear convolution | — |
|  | **Overlap-Save** | Discard first L–1 samples | — |
| **2** | **FFT Complexity** | Reason FFT used | Direct: $N^2$ vs FFT: $N\log_2 N$ |
|  | **DIT FFT** | Bit-reverse input → butterflies | Butterfly: $X_e \pm W_N^kX_o$ |
|  | **DIF FFT** | Butterflies first → bit-reverse output | Same butterfly |
|  | **Twiddle Factor** | Rotation factor | $W_N^k=e^{-j2\pi k/N}$ |
|  | **Two Real Sequences via One FFT** | High-speed exam trick | $c[n]=a[n]+jb[n]$ |
| **3** | **FIR Linear Phase Conditions** | FIR → linear phase only if symmetric/antisymmetric | $h[n]=\pm h[M-n]$ |
|  | **Ideal LPF for Window Method** | Base kernel before windowing | $h_d[n]=\frac{\sin(\omega_c(n-M/2))}{\pi(n-M/2)}$ |
|  | **Windows** | Used in FIR design | Hamming: $0.54-0.46\cos(...)$; Hanning: $0.5-0.5\cos(...)$ |
|  | **Butterworth LPF** | Smooth, monotonic IIR | ( |
|  | **Order Formula (VERY IMPORTANT)** | Used in all IIR PYQs | $N=\frac{\log_{10}\left(\tfrac{10^{A_s/10}-1}{10^{A_p/10}-1}\right)}{2\log_{10}(\Omega_s/\Omega_p)}$ |
|  | **Bilinear Transform** | Analog → digital IIR | $s=\frac{2}{T}\frac{1-z^{-1}}{1+z^{-1}}$ |
|  | **Frequency Pre-warping** | Removes distortion due to BLT | $\Omega=\tfrac{2}{T}\tan(\omega/2)$ |
|  | **Impulse Invariance** | Sample analog impulse response | $h[n]=h_a(nT)$ |
| **4** | **Direct Form I** | Separate x and y delay chains | — |
|  | **Direct Form II** | Minimum memory (single chain) | — |
|  | **Cascade Form** | Break H(z) into 2nd-order sections | — |
|  | **Parallel Form** | Partial fractions | — |
|  | **Decimation** | Downsample by M | $y[n]=x[nM]$ |
|  | **Decimation Frequency Relation** | Aliasing formula | $Y(e^{j\omega})=\frac{1}{M}\sum X(e^{j(\omega+2\pi k)/M})$ |
|  | **Interpolation** | Insert L–1 zeros → LPF | $Y(e^{j\omega})=X(e^{j\omega L})$ |
|  | **Anti-aliasing Filter** | Before decimator | LPF, cutoff = π/M |
|  | **Anti-imaging Filter** | After interpolator | LPF, cutoff = π/L |
| **5** | **Harvard Architecture** | Separate instruction/data → faster | — |
|  | **MAC Unit** | Fast multiply-accumulate | — |
|  | **TMS320C67xx** | VLIW, 8 units, floating-point DSP | — |
|  | **Quantization Noise Variance** | MOST repeated exam question | $\sigma_q^2=\frac{\Delta^2}{12}$ |
|  | **Coefficient Quantization** | Moves poles, may destabilize | — |
|  | **FFT Round-off Error** | Grows with size | Error ∝ $N\log N$ |

# ⭐ **FFT Complexity for N = 1024**

We use:

- Additions = Nlog⁡2NN \log_2 NNlog2​N
    
- Multiplications = N2log⁡2N\frac{N}{2} \log_2 N2N​log2​N