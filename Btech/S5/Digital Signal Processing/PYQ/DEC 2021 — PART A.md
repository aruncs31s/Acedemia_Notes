
# ✅ **DEC 2021 — PART A**

ECT303 DIGITAL SIGNAL PROCESSIN…
### **1) Methods of filtering long sequences**
- [[Filtering Long Sequences]]

Overlap-Add and Overlap-Save. Both split the long signal into blocks, use FFT-based convolution, and stitch the output back.

### **2) Three properties of DFT**

Linearity, Time shift ↔ phase shift, Circular convolution property.

### **3) 4-point DFT of cos(2πn)**

cos(2πn) = 1 for all n → sequence = {1,1,1,1}.  
DFT = {4,0,0,0}.

### **4) Circular time reversal of [8,5,3,1]**

Reverse indices mod-N → [1,3,5,8].

### **5) Butterworth IIR design steps**

Find filter order → analog Butterworth poles → analog H(s) → map to digital using bilinear transform.

### **6) Advantage of frequency-sampling FIR design**

Easy control of frequency response, flexible shaping, simple implementation for some responses.

### **7) Cascade implementation of IIR**

Break H(z) into 2nd-order (biquad) sections to improve stability and numerical accuracy.

### **8) Linear-phase FIR — conditions**

Impulse response must be symmetric or antisymmetric:  
h[n] = h[N−1−n] or h[n] = −h[N−1−n].

### **9) DSP processor vs General-purpose processor (3 points)**

DSP: fast MAC, Harvard architecture, deterministic timing.  
GPP: slower MAC, shared memory, general tasks.

### **10) Three applications of DSP processors**

Audio processing, communication modems, radar/sonar.
