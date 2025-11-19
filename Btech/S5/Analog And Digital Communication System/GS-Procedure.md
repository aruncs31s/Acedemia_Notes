---
id: GS-Procedure
aliases: []
tags: []
---

# According to YT

1. First calculate $\phi_{1} (t)$
   $$
   \phi_{1} (t) = \frac{{y_{1}(t)}}{\sqrt{ Energy }}
   $$
   $$
   \phi_{1} (t) = \frac{{y_{1}(t)}}{\int_{0}^T {A dt}}
   $$

Where $A$ is the ambliture of the given wave 2. For finding $\phi_{2} (t)$ calculate the intermediate function $g_{2}(t)$

$$
g_{i}(t) = y_{i}(t) - \sum_{j=1}^{i - 1} y_{ij} \phi_{j} (t)
$$

and for finding $y_{ij}(t)$

$$
s_{ij}(t) = \int_{0}^{T} s_{i}(t) \times \phi_{j}(t) dt
$$

or

$$


y_{ij}(t) = \int_{0}^{T} y_{i}(t) \times \phi_{j}(t) dt
$$

# Core G–S equations

1. First basis vector (normalize first signal that is nonzero):

$$u_1(t)=s_1(t),\qquad \phi_1(t)=\frac{u_1(t)}{\|u_1\|}=\frac{s_1(t)}{\sqrt{\langle s_1,s_1\rangle}}.$$

2. For $k=2,\dots,M$:

$$u_k(t)=s_k(t)-\sum_{j=1}^{k-1}\langle s_k,\phi_j\rangle\,\phi_j(t).$$

If $u_k\neq 0$, normalize:

$$\phi_k(t)=\frac{u_k(t)}{\|u_k\|}=\frac{u_k(t)}{\sqrt{\langle u_k,u_k\rangle}}.$$

If $u_k=0$ (dependent), skip and do not increase $K$.

3. Coefficients (signal-space coordinates):

$$a_{ik}=\langle s_i,\phi_k\rangle=\int_T s_i(t)\,\phi_k(t)\,dt.$$

Each original signal expands as

$$s_i(t)=\sum_{k=1}^{K} a_{ik}\,\phi_k(t).$$

Matrix form (compact): let $\Phi=[\phi_1\ \phi_2\ \cdots\ \phi_K]$ and for a single signal $s$,

$$\mathbf a = \Phi^\top \mathbf s,\qquad \text{where } a_k=\langle s,\phi_k\rangle.$$

---

# Step-by-step recipe to compute $i_{jt}$ (projection coefficients)

1. Compute all pairwise inner products needed:  
   $\langle s_k,s_\ell\rangle = \int_T s_k(t)s_\ell(t)\,dt$. (Used in projections.)
2. Initialize $k\leftarrow1$.
   - Set $u_1(t)=s_1(t)$.
   - If $\|u_1\|=0$ choose next nonzero signal; otherwise $\phi_1(t)=u_1/\|u_1\|$.

3. For each $k=2$ to $M$:
   - Compute projections of $s_k$ onto existing $\phi_j$: $p_{kj}=\langle s_k,\phi_j\rangle$ for $j=1\ldots,k-1$.
   - Form residual $u_k(t)=s_k(t)-\sum_{j=1}^{k-1} p_{kj}\,\phi_j(t)$.
   - If $\|u_k\|>0$ then $\phi_k=u_k/\|u_k\|$; else $s_k$ is in span$(\phi_1,\dots,\phi_{k-1})$ and is discarded.
   - Continue until all signals processed; final $K$ is number of orthonormal basis functions.

4. Compute coefficients $a_{ik}=\langle s_i,\phi_k\rangle$ for every original signal $s_i$ and each basis $\phi_k$. These $a_{ik}$ are the $i_{jt}$-type values used in signal-space diagrams and in ML/MAP decision rules.

---

# Small worked example (two signals)

Given $s_1,s_2$:

- $\phi_1=\dfrac{s_1}{\sqrt{\langle s_1,s_1\rangle}}$.
- $u_2=s_2-\langle s_2,\phi_1\rangle\phi_1$.
- $\phi_2=u_2/\|u_2\|$ (if nonzero).
- Coefficients: $a_{11}=\langle s_1,\phi_1\rangle=\|s_1\|$, $a_{12}=\langle s_1,\phi_2\rangle$, $a_{21}=\langle s_2,\phi_1\rangle$, $a_{22}=\langle s_2,\phi_2\rangle$.

---

# Practical notes

- For real signals use the real inner product above; for complex signals use $\langle x,y\rangle=\int x(t)\,y^*(t)\,dt$.
- If signals are discrete/time-sampled evaluate the integrals by sums (numerical quadrature): $\langle x,y\rangle\approx\sum_n x[n]\,y[n]\,\Delta t$.
- Keep numerical orthogonality stable: when $M$ large, consider modified Gram–Schmidt or orthonormalization using QR on a sampled matrix of signals.
