- Definition of the unit impulse (discrete): $$ \delta[n]=\begin{cases}1,&n=0,\0,&n\ne0.\end{cases} $$
- Impulse response: the output of the system when the input is the unit impulse: $$ h[n]=\text{output when } x[n]=\delta[n]. $$
- Z-transform (transfer function) of the impulse response: $$ H(z)=\mathcal{Z}{h[n]}=\sum_{n=-\infty}^{\infty} h[n],z^{-n}. $$
- Input–output relation (convolution in time, multiplication in z‑domain): $$ y[n]=(h*x)[n]=\sum_{k=-\infty}^{\infty} h[k],x[n-k], \qquad Y(z)=H(z),X(z). $$
- Inverse Z‑transform (to recover h[n] from H(z)): $$ h[n]=\frac{1}{2\pi j}\oint_C H(z),z^{,n-1},dz, $$ or by expanding H(z) as a power series in (z^{-1}): $$ H(z)=\sum_{n=-\infty}^{\infty} h[n],z^{-n}\quad\Longrightarrow\quad h[n]=\text{coefficient of }z^{-n}. $$
- Useful properties:
    - Causality ⇔ ($h[n]=0$) for ($n<0$).
    - BIBO stability (discrete) ⇔ ($\sum_{n=-\infty}^\infty |h[n]|<\infty$).
    - Frequency response: ($H(e^{j\omega})=\sum_n h[n] e^{-j\omega n}$) (evaluate ($H(z)$) on the unit circle if ROC includes it).

So: h[n] is the impulse response (time-domain). H(z) is its Z-transform (complex-/frequency-domain representation).