
## 🔹 Section 6: Introduction

**What is interval estimation?**

| Concept | Meaning | Example |
|---------|---------|---------|
| **Point Estimate** | A single number used to estimate a population parameter | Sample mean = 45 → we guess μ ≈ 45 |
| **Interval Estimate** | A *range* of values that likely contains the true parameter | "We're 95% confident μ is between 42 and 48" |
| **Estimator** | The sample statistic used to estimate a parameter | $\bar{x}$ estimates μ; $\hat{p}$ estimates p |

**✓ Key idea**: A point estimate is almost never exactly right. An interval estimate acknowledges uncertainty.

---

## 🔹 Section 6.1: Introduction (to inference)

**Statistical inference** = using sample data to draw conclusions about a population.

**Two types of estimates**:
1. **Point estimate**: One number (e.g., $\bar{x} = 45$)
2. **Interval estimate**: A range with a confidence level (e.g., 42 < μ < 48 with 95% confidence)

**Example**:  
A manager samples 50 new employees and finds $\bar{x} = 10$ hours to learn a job.  
→ Point estimate: μ ≈ 10 hours  
→ Interval estimate: "We're 95% confident the true mean is between 9.2 and 10.8 hours"

---

## 🔹 Section 6.2: Confidence Interval and Confidence Level

### What does "95% confident" really mean?

$$\boxed{\text{Confidence Level } = (1-\alpha) \times 100\%}$$

| Term | Meaning | Example |
|------|---------|---------|
| **Confidence Level** | Long-run percentage of intervals that contain the true parameter | 95% = if we repeated sampling 100 times, ~95 intervals would catch μ |
| **α (alpha)** | Probability the interval does NOT contain the parameter | α = 0.05 for 95% confidence |
| **$z_{\alpha/2}$** | Critical value from standard normal table | For 95%: $z_{0.025}$ = 1.96 |

**✓ Important**: The confidence level describes the *method*, not a single interval. The true μ is fixed—it's either in your interval or not.

[[how to find z by confidence interval]]
**Finding $z_{\alpha/2}$**:
- 90% confidence → α = 0.10 → α/2 = 0.05 → $z_{0.05}$ = 1.645
- 95% confidence → α = 0.05 → α/2 = 0.025 → $z_{0.025}$ = 1.96
- 99% confidence → α = 0.01 → α/2 = 0.005 → $z_{0.005}$ = 2.575

---

## 🔹 Section 6.3: Confidence Intervals for μ — Normal Population (or n≥30), σ Known

**When to use**: 
- Population is normal (or approximately normal)
- Population standard deviation σ is **known**
- Any sample size n

$$\boxed{\bar{x} \pm z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}}}$$

**Worked Example**:  
σ = 8, n = 36, $\bar{x}$ = 45.3, 95% confidence  
→ $z_{0.025}$ = 1.96  
→ Standard error = $\frac{8}{\sqrt{36}} = \frac{8}{6} = 1.333$  
→ Margin of error = $1.96 \times 1.333 = 2.61$  
→ Interval: $45.3 \pm 2.61$ → **(42.69, 47.91)**

✓ We are 95% confident the population mean μ is between 42.69 and 47.91.

---

## 🔹 Section 6.4: Confidence Intervals for μ — Large Sample (σ Unknown)

**When to use**:
- Sample size n ≥ 30 (large sample)
- σ is **unknown** → use sample standard deviation $s_x$ instead
- Population shape doesn't matter (Central Limit Theorem applies)

$$\boxed{\bar{x} \pm z_{\alpha/2} \cdot \frac{s_x}{\sqrt{n}}}$$

**Why this works**: For large n, $s_x$ is a good estimate of σ, and $\bar{x}$ is approximately normal.

**Worked Example**:  
n = 64, $\bar{x}$ = 172, $s_x^2$ = 299 → $s_x = \sqrt{299} = 17.29$, 99% confidence  
→ $z_{0.005}$ = 2.58  
→ Standard error = $\frac{17.29}{\sqrt{64}} = \frac{17.29}{8} = 2.16$  
→ Margin of error = $2.58 \times 2.16 = 5.57$  
→ Interval: $172 \pm 5.57$ → **(166.43, 177.57)**

---

## 🔹 Section 6.5: Confidence Intervals for μ — Small Sample, σ Unknown

**When to use**:
- n < 30 (small sample)
- σ is **unknown**
- Population is **normally distributed** (critical assumption!)

→ We cannot use z; we must use the **t-distribution**.
[[how to find t by confidence interval]]

---

### 🔹 Section 6.5.1: Student's t Distribution

| Feature     | Standard Normal (z) | Student's t                                      |
| ----------- | ------------------- | ------------------------------------------------ |
| Shape       | Bell-shaped, fixed  | Bell-shaped, but varies with df                  |
| Mean        | 0                   | 0                                                |
| Spread      | Fixed (σ = 1)       | Wider for small df, approaches z as df increases |
| When to use | σ known OR large n  | σ unknown + small n + normal population          |

**Degrees of freedom (df)**: $df = n - 1$  
✓ We lose 1 df because we use $\bar{x}$ to calculate $s_x$.

**Finding $t_{\alpha/2, df}$**: Use t-table (Table 4 in Appendix)  
Example: 95% confidence, n = 10 → df = 9 → $t_{0.025, 9}$ = 2.262

---

### 🔹 Section 6.5.2: Confidence Interval for μ — Small Samples

$$\boxed{\bar{x} \pm t_{\alpha/2, n-1} \cdot \frac{s_x}{\sqrt{n}}}$$

**Worked Example**:  
n = 25 buses, $\bar{x}$ = 225 passengers, $s_x$ = 60, 90% confidence  
→ df = 25 − 1 = 24  
→ $t_{0.05, 24}$ = 1.711 (from t-table)  
→ Standard error = $\frac{60}{\sqrt{25}} = 12$  
→ Margin of error = $1.711 \times 12 = 20.53$  
→ Interval: $225 \pm 20.53$ → **(204.47, 245.53)**

✓ We are 90% confident the true mean passengers per bus is between 204.47 and 245.53.

---

## 🔹 Section 6.6: Confidence Intervals for Population Proportion p — Large Samples

**When to use**:
- Estimating a proportion (e.g., % unemployed, % who prefer X)
- Sample is large enough that: $\boxed{npq > 9}$  
  where $p$ ≈ $\hat{p}$, $q = 1 - p$, and n = sample size

$$\boxed{\hat{p} \pm z_{\alpha/2} \cdot \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}}$$

**Worked Example**:  
Sample of 800 people, 75 unemployed → $\hat{p} = 75/800 = 0.09375$, 90% confidence  
✓ Check: $n\hat{p}\hat{q} = 800 \times 0.09375 \times 0.90625 = 67.97 > 9$ ✓  
→ $z_{0.05}$ = 1.645  
→ Standard error = $\sqrt{\frac{0.09375 \times 0.90625}{800}} = 0.0103$  
→ Margin of error = $1.645 \times 0.0103 = 0.0169$  
→ Interval: $0.09375 \pm 0.0169$ → **(0.0768, 0.1107)** or **(7.68%, 11.07%)**

✓ We are 90% confident the true unemployment rate is between 7.68% and 11.07%.

---

## 🔹 Section 6.7: Confidence Intervals for Difference Between Two Means (μₓ − μᵧ)

**Goal**: Estimate how much two population means differ.

| Case | When to Use | Formula |
|------|------------|---------|
| **6.7.1 Paired samples** | Same subjects measured twice (before/after) or matched pairs | $\bar{d} \pm t_{\alpha/2, n-1} \cdot \frac{s_d}{\sqrt{n}}$ |
| **6.7.2 Independent, σ known** | Two independent samples, both σₓ and σᵧ known | $(\bar{x} - \bar{y}) \pm z_{\alpha/2} \cdot \sqrt{\frac{\sigma_x^2}{n_x} + \frac{\sigma_y^2}{n_y}}$ |

---

### 🔹 Section 6.7.1: Paired Samples

**Steps**:
1. Compute differences: $d_i = x_i - y_i$ for each pair
2. Find $\bar{d}$ and $s_d$ (mean and SD of differences)
3. Use t-interval with df = n − 1

**Worked Example**:  
7 people, weights before/after exercise program:

| Person | Before | After | d = Before − After |
|--------|--------|-------|-------------------|
| 1 | 68 | 62 | 6 |
| 2 | 81 | 76 | 5 |
| 3 | 98 | 86 | 12 |
| 4 | 86 | 79 | 7 |
| 5 | 110 | 103 | 7 |
| 6 | 92 | 87 | 5 |
| 7 | 80 | 82 | −2 |

→ $\bar{d} = 40/7 = 5.71$, $s_d = \sqrt{\frac{332 - 7(5.71)^2}{6}} = 4.16$  
→ n = 7, df = 6, 90% confidence → $t_{0.05, 6}$ = 1.943  
→ Standard error = $\frac{4.16}{\sqrt{7}} = 1.57$  
→ Margin of error = $1.943 \times 1.57 = 3.05$  
→ Interval: $5.71 \pm 3.05$ → **(2.66, 8.76)**

✓ We are 90% confident the mean weight loss is between 2.66 and 8.76 kg.

---

### 🔹 Section 6.7.2: Independent Samples, Known Variances

**When to use**:
- Two independent random samples
- Both populations normal
- Both population variances σₓ² and σᵧ² are **known**

$$\boxed{(\bar{x} - \bar{y}) \pm z_{\alpha/2} \cdot \sqrt{\frac{\sigma_x^2}{n_x} + \frac{\sigma_y^2}{n_y}}}$$

**Worked Example**:  
Sample 1: nₓ = 13, $\bar{x}$ = 31.4, σₓ² = 100  
Sample 2: nᵧ = 7, $\bar{y}$ = 38.1, σᵧ² = 80, 95% confidence  
→ $z_{0.025}$ = 1.96  
→ Standard error = $\sqrt{\frac{100}{13} + \frac{80}{7}} = \sqrt{7.69 + 11.43} = \sqrt{19.12} = 4.37$  
→ Margin of error = $1.96 \times 4.37 = 8.57$  
→ Difference: $\bar{x} - \bar{y} = 31.4 - 38.1 = -6.7$  
→ Interval: $-6.7 \pm 8.57$ → **(−15.27, 1.87)**

✓ We are 95% confident the true difference μₓ − μᵧ is between −15.27 and 1.87.  
✓ Since the interval includes 0, we cannot conclude the means are different.

---

## 📋 Summary Table: Which Formula When?

| Section | Parameter | Conditions | Formula |
|---------|-----------|-----------|---------|
| **6.3** | μ (one mean) | Normal pop, σ known, any n | $\bar{x} \pm z \cdot \frac{\sigma}{\sqrt{n}}$ |
| **6.4** | μ (one mean) | Large n (≥30), σ unknown | $\bar{x} \pm z \cdot \frac{s_x}{\sqrt{n}}$ |
| **6.5.2** | μ (one mean) | Small n (<30), σ unknown, normal pop | $\bar{x} \pm t \cdot \frac{s_x}{\sqrt{n}}$ |
| **6.6** | p (proportion) | Large sample: $npq > 9$ | $\hat{p} \pm z \cdot \sqrt{\frac{\hat{p}q}{n}}$ |
| **6.7.1** | μₓ − μᵧ (paired) | Paired data, normal differences | $\bar{d} \pm t \cdot \frac{s_d}{\sqrt{n}}$ |
| **6.7.2** | μₓ − μᵧ (indep.) | Independent, normal, σₓ & σᵧ known | $(\bar{x}-\bar{y}) \pm z \cdot \sqrt{\frac{\sigma_x^2}{n_x}+\frac{\sigma_y^2}{n_y}}$ |

---

## 🛠️ How to Choose the Right Method: Quick Checklist

1. **What parameter?**  
   → One mean (μ)? → Go to steps 2–4  
   → One proportion (p)? → Use Section 6.6 (check $npq > 9$)  
   → Difference of means (μₓ − μᵧ)? → Paired (6.7.1) or independent (6.7.2)?

2. **Is σ known?**  
   → Yes → Use z-formula (Section 6.3 or 6.7.2)  
   → No → Go to step 3

3. **Is sample large (n ≥ 30)?**  
   → Yes → Use z with $s_x$ (Section 6.4)  
   → No → Go to step 4

4. **Is population normal?**  
   → Yes → Use t-formula (Section 6.5.2)  
   → No → Cannot use these methods; need nonparametric or larger sample

5. **For proportions**: Always check $npq > 9$ using $\hat{p}$ as estimate of p.

**✓ Final tip**: When in doubt, write down:  
- What you're estimating  
- What you know (σ? n? normal?)  
- Then match to the table above.

---
