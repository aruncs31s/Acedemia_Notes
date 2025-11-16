# Study Plan: AC Module 2 - Random Variables & Random Processes

## 📚 Overview
**Duration:** 10-12 days  
**Topics:** Probability Theory, Entropy, Information Theory, Stochastic Processes  
**Goal:** Master statistical concepts for communication systems

---

## 🎯 Learning Objectives
- [ ] Master discrete and continuous random variables
- [ ] Understand CDF, PDF relationships and calculations
- [ ] Calculate entropy and mutual information
- [ ] Analyze stochastic processes (WSS, SSS)
- [ ] Apply Wiener-Khinchin theorem for PSD analysis

---

## 📅 Day-wise Study Schedule

### **Day 1-2: Random Variables Fundamentals**

#### Study Tasks:
- [ ] **Discrete vs Continuous RVs**
  - Countable vs uncountable sets
  - PMF vs PDF concepts
  
- [ ] **CDF (Cumulative Distribution Function)**
  - Definition: $F_X(x) = P(X \leq x)$
  - Properties: non-decreasing, boundaries, right continuous
  - Discrete vs continuous CDF visualization
  
- [ ] **PDF (Probability Density Function)**
  - Relationship: $f_X(x) = \frac{dF_X(x)}{dx}$
  - Why $P(X=x) = 0$ for continuous RVs
  - Common distributions: Gaussian, Uniform, Exponential

#### Practice Problems:
1. Given PMF, calculate CDF for discrete RV
2. Given PDF, find probabilities over intervals
3. Verify PDF normalization: $\int f_X(x)dx = 1$

---

### **Day 3-4: Statistical Averages**

#### Study Tasks:
- [ ] **Expected Value (Mean)**
  - Discrete: $E[X] = \sum x_i p(x_i)$
  - Continuous: $E[X] = \int x f_X(x) dx$
  
- [ ] **Variance and Standard Deviation**
  - Formula: $\sigma^2 = E[X^2] - (E[X])^2$
  - Physical interpretation: spread/uncertainty
  
- [ ] **Moments**
  - 1st moment = mean
  - 2nd moment = power
  - Higher moments: skewness, kurtosis

#### Practice Problems:
1. Calculate mean and variance for given distributions
2. Find second moment and relate to power
3. Gaussian distribution: 68-95-99.7 rule applications

---

### **Day 5-6: Entropy & Information Theory**

#### Study Tasks:
- [ ] **Discrete Entropy**
  - Formula: $H(X) = -\sum p(x) \log_2 p(x)$ [bits]
  - Maximum entropy: $H_{max} = \log_2 n$
  - Binary source examples
  
- [ ] **Differential Entropy**
  - Continuous case: $H(X) = -\int f(x) \log_2 f(x) dx$
  - Can be negative (unlike discrete!)
  
- [ ] **Gaussian Entropy (Critical!)**
  - $H = \frac{1}{2}\log_2(2\pi e \sigma^2)$ bits
  - Depends only on variance
  - Maximum entropy property

#### Practice Problems:
1. Calculate entropy for fair vs biased coin
2. Find differential entropy for uniform distribution
3. Compute Gaussian entropy for given variance
4. Compare entropy of different distributions

---

### **Day 7-8: Conditional Entropy & Mutual Information**

#### Study Tasks:
- [ ] **Conditional Entropy**
  - $H(X|Y)$ = uncertainty in X given Y
  - $H(X|Y) = 0$ → complete dependence
  - $H(X|Y) = H(X)$ → independence
  
- [ ] **Mutual Information**
  - $I(X;Y) = H(X) - H(X|Y)$
  - Always non-negative: $I(X;Y) \geq 0$
  - Symmetric: $I(X;Y) = I(Y;X)$
  
- [ ] **Chain Rule**
  - $H(X,Y) = H(X) + H(Y|X)$
  
- [ ] **Channel Capacity**
  - $C = \max_{p(x)} I(X;Y)$
  - Shannon's formula: $C = B \log_2(1 + SNR)$

#### Practice Problems:
1. Calculate conditional entropy for joint distributions
2. Find mutual information between input/output
3. Verify $I(X;Y) = H(X) + H(Y) - H(X,Y)$
4. Channel capacity calculations

---

### **Day 9-10: Stochastic Processes**

#### Study Tasks:
- [ ] **Definition & Classification**
  - Collection of RVs indexed by time
  - Discrete vs continuous time/amplitude
  - Examples: AWGN, bit sequences
  
- [ ] **Strict Sense Stationary (SSS)**
  - All statistics invariant to time shift
  - Very restrictive condition
  
- [ ] **Wide Sense Stationary (WSS)**
  - Condition 1: $E[X(t)] = \mu$ (constant)
  - Condition 2: $R_X(t_1,t_2) = R_X(\tau)$
  - Easier to verify than SSS
  - For Gaussian: WSS ⟺ SSS

#### Practice Problems:
1. Determine if given process is WSS or SSS
2. Verify WSS conditions for random processes
3. Calculate mean and autocorrelation functions

---

### **Day 11-12: Autocorrelation & PSD**

#### Study Tasks:
- [ ] **Autocorrelation Function**
  - $R_X(\tau) = E[X(t)X(t+\tau)]$
  - Properties: maximum at origin, even function
  - $R_X(0) = E[X^2]$ = average power
  
- [ ] **Power Spectral Density (PSD)**
  - Fourier transform of autocorrelation
  - Wiener-Khinchin: $R_X(\tau) \stackrel{\mathcal{F}}{\longleftrightarrow} S_X(f)$
  - Total power: $P = \int S_X(f) df$
  
- [ ] **LTI Systems with WSS Input**
  - Output PSD: $S_Y(f) = |H(f)|^2 S_X(f)$
  - Output power: $P_Y = \int |H(f)|^2 S_X(f) df$
  - WSS input → WSS output

#### Practice Problems:
1. Find PSD from autocorrelation (Fourier transform)
2. Calculate total power from PSD
3. Determine output PSD for filtered signals
4. White noise examples: $S_X(f) = N_0/2$

---

## 🔑 Key Formulas to Memorize

### Random Variables:
```
F_X(x) = P(X ≤ x)
f_X(x) = dF_X(x)/dx
E[X] = ∫ x f_X(x) dx
σ² = E[X²] - (E[X])²
```

### Entropy:
```
H(X) = -Σ p(x) log₂ p(x)  [discrete]
H(X) = -∫ f(x) log₂ f(x) dx  [continuous]
H_Gaussian = ½ log₂(2πe σ²)  [CRITICAL!]
I(X;Y) = H(X) - H(X|Y)
```

### Stochastic Processes:
```
R_X(τ) = E[X(t)X(t+τ)]
R_X(τ) ⟷ S_X(f)  [Wiener-Khinchin]
S_Y(f) = |H(f)|² S_X(f)
P_total = R_X(0) = ∫ S_X(f) df
```

---

## 📊 Self-Assessment Checklist

### Conceptual Understanding:
- [ ] Explain why P(X=x)=0 for continuous RVs
- [ ] Why Gaussian maximizes entropy for given variance
- [ ] Difference between WSS and SSS
- [ ] Physical meaning of autocorrelation decay
- [ ] Why differential entropy can be negative

### Problem-Solving Skills:
- [ ] Calculate CDF from PDF and vice versa
- [ ] Compute entropy for any distribution
- [ ] Find mutual information from joint distributions
- [ ] Determine stationarity of processes
- [ ] Apply Wiener-Khinchin theorem

### Exam Readiness:
- [ ] Derive Gaussian entropy formula
- [ ] Prove autocorrelation properties
- [ ] Solve LTI system output problems
- [ ] Handle multi-part numerical questions

---

## 🎯 Success Tips

1. **Master Gaussian Distribution:** Most important for communication systems
2. **Practice Entropy Calculations:** Common exam questions
3. **Understand WSS Conditions:** Frequently tested concept
4. **Memorize Wiener-Khinchin:** Foundation for PSD analysis
5. **Draw Diagrams:** Visualize PDFs, CDFs, autocorrelation
6. **Connect Concepts:** Link entropy to channel capacity

---

## 📚 Common Exam Questions

**Q1:** Why is Gaussian distribution important?
- Maximizes entropy → worst-case noise
- AWGN modeling
- Central Limit Theorem
- Analytic tractability

**Q2:** Difference between WSS and SSS?
- WSS: Only mean and autocorrelation time-invariant
- SSS: All statistics time-invariant
- For Gaussian: WSS ⟺ SSS

**Q3:** Why can differential entropy be negative?
- PDF can be > 1 for continuous RVs
- log₂(f) < 0 when f > 1
- Discrete entropy always ≥ 0

**Q4:** Wiener-Khinchin theorem application?
- Converts time-domain correlation to frequency-domain power
- Essential for filter analysis
- Total power = area under PSD

---

## 🔥 Priority Topics for Exam

### High Priority (Must Know):
1. ✅ Gaussian entropy formula
2. ✅ WSS conditions
3. ✅ Mutual information calculations
4. ✅ Wiener-Khinchin theorem
5. ✅ LTI system output PSD

### Medium Priority:
1. CDF/PDF relationships
2. Variance calculations
3. Conditional entropy
4. Autocorrelation properties

### Lower Priority:
1. Higher moments (skewness, kurtosis)
2. Specific distribution derivations
3. Advanced stationarity proofs

**Target Score:** 85%+ in Module 2 topics
