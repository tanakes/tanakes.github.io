## First: What Do All These Letters Mean?

### Population vs Sample

| Symbol | Meaning                                                                            | Example                                 |
| ------ | ---------------------------------------------------------------------------------- | --------------------------------------- |
| $N$    | Total number of elements in the **population** (the whole group we care about)     | All 5000 students at a university       |
| $n$    | Total number of elements in the **sample** (the smaller group we actually measure) | 100 students we randomly pick to survey |
| $X_i$  | The value of the $i$-th element in the population                                  | Salary of employee #3: $35,000          |
| $x_i$  | The value of the $i$-th element in the sample                                      | Salary of sampled employee #2: $28,000  |

### Parameters vs Statistics

| Symbol            | Name                          | What it is                                   | Formula                                                           |
| ----------------- | ----------------------------- | -------------------------------------------- | ----------------------------------------------------------------- |
| $\mu$ (mu)        | Population mean               | Average of ALL elements in population        | $\mu = \frac{1}{N}\sum_{i=1}^{N} X_i$                             |
| $\sigma$ (sigma)  | Population standard deviation | Spread of ALL elements in population         | $\sigma = \sqrt{\frac{1}{N}\sum_{i=1}^{N}(X_i - \mu)^2}$          |
| $p$               | Population proportion         | Fraction of population with a characteristic | $p = \frac{\text{number with characteristic in population}}{N}$   |
| $\bar{X}$ (X-bar) | Sample mean                   | Average of the sample we took                | $\bar{X} = \frac{1}{n}\sum_{i=1}^{n} x_i$                         |
| $s$               | Sample standard deviation     | Spread of the sample we took                 | $s = \sqrt{\frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{X})^2}$         |
| $\hat{p}$ (p-hat) | Sample proportion             | Fraction of sample with a characteristic     | $\hat{p} = \frac{\text{number with characteristic in sample}}{n}$ |

**Key idea**: 
- **Parameters** ($\mu, \sigma, p$) = fixed numbers about the population (usually unknown)
- **Statistics** ($\bar{X}, s, \hat{p}$) = random numbers calculated from our sample (we can compute these)

---

## 5.1 Sampling and Sampling Distributions

### What is a Simple Random Sample?

From your textbook (p. 439):

> A simple random sample is selected such that:
> 1. Every element has **equal probability** of being selected: $P(\text{any element}) = \frac{1}{N}$
> 2. Elements are selected **independently** (for sampling with replacement)

**Example**: Population = {A, B, C, D, E} ($N=5$). We want a sample of size $n=2$.

- Probability A is selected on first draw: $P(A) = \frac{1}{5}$
- If we replace A before second draw: $P(B \text{ on second} \mid A \text{ on first}) = \frac{1}{5}$ (independent)
- If we do NOT replace: $P(B \text{ on second} \mid A \text{ on first}) = \frac{1}{4}$ (dependent, but still a simple random sample)

---

### What is a Sampling Distribution?

**Definition**: The sampling distribution of a statistic (like $\bar{X}$) is the probability distribution of all possible values that statistic can take when we draw ALL possible samples of size $n$ from the population.

**In plain words**: If we could repeat our sampling process infinitely many times, what values would $\bar{X}$ take, and how often?

---

### Example: Sampling Distribution of $\bar{X}$ (From Textbook p. 439-442)

**Population**: 5 employees with salaries (in thousands): $17, 24, 35, 35, 43$

**Step 1: Calculate population parameters**

$$N = 5$$

$$\mu = \frac{17 + 24 + 35 + 35 + 43}{5} = \frac{154}{5} = 30.80$$

$$\sigma^2 = \frac{(17-30.8)^2 + (24-30.8)^2 + 2(35-30.8)^2 + (43-30.8)^2}{5} = 84.16$$

$$\sigma = \sqrt{84.16} = 9.174$$

**Step 2: List all possible samples of size $n=3$ (without replacement)**

Number of possible samples = $C_5^3 = \frac{5!}{3!2!} = 10$

| Sample | Salaries | $\bar{X} = \frac{\sum x_i}{3}$ |
|--------|----------|--------------------------------|
| ABC | 17, 24, 35 | $\frac{76}{3} = 25.33$ |
| ABD | 17, 24, 35 | $\frac{76}{3} = 25.33$ |
| ABE | 17, 24, 43 | $\frac{84}{3} = 28.00$ |
| ACD | 17, 35, 35 | $\frac{87}{3} = 29.00$ |
| ACE | 17, 35, 43 | $\frac{95}{3} = 31.67$ |
| ADE | 17, 35, 43 | $\frac{95}{3} = 31.67$ |
| BCD | 24, 35, 35 | $\frac{94}{3} = 31.33$ |
| BCE | 24, 35, 43 | $\frac{102}{3} = 34.00$ |
| BDE | 24, 35, 43 | $\frac{102}{3} = 34.00$ |
| CDE | 35, 35, 43 | $\frac{113}{3} = 37.67$ |

**Step 3: Build the sampling distribution of $\bar{X}$**

| $\bar{X}$ | Frequency | $P(\bar{X})$ |
|-----------|-----------|--------------|
| 25.33 | 2 | $2/10 = 0.20$ |
| 28.00 | 1 | $1/10 = 0.10$ |
| 29.00 | 1 | $1/10 = 0.10$ |
| 31.33 | 1 | $1/10 = 0.10$ |
| 31.67 | 2 | $2/10 = 0.20$ |
| 34.00 | 2 | $2/10 = 0.20$ |
| 37.67 | 1 | $1/10 = 0.10$ |
| **Total** | **10** | **1.00** |

**Step 4: Calculate mean of the sampling distribution**

$$\mu_{\bar{X}} = E(\bar{X}) = \sum \bar{X} \cdot P(\bar{X})$$

$$= 25.33(0.20) + 28.00(0.10) + 29.00(0.10) + 31.33(0.10) + 31.67(0.20) + 34.00(0.20) + 37.67(0.10)$$

$$= 30.80 = \mu \quad \checkmark$$

**Key Result #1**: The mean of the sampling distribution of $\bar{X}$ equals the population mean.

$$\boxed{\mu_{\bar{X}} = \mu}$$

This means $\bar{X}$ is an **unbiased estimator** of $\mu$.

---

## 5.1.1 Mean and Standard Deviation of $\bar{X}$

### Formula for Standard Deviation of $\bar{X}$ (Standard Error)

$$\boxed{\sigma_{\bar{X}} = \frac{\sigma}{\sqrt{n}} \quad \text{if } \frac{n}{N} \leq 0.05}$$

$$\boxed{\sigma_{\bar{X}} = \frac{\sigma}{\sqrt{n}} \cdot \sqrt{\frac{N-n}{N-1}} \quad \text{if } \frac{n}{N} > 0.05}$$

**What each symbol means**:
- $\sigma_{\bar{X}}$ = standard deviation of the sampling distribution of $\bar{X}$ (called the **standard error**)
- $\sigma$ = population standard deviation
- $n$ = sample size
- $N$ = population size
- $\sqrt{\frac{N-n}{N-1}}$ = **finite population correction factor** (used when sample is large relative to population)

**Why $\sqrt{n}$ in denominator?**  
Because averaging reduces variability. If you average more observations, the result is more stable.

---

### Example: Verify the Formula

From our salary example:
- $\sigma = 9.174$
- $n = 3$
- $N = 5$, so $n/N = 3/5 = 0.60 > 0.05$ → use finite population correction

$$\sigma_{\bar{X}} = \frac{9.174}{\sqrt{3}} \cdot \sqrt{\frac{5-3}{5-1}} = \frac{9.174}{1.732} \cdot \sqrt{0.5} = 5.296 \cdot 0.707 = 3.745$$

From our sampling distribution table, we calculated:
$$\sigma_{\bar{X}} = \sqrt{\sum (\bar{X} - 30.80)^2 \cdot P(\bar{X})} = 3.747 \quad \checkmark$$

(The tiny difference is due to rounding.)

---

## 5.1.2 Central Limit Theorem (CLT)

### Statement (From Textbook p. 445-446)

> Whatever the population, the distribution of $\bar{X}$ is approximately normal when $n$ is large.

**More precisely**: If we take a random sample of size $n$ from ANY population with mean $\mu$ and standard deviation $\sigma$, then when $n$ is large ($n \geq 30$):

$$\bar{X} \overset{\text{approx}}{\sim} N\left(\mu, \frac{\sigma^2}{n}\right)$$

**Standardized form**:
$$\boxed{Z = \frac{\bar{X} - \mu}{\sigma/\sqrt{n}} \sim N(0,1)}$$

**What this means**: Even if the population is skewed, weird, or unknown, the sample mean $\bar{X}$ will be approximately normally distributed if we take a large enough sample.

---

### Example: Using CLT (From Textbook p. 449)

**Given**: Population with $\mu = 75$, $\sigma = 11$. Sample size $n = 64$.

**Find**: $P(73 \leq \bar{X} \leq 78)$

**Step 1: Check condition**
$$n = 64 \geq 30 \quad \checkmark \quad \text{CLT applies}$$

**Step 2: Calculate standard error**
$$\sigma_{\bar{X}} = \frac{\sigma}{\sqrt{n}} = \frac{11}{\sqrt{64}} = \frac{11}{8} = 1.375$$

**Step 3: Convert bounds to Z-scores**
$$Z_{\text{lower}} = \frac{73 - 75}{1.375} = \frac{-2}{1.375} = -1.45$$
$$Z_{\text{upper}} = \frac{78 - 75}{1.375} = \frac{3}{1.375} = 2.18$$

**Step 4: Use standard normal table (Table 2 in Appendix)**
$$P(73 \leq \bar{X} \leq 78) = P(-1.45 \leq Z \leq 2.18)$$
$$= F(2.18) - F(-1.45) = 0.9854 - (1 - 0.9265) = 0.9119$$

**Interpretation**: There is a 91.19% probability that the sample mean of 64 observations falls between 73 and 78.

---

## 5.2 Sampling Distribution of a Sample Proportion

### 5.2.1 Population and Sample Proportions

**Definitions**:

$$\boxed{p = \frac{X}{N}} \quad \text{(Population proportion)}$$
$$\boxed{\hat{p} = \frac{x}{n}} \quad \text{(Sample proportion)}$$

**What each symbol means**:
- $p$ = true proportion in the entire population (unknown parameter)
- $\hat{p}$ = proportion observed in our sample (random statistic)
- $X$ = number of elements with the characteristic in the population
- $x$ = number of elements with the characteristic in the sample
- $N$ = population size
- $n$ = sample size
- $q = 1 - p$ (proportion without the characteristic)

**Example** (From Textbook p. 454):
- City has $N = 393,217$ families
- $X = 123,017$ families own a car
- Population proportion: $p = \frac{123017}{393217} = 0.31$

- Sample of $n = 560$ families
- $x = 215$ own a car
- Sample proportion: $\hat{p} = \frac{215}{560} = 0.38$

---

### 5.2.2 Mean and Standard Deviation of $\hat{p}$

**Formulas**:

$$\boxed{\mu_{\hat{p}} = E(\hat{p}) = p}$$

$$\boxed{\sigma_{\hat{p}} = \sqrt{\frac{p(1-p)}{n}} = \sqrt{\frac{pq}{n}} \quad \text{if } \frac{n}{N} \leq 0.05}$$

$$\boxed{\sigma_{\hat{p}} = \sqrt{\frac{pq}{n}} \cdot \sqrt{\frac{N-n}{N-1}} \quad \text{if } \frac{n}{N} > 0.05}$$


---

### 5.2.3 Form of the Sampling Distribution of $\hat{p}$

**Central Limit Theorem for Proportions**:

If $npq > 9$, then:
$$\hat{p} \overset{\text{approx}}{\sim} N\left(p, \frac{pq}{n}\right)$$

**Standardized form**:
$$\boxed{Z = \frac{\hat{p} - p}{\sqrt{pq/n}} \sim N(0,1)}$$

**Why $npq > 9$?**  
The binomial distribution is skewed when $p$ is near 0 or 1. The condition $npq > 9$ ensures the distribution is symmetric enough for the normal approximation to work well.

---

### Example: Using CLT for Proportions (From Textbook p. 457-459)

**Given**: $p = 0.75$, $n = 210$. Find $P(0.73 \leq \hat{p} \leq 0.80)$

**Step 1: Verify condition**
$$npq = 210 \cdot 0.75 \cdot 0.25 = 39.375 > 9 \quad \checkmark$$

**Step 2: Calculate standard error**
$$\sigma_{\hat{p}} = \sqrt{\frac{0.75 \cdot 0.25}{210}} = \sqrt{0.000893} = 0.0299$$

**Step 3: Convert bounds to Z-scores**
$$Z_{\text{lower}} = \frac{0.73 - 0.75}{0.0299} = -0.67$$
$$Z_{\text{upper}} = \frac{0.80 - 0.75}{0.0299} = 1.67$$

**Step 4: Use standard normal table**
$$P(0.73 \leq \hat{p} \leq 0.80) = P(-0.67 \leq Z \leq 1.67)$$
$$= F(1.67) - F(-0.67) = 0.9525 - (1 - 0.7486) = 0.7011$$

**Interpretation**: There is a 70.11% probability that the sample proportion falls between 0.73 and 0.80.

---

## Summary: All Formulas in One Place

| Statistic | Parameter | Estimator | Mean of Estimator | Standard Error | Condition |
|-----------|-----------|-----------|------------------|----------------|-----------|
| Mean | $\mu$ | $\bar{X}$ | $\mu$ | $\frac{\sigma}{\sqrt{n}}$ | $n \geq 30$ or population normal |
| Proportion | $p$ | $\hat{p}$ | $p$ | $\sqrt{\frac{pq}{n}}$ | $npq > 9$ |

**Golden Rules**:
1. **Unbiasedness**: $E(\bar{X}) = \mu$, $E(\hat{p}) = p$
2. **Standard Error**: Always divide by $\sqrt{n}$ (more data = more precision)
3. **Finite Population Correction**: Only use $\sqrt{\frac{N-n}{N-1}}$ if $n/N > 0.05$
4. **CLT**: Use normal approximation when $n \geq 30$ (for means) or $npq > 9$ (for proportions)
5. **Z-score formula**: Always $Z = \frac{\text{statistic} - \text{parameter}}{\text{standard error}}$

---

## How to Solve Any Problem in This Chapter

$$\text{Step 1: Identify what you're estimating } (\mu \text{ or } p)$$
$$\text{Step 2: Write the estimator } (\bar{X} \text{ or } \hat{p})$$
$$\text{Step 3: Write its mean } (\mu_{\bar{X}} = \mu \text{ or } \mu_{\hat{p}} = p)$$
$$\text{Step 4: Compute standard error } \left(\frac{\sigma}{\sqrt{n}} \text{ or } \sqrt{\frac{pq}{n}}\right)$$
$$\text{Step 5: Check conditions } (n \geq 30 \text{ or } npq > 9)$$
$$\text{Step 6: Form } Z = \frac{\text{observed} - \text{expected}}{SE}$$
$$\text{Step 7: Use standard normal table for probabilities}$$

$$\text{Result: You can solve any sampling distribution problem without memorizing formulas.}$$