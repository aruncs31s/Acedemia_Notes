# Part B


# MODULE 1 — **Overlap–Save (worked example)**
- [ ] Practce. this one 📅 2025-11-15 
	

**Problem (picked):** Filter a long sequence $x[n]$ of length 7 by a short FIR $h[n]$ of length 3 using overlap–save.  
Use $x=[1,2,3,4,5,6,7]$, $h=[1,1,1]$.

### Steps (point form)

1. Let filter length $M$ and choose FFT size $N$ (common choice: power of 2, $N\ge M$).
2. Compute block useful-length $L = N-M+1$.
3. Partition $x$ into blocks of length $L$. For each block, form an $N$-length vector by **prepending** the previous $M-1$ samples (first block uses zeros).
4. Compute $X_{\text{blk}} = \text{FFT}_N(\text{block})$, $H = \text{FFT}_N(h\text{ padded to }N)$.
5. Multiply: $Y_{\text{blk}} = X_{\text{blk}}\cdot H$. IFFT $\Rightarrow$ circular convolution result.
6. **Discard first $M-1$** samples of the IFFT result; remaining $L$ samples are the block output.
7. Concatenate block outputs; append final tail (last $M-1$ linear convolution samples) if needed.
    

* * *

### Demonstration (numbers)

Take $M=3,\;N=4$ (small, power of 2) → $L=N-M+1=2$.  
Partition $x$ into blocks of length $L=2$:

* Blocks of original data: $[1,2],\;[3,4],\;[5,6],\;[7]$.
    

Form $N$-length input blocks by prepending previous $M-1=2$ samples (first block prepends zeros):

* Block0: $[0,0,1,2]$
    
* Block1: $[1,2,3,4]$
    
* Block2: $[3,4,5,6]$
    
* Block3: $[5,6,7,0]$ (pad final to length $L$)
    

Filter padded to length $N$: $h_{\text{pad}}=[1,1,1,0]$.

We can use linear convolution per block and then discard first $M-1$ samples (equivalent to FFT method for this example).

**Block0** linear conv (length $4+3-1=6$):  
$[0,0,1,2]*[1,1,1] \Rightarrow y_{\text{lin}}=[0,0,1,3,3,2]$.  
Discard first $M-1=2$ → output = $[1,3]$.

**Block1:** $[1,2,3,4]*[1,1,1] \Rightarrow [1,3,6,9,7,4]$. Discard → $[6,9]$.

**Block2:** $[3,4,5,6]*[1,1,1] \Rightarrow [3,7,12,15,11,6]$. Discard → $[12,15]$.

**Block3:** $[5,6,7,0]*[1,1,1] \Rightarrow [5,11,18,13,7,0]$. Discard → $[18,13]$.

Concatenate block outputs:  
$[1,3,6,9,12,15,18,13]$. Append tail sample from final linear convolution (last sample $=7$). Final linear-convolution output is

$$\boxed{y = [1,\,3,\,6,\,9,\,12,\,15,\,18,\,13,\,7].}$$

(Which matches direct linear convolution $y[n]=x[n]+x[n-1]+x[n-2]$.)

* * *

# MODULE 2 — **DIT (Decimation-in-Time) FFT derivation + 4-point example**

### Steps (point form)

1. Write $N$-point DFT: $X[k]=\sum_{n=0}^{N-1} x[n] W_N^{kn}$ with $W_N=e^{-j2\pi/N}$.
    
2. Split $x[n]$ into even/odd parts: $x_e[n]=x[2n]$, $x_o[n]=x[2n+1]$.
    
3. Express $X[k]=\sum x_e[n]W_{N/2}^{kn} + W_N^k\sum x_o[n]W_{N/2}^{kn}$.
    
4. Recursively compute $E[k]$ and $O[k]$ (size $N/2$ FFTs). Combine:
    

$$\boxed{X[k]=E[k]+W_N^{k}O[k],\quad X[k+N/2]=E[k]-W_N^{k}O[k].}$$

* * *

### 4-point FFT of $x=[3,4,8,1]$

**Step A — split even/odd**

* Even samples: $x_e=[x_0,x_2]=[3,8]$
    
* Odd samples: $x_o=[x_1,x_3]=[4,1]$
    

**Step B — 2-point DFTs** (2-point DFT: $X[0]=x_0+x_1,\; X[1]=x_0-x_1$)

* $$E[0]=3+8=11,\; E[1]=3-8=-5$$
    
* $$O[0]=4+1=5,\; O[1]=4-1=3$$
    

**Step C — combine with twiddle factors** ($W_4 = e^{-j\pi/2}$):

$$\begin{aligned}  
X[0] &= E[0] + W_4^0 O[0] = 11 + 1\cdot 5 = 16,\\  
X[1] &= E[1] + W_4^1 O[1] = -5 + (-j)\cdot 3 = -5 - 3j,\\  
X[2] &= E[0] - W_4^0 O[0] = 11 - 5 = 6,\\  
X[3] &= E[1] - W_4^1 O[1] = -5 - (-j)\cdot 3 = -5 + 3j.  
\end{aligned}$$

So the 4-point DFT is

$$\boxed{X = [\,16,\; -5-3j,\; 6,\; -5+3j\,].}$$

(Equivalent to earlier numeric result; some solutions scale signs of imaginary part depending on $W_N$ convention — above uses $W_N=e^{-j2\pi/N}$.)

* * *

# MODULE 4 — **Realization (Direct Form I / II) — worked**

**Problem (picked):** Realize the system

$$y[n] = -0.1\,y[n-1] + 0.2\,y[n-2] + 3\,x[n] + 3.6\,x[n-1] + 0.6\,x[n-2].$$

### Steps (point form)

1. Bring to standard LTI difference-equation form with all $y$ terms on LHS.
    
2. Take z-transform; form $H(z)=\dfrac{Y(z)}{X(z)}$.
    
3. Write numerator and denominator polynomials in $z^{-1}$.
    
4. Direct Form I: implement numerator and denominator as two cascaded parts (delay lines for both).
    
5. Direct Form II (canonical): reduce delay elements to minimum (same delays used for feedforward and feedback). Optionally factor $H(z)$ into biquads for cascade.
    

* * *

### Demonstration & equations

Move all $y$-terms to LHS:

$$y[n] + 0.1\,y[n-1] - 0.2\,y[n-2] = 3\,x[n] + 3.6\,x[n-1] + 0.6\,x[n-2].$$

Take z-transform and divide:

$$\boxed{H(z)=\frac{Y(z)}{X(z)}=\frac{3 + 3.6\,z^{-1} + 0.6\,z^{-2}}{1 + 0.1\,z^{-1} - 0.2\,z^{-2}}.}$$

**Direct Form I (DF-I):** two separate sections

* Implement denominator as an IIR feedback filter using delay line $z^{-1}$s.
    
* Implement numerator (FIR) using its own delay line.  
    DF-I uses up to 4 delay elements (2 for numerator, 2 for denominator) — visually it's numerator and denominator filters in cascade.
    

**Direct Form II (DF-II) — canonical:** combine delay lines so only $\max(\text{order num},\text{order den})=2$ delay elements are used:

State update (one convenient realization):  
Let $w[n]$ be the internal states such that

$$\begin{aligned}  
w[n] &= x[n] - 0.1\,w[n-1] + 0.2\,w[n-2]\quad\text{(intermediate)},\\  
y[n] &= 3\,w[n] + 3.6\,w[n-1] + 0.6\,w[n-2].  
\end{aligned}$$

(One can derive the exact coefficient mapping by algebraic rearrangement — the key idea: use two delay registers shared between feedforward and feedback.)

**Cascade / Parallel:**

* Factor $H(z)$ into second-order sections (biquads) for numerical stability (cascade of biquads).
    
* Or perform partial-fraction (direct form parallel) if poles are separated for easier implementation.
    

* * *

## Quick exam-tip (boxed)

$$\boxed{H(z)=\dfrac{3 + 3.6z^{-1} + 0.6z^{-2}}{1 + 0.1z^{-1} - 0.2z^{-2}}}  
\quad\text{(use this to draw DF-I or convert to DF-II).}$$

* * *

If you want, I can:

* Turn the **Overlap–Save** numeric walkthrough into an FFT-table style (show FFT/H[k], multiply, IFFT values), or
    
* Show the **exact DF-II signal-flow equations** with coefficients expanded for implementation, or
    
* Do the **butterworth design** (Module 3) worked numerically for a given passband/stopband (prewarp → analog design → bilinear transform) step-by-step and boxed formulas.
    

# Other

## Compute  DFT
#module_1
Compute DFT of $x[n] = \left( \frac{1}{2} \right)^n [\sum_{k=0}^{3} (\delta(n -k))]$


$$x[n]=\Big(\tfrac12\Big)^n\sum_{k=0}^{3}\delta[n-k],$$

i.e. $x[n]=(1/2)^n$ for $n=0,1,2,3$, and $0$ elsewhere.
# Steps (short)

1. Write the DFT definition for length $N=4$:
    
    $$X[k]=\sum_{n=0}^{3} x[n] e^{-j\frac{2\pi}{4}kn}.$$
2. Substitute $x[n]=(1/2)^n$ to get a finite geometric series in $n$.
    
3. Sum the geometric series (closed form).
    
4. Evaluate for each $k=0,1,2,3$. Box the key formulas and final answers.
    

# Derivation & numeric evaluation

Define $W_4=e^{-j\frac{2\pi}{4}}=e^{-j\pi/2}$. For all $k$:

$$\begin{aligned}  
X[k]  
&=\sum_{n=0}^{3}\Big(\tfrac12\Big)^n W_4^{kn}  
=\sum_{n=0}^{3}\big((\tfrac12)W_4^{k}\big)^n \\  
&=\frac{1-\big((\tfrac12)W_4^{k}\big)^{4}}{1-(\tfrac12)W_4^{k}}\qquad(\text{for }1-(\tfrac12)W_4^{k}\neq0).  
\end{aligned}$$ $$\boxed{\,X[k]=\dfrac{1-\big(\tfrac{1}{2}W_4^{k}\big)^{4}}{1-\tfrac{1}{2}W_4^{k}}\,}$$

Now compute each $k$ (work shown):

**$k=0$** ($W_4^0=1$, ratio $r=\tfrac12$):

$$X[0]=\sum_{n=0}^3\Big(\tfrac12\Big)^n=1+\tfrac12+\tfrac14+\tfrac18=\frac{15}{8}.$$ $$\boxed{X[0]=\dfrac{15}{8}=1.875}$$

**$k=1$** ($W_4=e^{-j\pi/2}=-j$, $r=-\tfrac{j}{2}$):

$$r=-\tfrac{j}{2},\quad r^4=\left(-\tfrac{j}{2}\right)^4=\tfrac{1}{16}.$$ $$X[1]=\frac{1-\tfrac{1}{16}}{1-(-\tfrac{j}{2})}=\frac{15/16}{1+\tfrac{j}{2}}  
=\frac{15}{16}\cdot\frac{1-\tfrac{j}{2}}{1+\tfrac{1}{4}}  
=\frac{15}{16}\cdot\frac{1-\tfrac{j}{2}}{5/4}.$$

Compute factors exactly:

$$\frac{15}{16}\cdot\frac{4}{5}=\frac{15\cdot4}{16\cdot5}=\frac{60}{80}=\frac{3}{4},  
\qquad  
\frac{15}{16}\cdot\frac{4}{5}\cdot\Big(-\tfrac{j}{2}\Big)=-\frac{3}{4}\cdot\frac{j}{2}=-\frac{3j}{8}.$$ $$\boxed{X[1]=\dfrac{3}{4}-j\dfrac{3}{8}=0.75 - j0.375}$$

**$k=2$** ($W_4^2=e^{-j\pi}=-1$, $r=-\tfrac{1}{2}$):

$$X[2]=\sum_{n=0}^3 \Big(\tfrac12\Big)^n(-1)^n  
=1-\tfrac12+\tfrac14-\tfrac18=\frac{5}{8}.$$ $$\boxed{X[2]=\dfrac{5}{8}=0.625}$$

**$k=3$** ($W_4^3=e^{-j3\pi/2}=j$, $r=\tfrac{j}{2}$): conjugate of $k=1$

$$X[3]=\frac{15/16}{1-\tfrac{j}{2}}=\overline{X[1]}=\dfrac{3}{4}+j\dfrac{3}{8}.$$ $$\boxed{X[3]=\dfrac{3}{4}+j\dfrac{3}{8}=0.75 + j0.375}$$

# Final boxed result

$$\boxed{\,X[0]=\tfrac{15}{8},\quad X[1]=\tfrac{3}{4}-j\tfrac{3}{8},\quad X[2]=\tfrac{5}{8},\quad X[3]=\tfrac{3}{4}+j\tfrac{3}{8}\,}$$
