# Part A
-[[Part B]]
### 1.  **What are the methods of filtering long sequence? Explain.**  

• **Overlap-Add** → break x[n], FFT each block, add overlapped parts.  
• **Overlap-Save** → overlap input, discard corrupted samples.  
• **Block convolution** → using FFT for faster filtering.

- **Overlap-Save** — split long input into overlapping blocks of length N, compute N-point FFT, multiply with H(ω) (FFT of filter), inverse FFT, discard the first L−1 (corrupted) samples and keep the rest. Efficient for long inputs with long FIR filters because convolution done in frequency domain.
- **Overlap-Add** — split input into non-overlapping blocks of length L, convolve each block (via FFT) with impulse of length M, then add the overlapped tails (hence add). Also FFT-based; similar complexity to Overlap-Save but different book-keeping.
- **Segmented (block) convolution (direct time-domain block processing)** — break input into blocks and perform direct convolution per block; used when filter is short or FFT overhead isn’t justified.  
    Use FFT methods (Overlap-Save/Add) when the sequence is very long and direct convolution is O(NM) too costly; these reduce asymptotic cost to about O(N log N).
    
---
### 2.  **Give any three properties of DFT.**

• **Linearity**  
• **Circular shift ↔ phase change**  
• **Conjugate symmetry** (for real sequences)


- **Periodicity:** $X[k+N]=X[k]$ for N-point DFT.
- **Linearity:** $\text{DFT}\{a x[n]+b y[n]\} = a X[k] + b Y[k]$.
- **Circular Convolution Theorem:** Time-domain circular convolution corresponds to multiplication in DFT domain: $\text{DFT}\{x \circledast y\} = X[k] Y[k]$.  
    (Other common ones: symmetry for real sequences, Parseval's relation, time/frequency shift.)
    
---


### 3.  **Calculate the 4-point DFT of $cos(\pi n)$ 




 $x[n] = \cos(\pi n) = (-1)^n$ for $n=0,1,2,3$.  
Sequence: $x = [1, -1, 1, -1]$. 
Recognize this is a single complex exponential at $\omega = \pi$ which corresponds to DFT bin $k=2$ (since $\omega_k = 2\pi k / 4 = \pi k / 2$). So the 4-point DFT is
$$X[k] = \begin{cases} 4, & k=2 \\ 0, & k=0,1,3 \end{cases}$$

So $X = [0, 0, 4, 0]$. 

---

### 4. **Find Circular time reversal of [8,5,3,1].**

> Reverse → [1,3,5,8].


For length $N=4$, circular time-reversal $y[n] = x[(-n) \mod 4]$. Compute for $n=0..3$:
- $y[0] = x[0] = 8$
- $y[1] = x[3] = 1$
- $y[2] = x[2] = 3$
- $y[3] = x[1] = 5$  
So circular time-reversed sequence: **[8, 1, 3, 5]**.
How?.
$y[n] = x[(-n) \mod 4]$ so,
$y[0] = x[(-0) \mod 4] = x[0] = 8$
$y[1] = x[(-1) \mod 4] = x[3] = 1$
$y[2] = x[(-2) \mod 4] = x[2] = 3$
$y[3] = x[(-3) \mod 4] = x[1] = 5$  
Thus, circular time-reversed sequence: **[8, 1, 3, 5]**.

---

### 5. **Explain the design steps of IIR filter using Butterworth Approximation.**  

• ==Specify digital specs== → ==prewarp to analog== → ==find Butterworth order==.  ==Compute analog poles== → form H(s) → ==Apply bilinear transform== → H(z).

-  **Specify** ripple/attenuation specs: passband edge $\omega_p$, stopband edge $\omega_s$, passband ripple/attenuation ($A_p$), stopband attenuation ($A_s$).
- **Prewarp** digital frequencies (if designing via bilinear transform): $\Omega = \tan(\omega/2)$ (for normalized $T=1$).
    
1. **Find analog specs** (if needed) — convert digital edges to analog prototype frequencies (prewarping) or work directly in analog domain if designing analog then mapping.
2. **Order and cutoff:** compute minimum analog filter order $n$ and cutoff $\Omega_c$ from Butterworth magnitude formula using $|H(j\Omega)|^2 = \frac{1}{1 + (\Omega / \Omega_c)^{2n}}$ and spec inequalities.
3. **Place poles:** Butterworth analog prototype poles are equally spaced on a circle in left half plane: $p_k = \Omega_c e^{j(\pi/2 + (2k+1)\pi/(2n))}$, $k=0..n-1$. No zeros (all-pole).
4. **Form analog transfer function** $H_a(s)$ from poles with unity DC gain or desired gain.
5. **Transform to digital** using a mapping (usually bilinear transform $s = \frac{2}{T} \frac{1 - z^{-1}}{1 + z^{-1}}$) — take care of frequency warping.
6. **Scale and realize:** scale gain, realize in direct/cascade/DFI/DFII forms, and validate frequency response (adjust if specs not met due to warping).




### **6. Advantages of frequency sampling method**

• Easy to specify arbitrary magnitude response.  
• FFT-based → efficient.  
• Guarantees linear-phase FIR.

* * *

### **7. Cascade implementation of IIR**

• Break H(z) into **second-order sections (biquads)**.  
• Connect sections in series → improves numerical stability.

* * *

### **8. What is a linear phase FIR? Conditions?**

Linear phase → constant group delay, no phase distortion.  
Conditions:  
• h[n] must be **symmetric** or **antisymmetric**.  
• FIR length finite.

* * *

### **9. DSP processor vs general-purpose processor (any 3)**

• DSP has **MAC unit**, GPP doesn’t.  
• DSP supports **circular addressing**.  
• DSP optimized for **real-time**, GPP isn’t.

* * *

### **10. Applications of DSP processor**

• Speech/audio processing  
• Image/video processing  
• Communication systems (modems, SDR, filters)
