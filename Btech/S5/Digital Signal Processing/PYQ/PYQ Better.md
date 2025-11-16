---
tags:
  - example
Status: false
---

# Parseval’s theorem 
-  [ ] Check out this.
==Parseval’s theorem equates the total energy of a signal in time-domain to the total energy in frequency-domain==.

==The total energy of a signal in the time domain is equal to its total energy in the frequency domain==

### **General (cross-correlation) form** of Parseval’s theorem for the **continuous-time Fourier transform (CTFT)**.


The continuous-time Fourier transform pair is

$$X(\omega)=\int_{-\infty}^{\infty} x(t)e^{-j\omega t}\,dt,  
\qquad  
x(t)=\frac{1}{2\pi}\int_{-\infty}^{\infty} X(\omega)e^{j\omega t}\,d\omega.$$

Parseval’s identity in its general form says:

$$\int_{-\infty}^{\infty} x_1(t)\,x_2^{*}(t)\,dt  
=  
\frac{1}{2\pi} \int_{-\infty}^{\infty} X_1(\omega)\,X_2^{*}(\omega)\,d\omega.$$


A couple of small clarifications:

1. If you choose the **other FT convention** (with $1/\sqrt{2\pi}$ on both transforms), the $1/2\pi$ disappears.  
    So the constant depends only on the FT definition, not on the theorem itself.
2. Setting $x_1 = x_2 = x$ gives the usual “energy equivalence” version:

$$\int_{-\infty}^{\infty} |x(t)|^2 dt  
=  
\frac{1}{2\pi}\int_{-\infty}^{\infty} |X(\omega)|^2 d\omega.$$
3. For periodic signals, you replace energy with **average power**, but the same idea survives:  
    time-domain power = frequency-domain power.


## 1) DFT (finite-length, discrete) — statement

Let $x[n]$, $n=0,\dots,N-1$, have $N$-point DFT

$$X[k]=\sum_{n=0}^{N-1} x[n]\,e^{-j\frac{2\pi}{N}kn},\qquad k=0,\dots,N-1.$$

Then Parseval’s identity for the DFT is

$$\sum_{n=0}^{N-1} |x[n]|^2 \;=\; \frac{1}{N}\sum_{k=0}^{N-1} |X[k]|^2.$$

### Proof (DFT)

Start with the cross-version (inner product) — for any two sequences $x[n]$ and $y[n]$ with DFTs $X[k]$ and $Y[k]$:

$$\sum_{n=0}^{N-1} x[n]\,y^*[n] \;=\; \frac{1}{N}\sum_{k=0}^{N-1} X[k]\,Y^*[k].$$

Proof of cross-version:

$$\begin{aligned}  
\frac{1}{N}\sum_{k=0}^{N-1} X[k]\,Y^*[k]  
&=\frac{1}{N}\sum_{k=0}^{N-1}\Big(\sum_{n=0}^{N-1} x[n]e^{-j\frac{2\pi}{N}kn}\Big)  
\Big(\sum_{m=0}^{N-1} y[m]e^{-j\frac{2\pi}{N}km}\Big)^*\\[6pt]  
&=\frac{1}{N}\sum_{k=0}^{N-1}\sum_{n=0}^{N-1}\sum_{m=0}^{N-1} x[n]\,y^*[m]\,e^{-j\frac{2\pi}{N}k(n-m)}.  
\end{aligned}$$

Swap sums and evaluate the inner sum over $k$. Use orthogonality of complex exponentials:

$$\sum_{k=0}^{N-1} e^{-j\frac{2\pi}{N}k(n-m)} =  
\begin{cases} N, & n\equiv m\pmod N,\\[4pt] 0, & n\not\equiv m\pmod N. \end{cases}$$

Because indices $n,m$ are both in $0,\dots,N-1$, equality modulo $N$ means $n=m$. Thus only terms with $n=m$ survive and we get

$$\frac{1}{N}\sum_{k}X[k]Y^*[k] = \sum_{n=0}^{N-1} x[n]\,y^*[n].$$

Setting $y=x$ (so $Y=X$) gives the Parseval identity for energy:

$$\sum_{n=0}^{N-1}|x[n]|^2=\frac{1}{N}\sum_{k=0}^{N-1}|X[k]|^2.$$

QED.

* * *

## 2) DTFT (discrete-time Fourier transform) — statement

For a (square-summable) discrete-time sequence $x[n]$ with DTFT

$$X(e^{j\omega})=\sum_{n=-\infty}^{\infty} x[n]\,e^{-j\omega n},$$

Parseval’s theorem (Plancherel form) is

$$\sum_{n=-\infty}^{\infty} |x[n]|^2 \;=\; \frac{1}{2\pi}\int_{-\pi}^{\pi} |X(e^{j\omega})|^2 \,d\omega.$$

### Proof sketch (DTFT)

Use the cross-version first:

$$\sum_{n=-\infty}^{\infty} x[n]\,y^*[n] \;=\; \frac{1}{2\pi}\int_{-\pi}^{\pi} X(e^{j\omega})\,Y^*(e^{j\omega})\,d\omega.$$

Proof idea: write $x[n]$ from the inverse DTFT,

$$x[n]=\frac{1}{2\pi}\int_{-\pi}^{\pi} X(e^{j\omega})\,e^{j\omega n}\,d\omega,$$

then form $\sum_n x[n]\,y^*[n]$, substitute the inverse formula for $x[n]$ and $y^*[n]$ (or substitute only for $x[n]$ and use the DTFT of $y$ for the sum over $n$). Swap sum and integral (justified by square-summability, Fubini/Tonelli conditions), use

$$\sum_{n=-\infty}^{\infty} e^{j\omega n} e^{-j\omega' n} = 2\pi\,\sum_{m\in\mathbb Z}\delta(\omega-\omega'-2\pi m)$$

and restrict to principal period $[-\pi,\pi)$ to obtain the integral identity. Setting $y=x$ yields

$$\sum_{n=-\infty}^{\infty} |x[n]|^2 = \frac{1}{2\pi}\int_{-\pi}^{\pi} |X(e^{j\omega})|^2\,d\omega.$$

This is the DTFT version of Parseval / Plancherel. (Rigorous proofs use properties of $L^2$ spaces / Fourier transform theory; the steps above give the key manipulations.)

* * *

## 3) Continuous-time FT (statement)

If $x(t)$ has Fourier transform $X(\omega)=\int_{-\infty}^{\infty} x(t)e^{-j\omega t}dt$ and $x\in L^2(\mathbb R)$, then

$$\int_{-\infty}^{\infty} |x(t)|^2\,dt \;=\; \frac{1}{2\pi}\int_{-\infty}^{\infty} |X(\omega)|^2\,d\omega.$$

Proof follows the same pattern as the DTFT proof and is a standard result in Fourier analysis (Plancherel theorem).

* * *

## Intuition / meaning (one line)

Parseval says energy is invariant under the Fourier transform: energy summed in time equals energy integrated (with normalization) in frequency. In DSP terms, ==no energy is “lost” by changing domains== — you just re-express it across frequency bins.

* * *


# Circular Convolution

- [ ] Revise this. 📅 2025-11-14 

Obtain linear convolution of the sequences $x(n) = {1,2,3}$ & $h(n) =$
${-1, -2}$ using circular convolution.

* * *

So $x[n]=\{1,2,3\}$ and $h[n]=\{-1,-2\}$.

Compute the **linear convolution** $y[n]=x[n]*h[n]$ using **circular convolution** with $N\ge 3+2-1=4$. Use $N=4$.

### Zero-pad to length 4

$x = [1,2,3,0]$  
$h = [-1,-2,0,0]$

### 4-point circular convolution (direct sum)
$$y_c[n]=\sum_{k=0}^{3} x[k]\,h[(n-k)\bmod 4]$$
Compute for $n=0..3$:
* $$y[0]=1\cdot(-1)+2\cdot0+3\cdot0+0\cdot(-2)=-1$$
* $$y[1]=1\cdot(-2)+2\cdot(-1)+3\cdot0+0\cdot0=-2-2=-4$$
* $$y[2]=1\cdot0+2\cdot(-2)+3\cdot(-1)+0\cdot0=-4-3=-7$$
* $$y[3]=1\cdot0+2\cdot0+3\cdot(-2)+0\cdot(-1)=-6$$
### Result (linear convolution)
$$y[n]=\{-1,\;-4,\;-7,\;-6\}$$
This matches the usual linear-convolution result (since $N$ was chosen ≥ output length).




## Find the number of complex multiplications involved in the calculation of a 64 point DFT 
using 
1. direct computation 
2. radix-2 FFT algorithm

* * *



Let $N=64$.

**(i) Direct DFT (naive)**  
Each output $X[k]=\sum_{n=0}^{N-1} x[n]W_N^{kn}$ needs $N$ complex multiplications and there are $N$ outputs, so the usual count is

$$\text{complex multiplications} = N^2 = 64^2 = 4096.$$

**(ii) Radix–2 FFT**  
For radix-2 decimation-in-time (or decimation-in-frequency) FFT with $N=2^m$:

* Number of stages $= \log_2 N = 6$.
    
* Each stage has $N/2 = 32$ complex twiddle multiplications (one per butterfly pair).
    

So

$$\text{complex multiplications} = \frac{N}{2}\log_2 N = 32\times 6 = 192.$$

# Derive the mapping between s and z in bilinear transformation.

# Derivation — bilinear $s \leftrightarrow z$ mapping

We want a one-to-one algebraic mapping that converts an analog Laplace variable $s$ into a digital $z$ variable so that integrators/differentiators are mapped sensibly when converting continuous-time filters to discrete-time. The bilinear transform does that using the trapezoidal (Tustin) rule for the derivative.

### 1) Trapezoidal rule → discrete derivative

The continuous-time derivative $\dfrac{d}{dt}x(t)$ approximated at sample period $T$ by the trapezoidal rule gives

$$\frac{dx}{dt}\Big|_{t=nT} \approx \frac{2}{T}\,\frac{x[n]-x[n-1]}{x[n]+x[n-1]}\quad\text{(in transfer-function form this becomes a ratio of difference and sum).}$$

More usefully, in $z$-domain the backward shift is $z^{-1}$. The discrete substitute for $s$ (i.e., for differentiation) becomes

$$s \;\longleftrightarrow\; \frac{2}{T}\,\frac{1-z^{-1}}{1+z^{-1}}.$$

Multiply numerator/denominator by $z$ to obtain the commonly used equivalent form:

$$\boxed{\,s = \frac{2}{T}\,\frac{z-1}{z+1}\,}$$

That is the bilinear transform mapping from $z$ to $s$.

### 2) Inverse mapping

Solve for $z$ in terms of $s$:

$$s = \frac{2}{T}\frac{z-1}{z+1}  
\quad\Rightarrow\quad  
s\,(z+1)=\frac{2}{T}(z-1)$$ $$s z + s = \frac{2}{T} z - \frac{2}{T}  
\quad\Rightarrow\quad  
z\left(s-\frac{2}{T}\right) = -s - \frac{2}{T}$$ $$\boxed{\,z = \frac{1 + \tfrac{sT}{2}}{1 - \tfrac{sT}{2}}\,}$$

### 3) Frequency mapping (warping)

For purely imaginary $s=j\Omega$ and $z=e^{j\omega}$,

$$j\Omega = \frac{2}{T}\frac{1-e^{-j\omega}}{1+e^{-j\omega}}.$$

Simplify the RHS (use Euler algebra or write in terms of sines/cosines); this yields

$$j\Omega = j\frac{2}{T}\tan\!\frac{\omega}{2}  
\quad\Rightarrow\quad  
\boxed{\,\Omega = \frac{2}{T}\tan\!\frac{\omega}{2}\,}$$

or equivalently

$$\omega = 2\arctan\!\left(\frac{\Omega T}{2}\right).$$

This is the standard frequency-warping relation: digital frequency $\omega$ (rad/sample) is mapped to analog frequency $\Omega$ (rad/sec) via the tangent.

### 4) Important properties / practical notes

* The transform is **one-to-one** and maps the entire left-half $s$-plane to the **interior of the unit circle** (so stable analog filters map to stable digital filters).
    
* The imaginary $s$-axis (analog frequency axis) maps onto the unit circle $|z|=1$.
    
* There is **no aliasing** (unlike simple sampling); instead we get **frequency warping** (the tan/atan relation above). To design IIR digital filters that match analog specifications, apply **pre-warping**: pick analog cutoff $\Omega_c$ satisfying $\omega_c = 2\arctan(\Omega_c T/2)$ (or invert that formula) before mapping.
    
* In digital design use the substitution
    
    $$H_d(z) = H_a\!\Big(s=\tfrac{2}{T}\frac{z-1}{z+1}\Big)$$
    
    then simplify and usually factor to get a causal, stable digital IIR.
    

### Quick summary (cheat-sheet)

$$\boxed{\,s=\dfrac{2}{T}\dfrac{z-1}{z+1}\quad\Longleftrightarrow\quad z=\dfrac{1+\tfrac{sT}{2}}{1-\tfrac{sT}{2}}\,}  
\qquad\text{and}\qquad  
\boxed{\,\Omega=\dfrac{2}{T}\tan\!\dfrac{\omega}{2}\,}$$

There — a compact derivation and the key formulas. If you want, I can show a worked example: map a Butterworth low-pass prototype with cutoff $\Omega_c$ into the digital domain using pre-warping and the bilinear transform.





# Given the specification ==pass band affenuation is I dB== , ==stop band attenuation is 30 dB==, pass band edge frequency 200 rad/sec and stop band edge frequency $600 rad/sec$ . Determine the order of the Butterworth Analog filter?

- [ ] Must Checkout this 📅 2025-11-14 

* ==Passband attenuation== $A_p=1\ \text{dB}$ at $\Omega_p=200\ \text{rad/s}$.
* ==Stopband attenuation== $A_s=30\ \text{dB}$ at $\Omega_s=600\ \text{rad/s}$.
    

For a Butterworth lowpass,

$$|H(j\Omega)|=\frac{1}{\sqrt{1+(\Omega/\Omega_c)^{2n}}}.$$

So

$$\frac{1}{|H(j\Omega)|^2}-1=(\Omega/\Omega_c)^{2n}.$$

Divide the equations at $\Omega_s$ and $\Omega_p$ to eliminate $\Omega_c$:

$$\Big(\frac{\Omega_s}{\Omega_p}\Big)^{2n}  
=\frac{\dfrac{1}{|H(j\Omega_s)|^2}-1}{\dfrac{1}{|H(j\Omega_p)|^2}-1}.$$

With magnitudes from dB:

$$|H(j\Omega_p)|=10^{-A_p/20},\qquad |H(j\Omega_s)|=10^{-A_s/20}.$$

Plugging numbers and solving for $n$:

$$|H(j\Omega_p)|=10^{-1/20}=0.8912509,\quad |H(j\Omega_s)|=10^{-30/20}=0.03162278.$$ $$\frac{1}{|H(j\Omega_s)|^2}-1 \approx 999.0,\qquad  
\frac{1}{|H(j\Omega_p)|^2}-1 \approx 0.2589254.$$ $$n=\frac{\ln\!\big(999.0/0.2589254\big)}{2\ln(600/200)}\approx 3.7584.$$

Minimum integer order is

$$\boxed{n=4.}$$

(If you want the analog cutoff $\Omega_c$ used for the Butterworth prototype: $\Omega_c \approx 236.8\ \text{rad/s}$.)



# Why antialiasing filter is used in decimating systems?
>to prevent **aliasing**

In a decimator you’re doing something fundamentally dangerous: you’re **throwing away samples**. ==Anytime you reduce the sampling rate, the allowable bandwidth of the signal shrinks==. Nature doesn’t politely compress the spectrum for you — everything above the new Nyquist limit folds back like a funhouse mirror. That folding is aliasing.

So before down-sampling, you slip in an anti-aliasing filter — a low-pass guardian at the gate.

Think of it this way:  
When you decimate by a factor $M$, the new sampling frequency becomes $F_s/M$.  
The new Nyquist limit becomes $F_s/(2M)$.  
All spectral content between this new limit and the old one has nowhere to go but **backward**, overlaying itself on the band you actually want.

The anti-aliasing filter’s job is simple and strict:

It **removes all frequency components above the new Nyquist frequency** before the sampler begins skipping points.

A small picture in words:

* Original bandwidth: wide highway.
    
* After decimation: half the lanes are removed.
    
* Without filtering: cars from the removed lanes crash into the remaining ones.
    
* Anti-aliasing filter: closes those lanes before cars ever drive into them.
    

DSP textbooks give bigger formulas, but the intuition is this: decimation reduces your “spectral headroom,” and the anti-aliasing filter trims everything that doesn’t fit.

If you’re exploring multirate filters deeper, the next fun curiosity is how polyphase structures make the filtering and decimation happen with far fewer multiplications.