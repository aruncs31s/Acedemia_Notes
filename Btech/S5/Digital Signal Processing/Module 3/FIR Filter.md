# FIR Filter


1. What are the advantage of FIR filters over IIR filters?
- FIR filters are inherently stable since they do not have feedback.
- They can have exactly linear phase response, which preserves the waveform of filtered signals.
- They are easier to design and implement for certain applications.
2. How is the impulse response of an FIR filter defined?
- The impulse response of an FIR filter is defined by its finite number of coefficients, which determine the filter's behavior.
3. What is the general form of the difference equation for an FIR filter?
- The general form of the difference equation for an FIR filter is:

$$y[n] = \sum_{k=0}^{M-1} h[k]\,x[n-k]$$

where:
- \(h[k]\) are the filter coefficients (taps)
- \(x[n]\) is the input signal
- \(y[n]\) is the output signal
- \(M\) is the number of taps (filter length)

This is the discrete convolution: \(y[n]=(h * x)[n]\) (or `y = h * x`).
- FIR filters can be designed using various methods such as the windowing method, the frequency sampling method, and the Parks-McClellan algorithm.
5. What is the significance of the filter order in FIR filters?
- The filter order determines the number of taps (coefficients) in the FIR filter, which affects the filter's frequency response and transition bandwidth.
6. How does the choice of window function affect FIR filter design?
- The choice of window function affects the side lobe levels and main lobe width in the frequency response of the FIR filter, influencing its performance in terms of ripple and transition sharpness.
7. What are some common applications of FIR filters?
- FIR filters are commonly used in applications such as audio processing, image processing, communications systems, and biomedical signal processing.
8. How can FIR filters be implemented in practice?
- FIR filters can be implemented using direct form structures, transposed structures, or using efficient algorithms like the overlap-add and overlap-save methods for long sequences.9. What is the relationship between FIR filters and convolution?
- The output of an FIR filter is obtained by convolving the input signal with the filter's impulse response, which is a finite sequence of coefficients.
10. How can the performance of an FIR filter be evaluated?
- The performance of an FIR filter can be evaluated by analyzing its frequency response, phase response, group delay, and computational efficiency.11. What is the effect of increasing the number of taps in an FIR filter?
- Increasing the number of taps in an FIR filter generally improves its frequency selectivity and reduces transition bandwidth, but it also increases computational complexity and delay. 

## What is the advantages of frequency sampling technique in FIR filter design?
- **Direct specification**: Allows direct specification of the desired frequency response at selected frequency samples.
- **Exact zeros/notches**: Enables easy placement of exact zeros or notches at specific frequencies.
- **Fast design**: Filter design is fast because it leverages FFT/IFFT computations.
- **Irregular responses**: Suitable for designing filters with irregular or discontinuous frequency responses.
- **Simplicity**: Conceptually simple—frequency samples → IFFT → FIR coefficients.


