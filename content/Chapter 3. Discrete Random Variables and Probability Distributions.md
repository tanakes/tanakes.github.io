## First: What do all these terms mean?

| Term                           | Meaning                                                                              | Example                                                                   |
| ------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------- |
| **Random Variable (X)**        | A number whose value depends on the outcome of a random experiment                   | Number of heads when flipping a coin 3 times                              |
| **Discrete Random Variable**   | A random variable that can only take specific, countable values (like 0, 1, 2, 3...) | Number of customers in a store (you can't have 2.5 customers)             |
| **Probability Distribution**   | A list/table showing each possible value of X and its probability                    | P(X=0)=0.125, P(X=1)=0.375, P(X=2)=0.375, P(X=3)=0.125                    |
| **Expected Value (μ or E[X])** | The long-run average value you'd expect if you repeated the experiment many times    | If you flip 3 coins many times, average heads ≈ 1.5                       |
| **Variance (σ²)**              | Measures how spread out the values are from the mean                                 | Tells you if outcomes cluster near the mean or scatter widely             |
| **Binomial Distribution**      | Models number of successes in n independent trials, each with success probability p  | Number of defective items in a batch of 20, where each has 5% defect rate |
| **Poisson Distribution**       | Models number of events occurring in a fixed interval of time/space                  | Number of phone calls received per hour at a call center                  |

---

## 3.1 Random Variables: The Starting Point

**What is a random variable?** Think of it as a "number machine" that gives you a numerical result after a random event happens.

> **Example:** You roll a die. The random variable X = "the number that appears". X can be 1, 2, 3, 4, 5, or 6. Each outcome is random, but once the die lands, X has a definite value.

**Discrete vs. Continuous:**

|Type|Can take...|Example|
|---|---|---|
|**Discrete**|Countable, separate values (like whole numbers)|Number of emails you receive today: 0, 1, 2, 3...|
|**Continuous**|Any value in an interval (like decimals)|Time to finish a test: 45.3 minutes, 45.31 minutes, etc.|

✓ **Key takeaway:** Chapter 3 only deals with **discrete** random variables—things you can count.

---

## 3.2 Probability Distributions for Discrete Random Variables

A probability distribution tells you: "If X can be these values, how likely is each one?"

**Two rules every probability distribution must follow:**

$$\boxed{
\begin{aligned}
&\text{1. } 0 \leq P(x) \leq 1 \quad \text{(each probability is between 0 and 1)} \\
&\text{2. } \sum P(x) = 1 \quad \text{(all probabilities add up to 1)}
\end{aligned}
}$$

> **Example:** Flip a fair coin 2 times. Let X = number of heads.
> 
> Possible outcomes: HH, HT, TH, TT
> - X=0 (TT): P=1/4 = 0.25
> - X=1 (HT or TH): P=2/4 = 0.50
> - X=2 (HH): P=1/4 = 0.25
> 
> ✓ Check: 0.25 + 0.50 + 0.25 = 1 ✓

**Cumulative Probability Function F(x₀):** The probability that X is *less than or equal to* a certain value.

> **Example (same coin flip):** F(1) = P(X ≤ 1) = P(X=0) + P(X=1) = 0.25 + 0.50 = 0.75  
> This means: "There's a 75% chance of getting 1 or fewer heads."

---

## 3.3 Expected Value and Variance: Summarizing the Distribution

### 3.3.1 Expected Value (The "Long-Run Average")

$$\boxed{
\mu = E[X] = \sum x \cdot P(x)
}$$

> **Example:** A game pays you: $0 with probability 0.5, $2 with probability 0.3, $5 with probability 0.2.  
> Expected value = (0)(0.5) + (2)(0.3) + (5)(0.2) = 0 + 0.6 + 1.0 = **$1.60**  
> ✓ Interpretation: If you play this game many times, you'll average $1.60 per game.

### 3.3.2 Variance and Standard Deviation (How "Spread Out" Are the Values?)

$$\boxed{
\sigma^2 = \sum (x - \mu)^2 \cdot P(x) \quad \text{or (shortcut)} \quad \sigma^2 = \sum x^2 \cdot P(x) - \mu^2
}$$

$$\boxed{
\sigma = \sqrt{\sigma^2}
}$$

> **Example (same game):** μ = 1.60  
> Using shortcut:  
> ∑x²·P(x) = (0²)(0.5) + (2²)(0.3) + (5²)(0.2) = 0 + 1.2 + 5.0 = 6.2  
> σ² = 6.2 − (1.60)² = 6.2 − 2.56 = 3.64  
> σ = √3.64 ≈ **1.91**  
> ✓ Interpretation: Typical winnings vary by about $1.91 from the $1.60 average.

### 3.3.3 Linear Functions: What If We Transform X?

If Y = a + bX, then:

$$\boxed{
\begin{aligned}
E[Y] &= a + b \cdot E[X] \\
Var(Y) &= b^2 \cdot Var(X) \\
\sigma_Y &= \sqrt{\mathrm{Var}(Y)} =|b| \cdot \sigma_X
\end{aligned}
}$$

> **Example:** Your bonus is $100 + $50 × (number of sales). If expected sales = 3, variance of sales = 4:  
> Expected bonus = 100 + 50(3) = **$250**  
> Variance of bonus = 50² × 4 = 2500 × 4 = **10,000**  
> Standard deviation = √10,000 = **$100**

---

## 3.4 Jointly Distributed Discrete Random Variables (Two Variables at Once)

Here's a simplified example table for X = number of tests, Y = number of snacks:

|                     | **X=0**  | **X=1**  | **X=2**  | **P(Y)** (marginal) |
| ------------------- | -------- | -------- | -------- | ------------------- |
| **Y=0**             | 0.05     | 0.08     | 0.09     | **0.22**            |
| **Y=1**             | 0.07     | 0.09     | 0.11     | **0.27**            |
| **Y=2**             | 0.09     | 0.04     | 0.10     | **0.25**            |
| **Y=3**             | 0.07     | 0.11     | 0.08     | **0.26**            |
| **P(X)** (marginal) | **0.31** | **0.28** | **0.41** | **1.00**            |

✓ Each cell = P(X=x, Y=y) — the joint probability  
✓ Row totals = marginal P(Y=y) — sum across each row  
✓ Column totals = marginal P(X=x) — sum down each column  
✓ All cells sum to 1 ✓

> **Example:** P(2 tests AND 3 snacks) = 0.08 (look at row Y=3, column X=2)  
> **Example:** P(1 test) = 0.28 (sum down the X=1 column: 0.08+0.09+0.04+0.11)

### How to Find Mean (Expected Value) for X and Y

**Step 1: Get the marginal probabilities** (already in the table margins!)  
- For X: P(X=0)=0.31, P(X=1)=0.28, P(X=2)=0.41  
- For Y: P(Y=0)=0.22, P(Y=1)=0.27, P(Y=2)=0.25, P(Y=3)=0.26

**Step 2: Apply the expected value formula**

$$\boxed{
E[X] = \sum_{\text{all } x} x \cdot P_X(x) \quad \quad E[Y] = \sum_{\text{all } y} y \cdot P_Y(y)
}$$

> **Concrete example for X:**  
> E[X] = (0)(0.31) + (1)(0.28) + (2)(0.41) = 0 + 0.28 + 0.82 = **1.10**  
> ✓ Interpretation: On average, a student has 1.10 tests per day.

> **Concrete example for Y:**  
> E[Y] = (0)(0.22) + (1)(0.27) + (2)(0.25) + (3)(0.26) = 0 + 0.27 + 0.50 + 0.78 = **1.55**  
> ✓ Interpretation: On average, a student eats 1.55 snacks per day.

### How to Find Variance for X and Y

Use the **shortcut formula** (easier than computing (x−μ)² every time):

$$\boxed{
Var(X) = \sum_{\text{all } x} x^2 \cdot P_X(x) \;-\; [E(X)]^2
}$$

$$\boxed{
\sigma_X = \sqrt{Var(X)} \quad \text{(standard deviation)}
}$$

> **Worked example for X** (marginals: P(0)=0.31, P(1)=0.28, P(2)=0.41; E[X]=1.10):  
> 
> Step 1: Compute Σx²·P(x)  
> = (0²)(0.31) + (1²)(0.28) + (2²)(0.41)  
> = 0 + 0.28 + 1.64 = **1.92**  
> 
> Step 2: Subtract [E(X)]²  
> Var(X) = 1.92 − (1.10)² = 1.92 − 1.21 = **0.71**  
> 
> Step 3: Standard deviation  
> σₓ = √0.71 ≈ **0.84**  
> 
> ✓ Interpretation: Typical values of X vary by about ±0.84 from the mean of 1.10.

> **Do the same for Y** using its marginal probabilities ✓

---

### Conditional Probability: "Given That..."

$$\boxed{
P(Y=y \mid X=x) = \frac{P(X=x, Y=y)}{P(X=x)}
}$$

> **Example:** P(3 snacks \| 1 test) = P(1 test AND 3 snacks) / P(1 test) = 0.11 / 0.28 ≈ **0.393**  
> ✓ Meaning: Given a student has 1 test, there's a 39.3% chance they eat 3 snacks.

> **Example:** P(2 tests \| 2 snacks) = P(2 tests AND 2 snacks) / P(2 snacks) = 0.10 / 0.25 = **0.40**  
> ✓ Meaning: Given a student eats 2 snacks, there's a 40% chance they have 2 tests.

---

### Independence Check: Do X and Y Affect Each Other?

$$\boxed{
X \text{ and } Y \text{ are independent if } P(X=x, Y=y) = P(X=x) \cdot P(Y=y) \text{ for ALL } x,y
}$$

| Result | Interpretation |
|--------|---------------|
| **Equal for all cells** | X and Y are independent — knowing one tells you nothing about the other |
| **Not equal for any cell** | X and Y are dependent — they're related somehow |

> **Example:** Check if X=1 and Y=2 are independent:  
> P(X=1, Y=2) = 0.04 (from table)  
> P(X=1)·P(Y=2) = 0.28 × 0.25 = 0.07  
> 0.04 ≠ 0.07 → **Not independent** ✓  
> **Bold takeaway**: You only need ONE cell that fails the test to conclude dependence.

---

### Covariance: Do X and Y Move Together?
[[Covariance Explained Simply]]
$$\boxed{
Cov(X,Y) = \sum\sum (x - \mu_X)(y - \mu_Y) \cdot P(x,y)
}$$

**Shortcut formula** (easier for calculations):

$$\boxed{
Cov(X,Y) = \sum\sum x y \cdot P(x,y) \;-\; E[X] \cdot E[Y]
}$$

| Cov(X,Y) | Interpretation |
|----------|---------------|
| **> 0** | When X is high, Y tends to be high (direct relationship) |
| **< 0** | When X is high, Y tends to be low (inverse relationship) |
| **≈ 0** | No *linear* relationship (but could still be nonlinear!) |

> **Tiny example using our table:**  
> First compute ΣΣ xy·P(x,y):  
> = (0·0)(0.05) + (0·1)(0.07) + ... + (2·3)(0.08) = **1.66** (after summing all 12 cells)  
> Then: Cov = 1.66 − E[X]·E[Y] = 1.66 − (1.10)(1.55) = 1.66 − 1.705 = **−0.045**  
> ✓ Interpretation: Weak negative association — more tests slightly linked to fewer snacks.

---

### Correlation: The "Standardized" Covariance

$$\boxed{
\rho_{XY} = \frac{Cov(X,Y)}{\sigma_X \cdot \sigma_Y}
}$$

| ρ value | Strength |
|---------|----------|
| \|ρ\| ≥ 0.7 | **Strong** |
| 0.4 ≤ \|ρ\| < 0.7 | **Moderate** |
| \|ρ\| < 0.4 | **Weak** |
| ρ = ±1 | Perfect linear relationship |
| ρ = 0 | No *linear* relationship |

> **From our example:** If σₓ=0.84, σᵧ=1.05, then  
> ρ = −0.045 / (0.84 × 1.05) ≈ **−0.05** → very weak negative correlation ✓  
> **Bold takeaway**: Correlation is unitless and always between −1 and +1 — perfect for comparing relationships.


### 🔧 FULL WORKED EXAMPLE: Mean, Variance & Covariance from a Joint Table

**Scenario**: A survey records:  
- X = number of online courses (0, 1, 2)  
- Y = number of study groups joined (0, 1)  

Joint probabilities:

| | X=0 | X=1 | X=2 | **P(Y)** |
|---|-----|-----|-----|----------|
| **Y=0** | 0.10 | 0.15 | 0.05 | **0.30** |
| **Y=1** | 0.20 | 0.30 | 0.20 | **0.70** |
| **P(X)** | **0.30** | **0.45** | **0.25** | **1.00** |

**Find**: E[X], Var(X), E[Y], Var(Y), Cov(X,Y), ρ

### Step 1: Marginals ✓ (already in table margins)

### Step 2: E[X] and E[Y]
- E[X] = 0(0.30) + 1(0.45) + 2(0.25) = 0 + 0.45 + 0.50 = **0.95**
- E[Y] = 0(0.30) + 1(0.70) = **0.70**

### Step 3: Var(X) and Var(Y)
- Σx²·P(x) = 0²(0.30) + 1²(0.45) + 2²(0.25) = 0 + 0.45 + 1.00 = 1.45  
  Var(X) = 1.45 − (0.95)² = 1.45 − 0.9025 = **0.5475**  
  σₓ = √0.5475 ≈ **0.740**

- Σy²·P(y) = 0²(0.30) + 1²(0.70) = 0.70  
  Var(Y) = 0.70 − (0.70)² = 0.70 − 0.49 = **0.21**  
  σᵧ = √0.21 ≈ **0.458**

### Step 4: Cov(X,Y)
Compute ΣΣ xy·P(x,y):  
= (0·0)(0.10) + (0·1)(0.20) + (1·0)(0.15) + (1·1)(0.30) + (2·0)(0.05) + (2·1)(0.20)  
= 0 + 0 + 0 + 0.30 + 0 + 0.40 = **0.70**  
Cov = 0.70 − E[X]·E[Y] = 0.70 − (0.95)(0.70) = 0.70 − 0.665 = **+0.035**

### Step 5: Correlation
ρ = Cov / (σₓ·σᵧ) = 0.035 / (0.740 × 0.458) ≈ 0.035 / 0.339 ≈ **0.103**  
✓ Interpretation: Very weak positive relationship — taking more online courses slightly linked to joining more study groups.

---

## 3.5 The Binomial Distribution: Counting Successes

A **binomial experiment** has 4 conditions:
1. Fixed number of trials (n)
2. Only two outcomes per trial: Success/Failure
3. Probability of success (p) is constant
4. Trials are independent

$$\boxed{
P(X = x) = \binom{n}{x} p^x (1-p)^{n-x} \quad \text{where } q = 1-p
}$$

> **Example:** A drug works 30% of the time (p=0.3). Given to 4 patients (n=4). What's P(exactly 3 work)?  
> P(X=3) = C(4,3) × (0.3)³ × (0.7)¹ = 4 × 0.027 × 0.7 = **0.0756** ✓

### Mean and Standard Deviation for Binomial

$$\boxed{
\mu = np \quad \quad \sigma = \sqrt{npq} \quad \text{where } q = 1-p
}$$

> **Example:** n=100 shots, p=0.3 chance of hit:  
> μ = 100×0.3 = **30 hits** (expected)  
> σ = √(100×0.3×0.7) = √21 ≈ **4.58** ✓

---

## 3.6 The Hypergeometric Distribution: Sampling WITHOUT Replacement

Use this when you sample from a small population *without putting items back* (so probabilities change).

$$\boxed{
P(X = x) = \frac{\binom{S}{x} \binom{N-S}{n-x}}{\binom{N}{n}}
}$$

Where:
- N = total population size
- S = number of "successes" in population
- n = sample size
- x = successes in sample

> **Example:** 12 managers: 7 female (S=7), 5 male. Pick 3 at random (n=3). P(all 3 female)?  
> P(X=3) = [C(7,3) × C(5,0)] / C(12,3) = (35 × 1) / 220 = **0.1591** ✓

---

## 3.7 The Poisson Distribution: Events Over Time/Space

Use when counting rare events in a fixed interval (time, area, volume), where events happen randomly and independently.

$$\boxed{
P(X = x) = \frac{e^{-\lambda} \lambda^x}{x!} \quad \text{where } \lambda = \text{average rate}
}$$

$$\boxed{
\mu = \lambda \quad \quad \sigma^2 = \lambda
}$$

> **Example:** A computer breaks down λ=3 times/month on average. P(exactly 4 breakdowns next month)?  
   P(X=4) = e⁻³ × 3⁴ / 4! = 0.049787 × 81 / 24 ≈ **0.168** ✓


---

## 📋 Summary: Chapter 3 at a Glance

| Concept                      | Key Formula                                                        | When to Use                                   |
| ---------------------------- | ------------------------------------------------------------------ | --------------------------------------------- |
| **Discrete RV**              | X takes countable values                                           | Counting things: people, defects, calls       |
| **Probability Distribution** | ∑P(x)=1, 0≤P(x)≤1                                                  | Listing all possible outcomes & chances       |
| **Expected Value**           | $\boxed{\mu = \sum x \cdot P(x)}$                                  | Long-run average prediction                   |
| **Variance**                 | $\boxed{\sigma^2 = \sum x^2 P(x) - \mu^2}$                         | Measuring spread/uncertainty                  |
| **Binomial**                 | $\boxed{P(x) = \binom{n}{x} p^x q^{n-x}}$                          | Fixed trials, constant p, independent         |
| **Hypergeometric**           | $\boxed{P(x) = \frac{\binom{S}{x}\binom{N-S}{n-x}}{\binom{N}{n}}}$ | Sampling WITHOUT replacement from small N     |
| **Poisson**                  | $\boxed{P(x) = \frac{e^{-\lambda}\lambda^x}{x!}}$                  | Rare events over time/space, λ = average rate |

**Key Rules from Your Book:**
✓ For normal approximation to binomial: use **npq > 9** (not np>10 & nq>10)  
✓ Always check: probabilities sum to 1, each P(x) between 0 and 1  
✓ For independence: P(X,Y) must equal P(X)·P(Y) for ALL combinations

---

## 🎯 How to Solve / Understand Any Problem in This Topic

1. **Identify the random variable**: What are you counting or measuring? Is it discrete? ✓
2. **Determine the distribution type**:
   - Counting successes in fixed independent trials? → **Binomial**
   - Sampling without replacement from small group? → **Hypergeometric**
   - Counting rare events over time/space? → **Poisson**
   - Just given a table of values? → Use **general discrete formulas**
3. **Write down known values**: n, p, λ, x, etc.
4. **Select the correct formula** from the boxes above ✓
5. **Plug in numbers carefully** — watch exponents and factorials!
6. **Check your answer**:
   - Is probability between 0 and 1? ✓
   - Does it make intuitive sense? (e.g., P(X=10) when p=0.01 should be tiny)
7. **For expected value/variance**: Use the shortcut formula if calculations get messy
8. **For two variables**: Build a joint table first, then compute marginals/conditionals

**Pro Tips:**
- **Bold takeaway**: Always define what "success" means in binomial problems — it's just a label, not necessarily "good"!
- **Bold takeaway**: Poisson λ must match your time/space unit (e.g., if λ=3 per month, don't use it for weekly calculations without adjusting)
- ✓ Verify npq > 9 before using normal approximation to binomial (per your book's rule)
- ✓ When in doubt, sketch a tiny probability table — it clarifies everything

You've got this! Chapter 3 is about turning uncertainty into numbers you can work with. Start simple, check each step, and the patterns will become clear. 🚀