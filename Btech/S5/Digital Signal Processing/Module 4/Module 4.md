## **1. Direct Form-I Realization (DF-I)**

Keep in mind: we’re not solving anything yet — just understanding the concept.

Think of an IIR system as having two ingredients:  
• a **feedforward path** (because of $x[n], x[n–1], x[n–2], …)$ 
• a **feedback path** (because of $y[n–1], y[n–2], …)$

The general difference equation looks like:

$$
y[n] = –a₁y[n–1] – a₂y[n–2] … + b₀x[n] + b₁x[n–1] + b₂x[n–2] …
$$

In Direct Form-I:

• You literally build **two separate delay chains**  
– one for$ x[n] $ 
– one for $y[n]$

• Both chains feed a big summer that computes $y[n]$.

# **2. Direct Form-II (DF-II)**

DF-II realizes that DF-I “wastes” memory by keeping two delay lines.  
But mathematically, those two delay lines can be merged.
### Imagine this like:

Instead of two separate shift registers, you compress them into **one single delay chain** called the **state chain**.

Core idea:  
• DF-II reduces memory  
• Same input–output behavior as DF-I  
• Uses a single set of delays to store internal state variables

If DF-I needed 2 delays, DF-II will need only **1 delay** for the same system.

A visual way to think about it:  
• First do feedback (IIR part)  
• Then do feedforward (FIR part)  
• Both share the same delay elements

Q2: Why does DF-II need fewer delays than DF-I?
The delays in the x-path and y-path are really storing **the same internal state**, so DF-II just collapses them into one shared chain. Nice.


## **3. Cascade Realization**

Think of a big IIR system as a product of smaller, simpler systems.
### How it works:
1. Factor H(z) into **second-order sections** (SOS) or sometimes first-order sections.
2. Realize each section separately (usually with DF-II).
3. Connect them **one after another**, like filters in series.
### Why engineers love this:
It improves numerical stability.  
Instead of one huge filter with big coefficients, we use small sections that behave nicely.
### Mental picture:

$$H(z) = H₁(z) × H₂(z) × H₃(z)$$

Implementation becomes:

$$x → [H₁] → [H₂] → [H₃] → y$$

Small sections = less rounding error, less coefficient sensitivity.


## How to get the impulse response from $H(z)$

- [[Impulse response]]
1. Recognize that $H(z)$ is the Z-transform of the impulse response[^1] $h[n]$.

$$
H(z) = \sum_{n=-\infty}^{\infty} h[n] z^{-n}
$$
For causal LTI systems, $h[n] = 0$ for $n < 0$, so the limits simplify to:
$$ H(z) = \sum_{n=-0}^{\infty} h[n] z^{-n} $$
2. If $H(z)$ is a finite polynomial in $z^{-1}$, you can directly read off the coefficients as the impulse response values:

$$
H(z) = b_0 + b_1 z^{-1} + b_2 z^{-2} + \ldots + b_M z^{-M})
$$
then the impulse response is simply the coefficient sequence:

$$ 
h[0] = b_0, \quad h[1] = b_1, \quad h[2] = b_2, \quad \ldots, \quad h[M] = b_M
$$


[^1]: the impulse response is the time-domain sequence $h[n]$ (or $h(t)$ in continuous time). $H(z)$ is its Z-transform — the transfer function (frequency-/complex-domain representation). $H(z)$ and $h[n]$ are two representations of the same LTI system.