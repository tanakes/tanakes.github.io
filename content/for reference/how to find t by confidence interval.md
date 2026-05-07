# How to Find the t-Value for 95% Confidence

## First: What do all these terms mean?

| Term | Meaning | Example |
|------|---------|---------|
| **Confidence Level** | How sure we want to be that our interval contains the true value | 95% confidence = we want to be 95% certain |
| **α (alpha)** | The "error rate" = 1 − confidence level | For 95%: α = 1 − 0.95 = 0.05 |
| **α/2** | Half of alpha, used for two-tailed intervals | For 95%: α/2 = 0.025 |
| **Degrees of Freedom (df)** | Sample size minus 1: df = n − 1 | If n = 10, then df = 9 |
| **t-value** | The critical value from the t-table that scales our margin of error | For df = 9, 95% confidence: t ≈ 2.262 |

---

## Step-by-Step: How to Find t for 95%

### 🔹 Step 1: Convert confidence level to α
$\boxed{\alpha = 1 - \text{confidence level}}$

For 95% confidence:
- α = 1 − 0.95 = **0.05**
- α/2 = 0.05 ÷ 2 = **0.025** ✓ (we use α/2 because confidence intervals are two-tailed)

### 🔹 Step 2: Find your degrees of freedom
$\boxed{df = n - 1}$

**Concrete example**: If your sample has n = 10 observations:
- df = 10 − 1 = **9**

### 🔹 Step 3: Use the t-table (Table 4 in Aliyev's Appendix)

Look at the t-table with:
- **Column**: α = 0.025 (for 95% confidence)
- **Row**: your df value

| df (ν) | α = 0.10 | α = 0.05 | **α = 0.025** ← use this for 95% CI | α = 0.01 | α = 0.005 |
|--------|----------|----------|-------------------------------------|----------|-----------|
| ... | ... | ... | ... | ... | ... |
| **9** | 1.383 | 1.833 | **2.262** ← your t-value! | 2.821 | 3.250 |
| ... | ... | ... | ... | ... | ... |

✓ **Answer**: For 95% confidence and df = 9, **t = 2.262**

---

## 🔹 Quick Reference: Common t-values for 95% Confidence

| Sample Size (n) | Degrees of Freedom (df) | t-value (α/2 = 0.025) |
|-----------------|------------------------|----------------------|
| 5 | 4 | 2.776 |
| 10 | 9 | 2.262 |
| 15 | 14 | 2.145 |
| 20 | 19 | 2.093 |
| 25 | 24 | 2.064 |
| 30 | 29 | 2.045 |
| ∞ (large sample) | ∞ | **1.960** ← this is the z-value! |

**Bold takeaway**: ✓ As sample size increases, the t-value gets closer to 1.96 (the z-value for 95% confidence).

---

## 🔹 Worked Example from Start to Finish

**Scenario**: You have a sample of n = 16 students. You want a 95% confidence interval for the mean test score. Sample mean = 78, sample standard deviation s = 12.

**Step 1**: Find α and α/2
- α = 1 − 0.95 = 0.05
- α/2 = 0.025 ✓

**Step 2**: Find degrees of freedom
- df = n − 1 = 16 − 1 = **15** ✓

**Step 3**: Look up t in Table 4
- Row: df = 15
- Column: α = 0.025
- **t = 2.131** ✓

**Step 4**: Use t in the confidence interval formula
$$\boxed{\bar{x} \pm t \cdot \frac{s}{\sqrt{n}}}$$

- Standard error = s/√n = 12/√16 = 12/4 = 3
- Margin of error = t × SE = 2.131 × 3 = 6.393
- Confidence interval = 78 ± 6.393 → **(71.607, 84.393)** ✓

**Interpretation**: We are 95% confident the true mean test score is between 71.6 and 84.4.

---

## 🔹 Common Mistakes vs. Correct Approach

| Mistake | Why It's Wrong | Correct Approach |
|---------|---------------|-----------------|
| Using α = 0.05 column for 95% CI | That's for one-tailed tests! | Use α/2 = 0.025 column for two-tailed CI |
| Forgetting df = n − 1 | df determines which row to use | Always calculate df first |
| Using z = 1.96 for small samples | z is only valid when n ≥ 30 or σ known | Use t-table when n < 30 and σ unknown |
| Reading the wrong row | Each df has a different t-value | Match your exact df to the table |

---

## 📋 Summary: Finding t for 95% Confidence

1. **Confidence level = 95%** → α = 0.05 → **α/2 = 0.025**
2. **Calculate df** → df = n − 1
3. **Open t-table** (Table 4 in Aliyev)
4. **Find intersection** of row = df and column = 0.025
5. **That number is your t-value** ✓

**Bold takeaways**:
✓ **Always use α/2 (not α) for confidence intervals** — they're two-tailed.
✓ **Degrees of freedom matter** — smaller samples need larger t-values.
✓ **When n ≥ 30**, t ≈ 1.96, so you can use the z-table as an approximation.

---

## 🛠️ Quick Checklist: "Do I Have the Right t-Value?"

- [ ] Did I convert 95% → α = 0.05 → α/2 = 0.025? ✓
- [ ] Did I calculate df = n − 1 correctly? ✓
- [ ] Did I use the **0.025 column** (not 0.05) in the t-table? ✓
- [ ] Did I match my df to the correct row? ✓
- [ ] Is my t-value larger than 1.96? (It should be, if n < 30) ✓

**Final checkmark**: ✓ If you can find t = 2.262 for df = 9 in Table 4, you've mastered it!