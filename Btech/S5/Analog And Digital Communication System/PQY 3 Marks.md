---
id: PQY 3 Marks
aliases: []
tags: []
---

# PYQ 3 Marks

## Compare AM , DSB-SC SSB SC with respect to bacndwidth and system complexity

### AMPLITUDE MODULATION (AM)

You take a carrier and wiggle its amplitude in proportion to the message signal. It’s the most textbook, budget-friendly modulation method.

**Key points**  
• Carrier + both sidebands are transmitted.  
• Simple transmitter and very simple envelope detector receiver.  
• Wastes power (carrier has no information).  
• Wastes bandwidth (two sidebands carrying the same info).

---

### DOUBLE-SIDEBAND SUPPRESSED CARRIER (DSB-SC)

You remove the carrier but keep both sidebands. Now the transmitter stops being lazy.

**Key points**  
• No carrier ⇒ more power goes toward the actual message.  
• Still transmits both sidebands, so same bandwidth as AM.  
• Receiver needs synchronous detection (must regenerate carrier).  
• Medium complexity system.

---

### SINGLE-SIDEBAND SUPPRESSED CARRIER (SSB-SC)

You knock out the carrier _and_ knock out one entire sideband. It’s the minimalist of modulation.

**Key points**  
• Only one sideband transmitted.  
• Extremely bandwidth-efficient.  
• Very power-efficient.  
• Highest transmitter/receiver complexity (filters, phasing, or Hilbert transform).  
• Used where spectrum is precious (HF radio, telephony, etc.).

---

## COMPARISON TABLE (This is what the examiner wants)

| Scheme     | Bandwidth | Power Efficiency                          | Carrier Sent? | Complexity                           |
| ---------- | --------- | ----------------------------------------- | ------------- | ------------------------------------ |
| **AM**     | $2 f_m$   | Very low (carrier consumes ~2/3 of power) | Yes           | Very low (simple envelope detector)  |
| **DSB-SC** | $2 f_m$   | Better (no carrier)                       | No            | Medium (requires coherent detection) |
| **SSB-SC** | $f_m$     | Highest                                   | No            | High (sideband filtering / phasing)  |

Where $f_m$ is the maximum message frequency.

---

### Final 3-mark summary (write this in your paper)

AM transmits carrier + both sidebands, uses bandwidth $2f_m$ and has very low power efficiency but simple circuitry.  
DSB-SC suppresses the carrier but keeps both sidebands, still uses $2f_m$ bandwidth and requires coherent detection, giving moderate complexity and better power efficiency.  
SSB-SC suppresses carrier and one sideband, using only $f_m$ bandwidth with highest efficiency, but increased system complexity due to filtering or phasing.

## With suitable block diagram explain the generation of wideband FM using narrow band FM.

### Generation of Wideband FM using Narrowband FM

To generate wideband FM (WBFM) from narrowband FM (NBFM), we can use a ==frequency multiplier==. ==The basic idea is to first create a narrowband FM signal and then increase its frequency deviation to achieve wideband characteristics==.

### NARROWBAND FM (NBFM)

NBFM happens when the **modulation index $\beta = \frac{\Delta f}{f_m} \ll 1$**. (There is less deviation from its maxmum frequency of carrier signal $f_c$)The frequency deviation is small, the spectrum looks like AM with phase twist, and the bandwidth is close to **$2 f_m$**.

### Block Diagram (NBFM)

```
Message m(t) → Integrator → Phase Modulator → NBFM Signal
                          ↑
                          Carrier Oscillator (cos ωc t)
```

An alternative practical block diagram (using indirect method):

```
Message m(t) → Integrator → Multiplier/Mixer → Add Carrier → NBFM Signal
                   ↑                             ↑
                   |                             |
              Carrier Oscillator ------------→ Phase Modifier
```

### Explanation

• Integration converts FM into phase modulation form:  
 FM: instantaneous phase = ωc t + kf ∫m(τ)dτ  
• A phase modulator driven by the integrated message creates small phase deviations ⇒ NBFM.  
• Because $\beta \ll 1$, only carrier + first sidebands appear.

Useful intuition: NBFM behaves like AM’s shy cousin—tiny wiggles around the carrier.

---

# WIDEBAND FM (WBFM)

Wideband FM enters the scene when the modulation index is **much greater than 1**,  
$\beta \gg 1$.  
Frequency swings are large and the spectrum contains many sidebands.  
Bandwidth ≈ **Carson’s Rule**:

$$B = 2(\Delta f + f_m)$$

### Block Diagram (WBFM)

**Indirect (Armstrong) Method** – Very important for exams

```
           ┌──────────┐
   m(t) →  │ Integrator │ → Phase Modulator → Mixer/Multiplier → Wideband FM
           └──────────┘             ↑
                                     Carrier (stable crystal oscillator)
```

Expanded Armstrong block diagram:

```
Message m(t)
     ↓
Integrator
     ↓
Phase Modulator (generates NBFM)
     ↓
Frequency Multiplier(s) (increase modulation index β)
     ↓
Mixer/Upconverter (shift to desired carrier frequency)
     ↓
Wideband FM Output
```

### Explanation

• You first generate **NBFM** because it’s easy to create small phase changes accurately.  
• Frequency multipliers scale the deviation:  
 e.g., multiply by 10 ⇒ deviation ×10 ⇒ β ×10  
• Mixer shifts the signal to the final transmission frequency.  
• Final output is **true wideband FM** with β ≫ 1 and large deviation.

WBFM is the extroverted, full-spectrum storyteller—big swings, rich harmonics.

---

# Short 3–5 Mark Answer (ready to write)

**Narrowband FM (NBFM)** is FM with small modulation index $\beta \ll 1$. Only the first pair of sidebands exist and its bandwidth ≈ 2 fₘ. It can be generated by integrating the message and applying it to a phase modulator. The block diagram shows:  
m(t) → integrator → phase modulator → NBFM.

**Wideband FM (WBFM)** has large modulation index $\beta \gg 1$ and many significant sidebands. Its bandwidth is given by Carson’s rule $B = 2(\Delta f + f_m)$. It is generated by Armstrong’s indirect method: first form NBFM using an integrator + phase modulator, then use frequency multipliers and a mixer to obtain the required deviation and carrier frequency.
