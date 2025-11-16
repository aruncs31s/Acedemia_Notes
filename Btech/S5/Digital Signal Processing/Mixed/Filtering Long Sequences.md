---
id: filtering-long-sequences
tags:
    - academics
    - btech
    - s5
    - digital_signal_processing
    - convolution
    - fft
updated: 2025-11-15
---

> [!toc]
> - [[#Overlap-Add Method|Overlap-Add]]
> - [[#Overlap-Save Method|Overlap-Save]]
> - [[#Tips-and-tradeoffs|Tips and tradeoffs]]

When dealing with long sequences, direct linear convolution can be computationally expensive (O(NM)). To efficiently filter long sequences, use FFT-based block convolution: Overlap‑Add and Overlap‑Save — both compute convolution using FFTs and reduce the cost to about O(N log N) per block.

## 🔗 Overlap-Add Method
> [!objective] Overview
> Split the input into non-overlapping blocks, use FFT-based convolution and add overlapped tails to assemble the full output.

```mermaid
graph TB
    X[Long input x[n]] --> B[Split into blocks (length L)]
    B --> Z[Zero-pad to N and FFT]
    Z --> M[Multiply by H[k] (FFT of h)]
    M --> I[IFFT]
    I --> A[Overlap & Add]
    A --> Out[Output y[n]]
```

![[Overlap-Add Method.png]]

The Overlap-Add method involves the following steps:
1. **Segment the Input**: ==Divide the long input sequence== $x[n]$ into smaller, manageable segments of length $L$.
2. **Zero-Pad the Impulse Response**: ==Zero-pad== the impulse response $h[n]$ to length $L + M - 1$, where $M$ is the length of $h[n]$.
3. **Compute FFTs**: ==Compute the FFT== of each segment and the zero-padded impulse response.
4. **Multiply in Frequency Domain**: Multiply

Processing per block:
- Compute H = FFT(h, n=N).
- For each block: X = FFT(block), Y = X*H, y_block = IFFT(Y).real
- Discard first M−1 = 3 values from each y_block; remaining L = 5 values are the valid outputs for that block.
- Concatenate the kept parts of each block, then trim to the original input length (16).

Expected numeric result:
- y_direct = np.convolve(x, h) gives first 16 outputs:
    [1.00, 2.50, 3.50, 4.75, 6.00,
     7.25, 8.50, 9.75, 11.00, 12.25,
     13.50, 14.75, 16.00, 17.25, 18.50, 19.75]
- Overlap‑save produces the same first 16 samples:
    y_overlap_save == y_direct[:16]  (verified with np.allclose).

Notes:
- Each block contributes L valid samples after discarding the first M−1 corrupted samples.
- If the last block is partial, it is zero‑padded to length N; final concatenation is trimmed to len(x).
- Choose N as a power of two for faster FFTs and trade off memory for fewer FFTs. the FFTs of the segments with the FFT of the impulse response.
5. **Inverse FFT**: Compute the inverse FFT of the product to obtain the filtered segments.
6. **Overlap and Add**: Overlap the segments appropriately and add them to form the final output sequence.

#### Example (sketch) — Overlap‑Add (Python pseudocode)

```python
# Overlap-Add (sketch)
N = next_power_of_two(L + M - 1)
H = np.fft.fft(h, n=N)
out = np.zeros(len(x)+M-1)
for i in range(0, len(x), L):
    block = x[i:i+L]
    X = np.fft.fft(np.pad(block, (0, N-len(block))), n=N)
    yb = np.fft.ifft(X*H).real
    out[i:i+N] += yb
```

### Example — Overlap‑Save in Python (NumPy)

Filter (impulse response): h = [1, 0.5, -0.5, 0.25]  (M = 4)
Input: x = [1, 2, 3, ..., 16]  (len = 16)
Choose FFT length N = 8 → block data length L = N − M + 1 = 5
Overlap = M − 1 = 3

Python snippet (Overlap-Save):
- x_padded = [0, 0, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]
- Blocks (N = 8, step = L = 5):
    1. start=0:  [0, 0, 0, 1, 2, 3, 4, 5]
    2. start=5:  [3, 4, 5, 6, 7, 8, 9, 10]
    3. start=10: [8, 9, 10, 11, 12, 13, 14, 15]
    4. start=15: [13, 16, 0, 0, 0, 0]

Python snippet:

```python
import numpy as np

# sequences
x = np.arange(1, 17)                # input 1..16
h = np.array([1.0, 0.5, -0.5, 0.25])
M = len(h)

# parameters
N = 8                               # FFT length (>= M). choose power of two
L = N - M + 1                       # new samples per block
H = np.fft.fft(h, n=N)

# prepend M-1 zeros for first block (overlap-save)
x_padded = np.concatenate([np.zeros(M-1), x])
output_blocks = []

for start in range(0, len(x_padded) - (M - 1), L):
    segment = x_padded[start:start + N]       # take block of length N
    if len(segment) < N:
        segment = np.concatenate([segment, np.zeros(N - len(segment))])
    X = np.fft.fft(segment)
    Y = X * H
    y_block = np.fft.ifft(Y).real
    output_blocks.append(y_block[M-1:])       # discard first M-1 (corrupted) samples


y_overlap_save = np.concatenate(output_blocks)[:len(x)]   # trim to input length

# verify vs direct convolution
y_direct = np.convolve(x, h)
print("Overlap-Save output:", y_overlap_save)
print("Direct convolution:", y_direct[:len(x)])  # compare first len(x) samples
print("Equal up to numerical error:", np.allclose(y_overlap_save, y_direct[:len(x)]))
```

What to expect:
- The results of y_overlap_save should match the first len(x) samples of np.convolve(x, h).
- Choose N large enough to trade memory for fewer FFTs; power-of-two N tends to be faster.
- If the input length isn't an exact multiple of L, the code above zero-pads the final incomplete block.

This demonstrates how overlap-save uses overlapping blocks of length N and discards the M−1 leading (corrupted) samples from each IFFT result, then concatenates the rest to reconstruct the full filtered output.



## 🔗 Overlap-Save Method
The Overlap-Save method involves the following steps:
1. **Segment the Input with Overlap**: Divide the input sequence into overlapping segments, each of length $L + M - 1$, where $M$ is the length of the impulse response.
2. **Compute FFTs**: Compute the FFT of each segment and the impulse response (zero-padded to the same length).
3. **Multiply in Frequency Domain**: Multiply the FFTs of the segments with the FFT of the impulse response.
4. **Inverse FFT**: Compute the inverse FFT of the product.
5. **Discard Overlap**: Discard the first $M - 1$ samples of each segment to remove the overlap.
6. **Concatenate**: Concatenate the remaining parts of each segment to form the final output sequence.

## Tips and tradeoffs
> [!callout]- Tradeoffs
>
> - Choose block size L to balance latency vs throughput: larger L reduces FFT overhead but increases latency and memory.
> - Pick N as a power-of-two for fastest FFT performance. Set N >= L + M - 1.
> - Overlap-Save is generally better for streaming/real-time (simple sliding), overlap-add often works well for offline/blocked processing.

> [!callout]- Exam Tip
>
> - For exam answers, state the complexity (direct O(NM) vs FFT O(N log N)), define L, M, N, and show how to avoid aliasing (zero-padding to at least L+M-1).



<iframe width="560" height="315" src="https://www.youtube.com/embed/vNxOhLTxhzI?si=JkLklT-lxaY9fnvX" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

