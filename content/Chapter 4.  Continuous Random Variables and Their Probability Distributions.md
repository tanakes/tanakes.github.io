## First: What do all these terms mean?

| Term | Meaning (Plain English) | Example |
|------|------------------------|---------|
| **Continuous random variable** | A variable that can take *any* value in a range (not just whole numbers) | Time to finish a task: 3.2 min, 3.25 min, 3.251 min... |
| **Probability density function (PDF)** | A curve that shows how likely different values are; *area under the curve* = probability | Bell curve showing heights of adults |
| **Cumulative distribution function (CDF)** | The probability that X is *less than or equal to* a certain value | P(height ≤ 170 cm) = 0.65 |
| **Normal distribution** | The famous "bell curve" — symmetric, most values cluster around the mean | Test scores, human heights, measurement errors |
| **Standard normal (Z)** | A normal distribution with mean = 0 and standard deviation = 1 | Used as a "universal translator" for all normal problems |
| **Standardizing** | Converting any normal variable to Z by subtracting the mean and dividing by SD | If X ~ N(50, 10), then Z = (X-50)/10 |
| **Exponential distribution** | Models time *between* random events; skewed right, only positive values | Time between customer arrivals, battery life |

---

## 4.1. Introduction

**What's the big idea?**  
In earlier chapters, we dealt with *discrete* variables (like number of heads in coin tosses — you can only get 0, 1, 2...). Now we switch to *continuous* variables — things you measure, not count.

> **Example**: The weight of a bag of rice isn't just "500g or 501g" — it could be 500.001g, 500.0001g, etc. There are *infinitely many* possible values between any two weights.

**Key difference**:  
- Discrete: Probability of a *single value* can be > 0 (e.g., P(X=3) = 0.2)  
- Continuous: Probability of a *single exact value* is **always zero** ✓

> **Example**: What's the probability someone is *exactly* 170.000... cm tall? Essentially zero. But P(169.5 < height < 170.5) could be 0.15 — that makes sense!

---

## 4.2. Areas under continuous probability density functions

For continuous variables, **probability = area under the curve**.

$\boxed{P(a < X < b) = \text{Area under } f(x) \text{ from } a \text{ to } b}$

**Properties of a valid PDF, f(x)**:
1. $f(x) \geq 0$ for all x (curve never goes below x-axis) ✓
2. Total area under curve = 1 (100% probability somewhere) ✓

> **Example**: Suppose a repair time X has PDF:  
> $f(x) = 2x$ for $0 < x < 1$ (and 0 elsewhere)  
> Check: Area = $\int_0^1 2x \, dx = [x^2]_0^1 = 1$ ✓ Valid!

**Comparing Discrete vs. Continuous Probability**:

| Feature | Discrete (e.g., dice) | Continuous (e.g., time) |
|---------|----------------------|------------------------|
| Possible values | Countable list | Any value in interval |
| P(X = exact value) | Can be > 0 | Always = 0 |
| How we find probability | Add up P(x) values | Find area under curve |
| Tool used | Probability table/formula | Integration or tables |

---

## 4.3. The normal distribution

The **normal distribution** is the most important continuous distribution. Its PDF is:

$$\boxed{f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}}$$

But don't panic — you rarely compute this directly! Instead, remember its **shape**:

- Bell-shaped, symmetric about the mean $\mu$
- Spread controlled by standard deviation $\sigma$
- Tails go on forever but get very close to zero

> **Example**: Adult male heights: $\mu = 175$ cm, $\sigma = 7$ cm  
> → Most men are between 168–182 cm ($\mu \pm \sigma$)  
> → Very few are below 154 cm or above 196 cm ($\mu \pm 3\sigma$)

### 4.3.1. Cumulative distribution function (CDF) of the normal

The CDF, $F(x_0) = P(X \leq x_0)$, is the **area under the normal curve to the left of $x_0$**.

> **Example**: If $F(180) = 0.76$ for heights, that means 76% of men are 180 cm or shorter.

**Rule for intervals**:  
$$\boxed{P(a < X < b) = F(b) - F(a)}$$

> **Example**: P(170 < height < 180) = F(180) − F(170) = 0.76 − 0.24 = 0.52 → 52% of men are between 170–180 cm.

---

## 4.4. The standard normal distribution

This is the "reference" normal distribution:

$$\boxed{Z \sim N(0, 1) \quad \text{(mean = 0, SD = 1)}}$$

Why care? Because **all normal problems can be converted to Z**, and we have tables for Z!

**Standard normal table**: Gives $F(z) = P(Z \leq z)$ for positive z.  
Use symmetry for negative z: $P(Z < -z) = 1 - P(Z < z)$ ✓

> **Example**: Find $P(Z < 1.13)$  
> → Look up 1.13 in table → 0.8708  
> → So 87.08% of Z-values are below 1.13.

> **Example**: Find $P(Z > -1.35)$  
> → By symmetry, this = $P(Z < 1.35)$ = 0.9115 ✓

---

## 4.5. Standardizing a normal distribution

This is the **magic step** that lets you use the Z-table for *any* normal variable.

$$\boxed{Z = \frac{X - \mu}{\sigma}}$$

**Steps**:
1. Identify $\mu$ and $\sigma$ of your X
2. Convert your x-value(s) to z-value(s) using the formula
3. Use the Z-table to find probabilities

> **Worked Example (Tiny Numbers!)**:  
> Suppose test scores: $X \sim N(50, 10)$ (mean=50, SD=10)  
> **Question**: What's P(X < 62)?  
>   
> **Step 1**: $\mu = 50$, $\sigma = 10$  
> **Step 2**: $z = \frac{62 - 50}{10} = 1.2$  
> **Step 3**: Look up $P(Z < 1.2)$ in table → 0.8849  
> **Answer**: $\boxed{P(X < 62) = 0.8849}$ ✓  
>   
> **Check**: 62 is 1.2 SDs above mean → makes sense that ~88% are below it.

**Comparing X and Z**:

| Original X            | Standardized Z                 | What changed?                  |
| --------------------- | ------------------------------ | ------------------------------ |
| Mean = $\mu$          | Mean = 0                       | Shifted left by $\mu$          |
| SD = $\sigma$         | SD = 1                         | Scaled by $1/\sigma$           |
| Units: whatever X was | Unitless "standard deviations" | Now comparable across problems |

---

## 4.6. The normal distribution approximation to the binomial distribution

**Definition:** Let $x$ be the number of successes from $n$ independent trials, each with probability of success $p$. Then number of successes, $x$, is a binomial random variable.

**Book's rule for approximation** (follow exactly):

$$\boxed{npq > 9 \quad \text{where } q = 1 - p}$$

If this condition holds, a good approximation is:

$$\boxed{P(a \leq x \leq b) = P\left(\frac{a - np}{\sqrt{npq}} \leq Z \leq \frac{b - np}{\sqrt{npq}}\right)} \quad \text{(4.1)}$$

where $Z$ is a standard normal random variable.

**Continuity correction case:** If $5 < npq < 9$, we can use the continuity correction factor to obtain:
[[Continuity Correction]]

$$\boxed{P(a \leq x \leq b) = P\left(\frac{a - 0.5 - np}{\sqrt{npq}} \leq Z \leq \frac{b + 0.5 - np}{\sqrt{npq}}\right)} \quad \text{(4.2)}$$

> **Example (no continuity correction, npq > 9):**  
> $n = 100$, $p = 0.3$ → $q = 0.7$  
> Check: $npq = 100 \times 0.3 \times 0.7 = 21 > 9$ ✓ Use formula (4.1)  
> Find $P(25 \leq x \leq 35)$:  
> $\mu = np = 30$, $\sigma = \sqrt{npq} = \sqrt{21} \approx 4.58$  
> $z_1 = \frac{25 - 30}{4.58} \approx -1.09$, $z_2 = \frac{35 - 30}{4.58} \approx 1.09$  
> $P(-1.09 \leq Z \leq 1.09) = F(1.09) - F(-1.09) = 0.8621 - 0.1379 = 0.7242$ ✓

> **Example (with continuity correction, 5 < npq < 9):**  
> $n = 30$, $p = 0.4$ → $q = 0.6$  
> Check: $npq = 30 \times 0.4 \times 0.6 = 7.2$ → $5 < 7.2 < 9$ ✓ Use formula (4.2)  
> Find $P(10 \leq x \leq 15)$:  
> $\mu = np = 12$, $\sigma = \sqrt{7.2} \approx 2.68$  
> Apply continuity correction: use $a - 0.5 = 9.5$ and $b + 0.5 = 15.5$  
> $z_1 = \frac{9.5 - 12}{2.68} \approx -0.93$, $z_2 = \frac{15.5 - 12}{2.68} \approx 1.31$  
> $P(-0.93 \leq Z \leq 1.31) = F(1.31) - F(-0.93) = 0.9049 - 0.1762 = 0.7287$ ✓

**When NOT to use normal approximation**:

| Condition | Action |
|-----------|--------|
| $npq \leq 5$ | Use exact binomial formula; normal approximation is not reliable |
| $npq > 9$ | Use formula (4.1) — no continuity correction needed |
| $5 < npq < 9$ | Use formula (4.2) — apply continuity correction (±0.5) |

✓ **Key takeaway**: Always check $npq$ first.

---

## 4.7. The exponential probability distribution

Models **time between random events** (e.g., time between phone calls, machine failures).

**PDF**:  
$$\boxed{f(x) = \lambda e^{-\lambda x} \quad \text{for } x > 0}$$

**Key facts**:
- Only defined for $x \geq 0$ (time can't be negative) ✓
- Mean = $1/\lambda$, Variance = $1/\lambda^2$
- **Memoryless property**: Past waiting time doesn't affect future wait

**Useful probability formulas**:
$$\boxed{P(X > a) = e^{-\lambda a}} \quad \boxed{P(X \leq a) = 1 - e^{-\lambda a}}$$

> **Example**: Calls arrive at average rate $\lambda = 0.5$ per minute (so mean wait = 2 min)  
> **Question**: P(wait > 4 minutes)?  
> → $P(X > 4) = e^{-0.5 \times 4} = e^{-2} \approx 0.1353$  
> → About 13.5% chance you wait more than 4 minutes ✓

**Normal vs. Exponential**:

| Feature | Normal | Exponential |
|---------|--------|-------------|
| Shape | Symmetric bell | Skewed right, starts high, decays |
| Range | $-\infty$ to $+\infty$ | 0 to $+\infty$ only |
| Parameters | $\mu$, $\sigma$ | $\lambda$ (rate) |
| Typical use | Measurements, errors | Waiting times, lifetimes |

---

## Summary: Chapter 4 in One Place

✅ **Continuous variables**: Probability = area under curve; P(exact value) = 0  
✅ **Normal distribution**: Bell curve; use Z = (X−μ)/σ to standardize  
✅ **Z-table**: Gives P(Z ≤ z); use symmetry for negative z  
✅ **Binomial approximation**: Use normal **only if npq > 9**; apply continuity correction (±0.5)  
✅ **Exponential**: Models waiting times; P(X > a) = e^(−λa); mean = 1/λ  
✅ **Always check assumptions** before applying formulas ✓

---

## How to Solve / Understand Any Problem in This Topic

1. **Identify the variable type**:  
   → Counting things? → Discrete (binomial/Poisson)  
   → Measuring things? → Continuous (normal/exponential)

2. **If normal**:  
   → Write down $\mu$ and $\sigma$  
   → Convert x to z: $\boxed{z = \frac{x - \mu}{\sigma}}$  
   → Use Z-table; apply symmetry if z is negative  
   → For intervals: $P(a<X<b) = F(b) - F(a)$

3. **If approximating binomial with normal**:  
   → **First check**: $\boxed{npq > 9}$ (book rule!)  
   → Compute $\mu = np$, $\sigma = \sqrt{npq}$  
   → Apply **continuity correction**: add/subtract 0.5 to discrete x-values  
   → Standardize and use Z-table

4. **If exponential**:  
   → Identify rate $\lambda$ (events per unit time)  
   → Use $P(X > a) = e^{-\lambda a}$ or $P(X \leq a) = 1 - e^{-\lambda a}$  
   → Remember: mean waiting time = $1/\lambda$

5. **Always verify**:  
   ✓ Does the answer make sense? (e.g., probability between 0 and 1)  
   ✓ Did I use the right tail? (draw a sketch!)  
   ✓ For approximations: was the condition satisfied?

**Pro tip**: Sketch the curve and shade the area you want — it prevents 80% of mistakes! 🎯