# Module 5

## BPSK Error Probability

Binary Phase Shift Keying (BPSK) is a digital modulation scheme where binary data (0s and 1s) is represented by shifting the phase of a carrier signal by 0° or 180°.

The bit error probability (BER) for BPSK in an Additive White Gaussian Noise (AWGN) channel is given by:

$$ P_e = Q\left(\sqrt{\frac{2E_b}{N_0}}\right) $$

where:
- $E_b$ is the energy per bit,
- $N_0$ is the noise power spectral density,
- $Q(x)$ is the tail probability of the standard normal distribution, defined as $Q(x) = \frac{1}{\sqrt{2\pi}} \int_x^\infty e^{-t^2/2} \, dt$.

This formula assumes coherent detection and ideal synchronization. For non-coherent detection, the BER is higher, approximately $ \frac{1}{2} e^{-E_b/(2N_0)} $. In fading channels, the error probability depends on the fading model (e.g., Rayleigh fading).

### Related Notes
- [[AC_Module_4]] - Previous module on modulation basics
- [[Digital Communication Systems]] - Overview
