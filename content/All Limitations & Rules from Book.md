# 📋 Complete Reference: All Limitations & Rules from Your Statistics Book

*Organized by topic so you never confuse them again!*

---

## 🔢 BINOMIAL → NORMAL APPROXIMATION (Section 4.6)

| Condition               | Rule                      | If TRUE → Do This                                                                                                               | If FALSE → Do This                                        |
| ----------------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| **Case 1: npq > 9**     | `npq > 9` where `q = 1-p` | ✅ Use normal approximation **WITHOUT** continuity correction:  <br>`P(a ≤ x ≤ b) ≈ P( (a-np)/√(npq) ≤ Z ≤ (b-np)/√(npq) )`      | ❌ Go to next check                                        |
| **Case 2: 5 < npq ≤ 9** | `5 < npq ≤ 9`             | ✅ Use normal approximation **WITH** continuity correction:  <br>`P(a ≤ x ≤ b) ≈ P( (a-0.5-np)/√(npq) ≤ Z ≤ (b+0.5-np)/√(npq) )` | ❌ Go to next check                                        |
| **Case 3: npq ≤ 5**     | `npq ≤ 5`                 | ❌ **Do NOT use** normal approximation                                                                                           | ✅ Use **exact binomial formula**: `P(x) = C(n,x)·pˣ·qⁿ⁻ˣ` |
[[Continuity Correction]]

> 🎯 **Book's exact formulas (4.1 & 4.2)**:
Case 1 (npq > 9):
P(a ≤ x ≤ b) ≈ P( (a-np)/√(npq) ≤ Z ≤ (b-np)/√(npq) )  ← NO ±0.5                                               
Case 2 (5 < npq ≤ 9):
P(a ≤ x ≤ b) ≈ P( (a-0.5-np)/√(npq) ≤ Z ≤ (b+0.5-np)/√(npq) )  ← WITH ±0.5                               
Case 3 (npq ≤ 5):
Use exact: P(x) = C(n,x)·pˣ·qⁿ⁻ˣ

---

## 🗃️ FINITE POPULATION CORRECTION (Section 5.1.1)

| Condition                               | Rule                                     | Standard Error Formula                                                                                                                                          |
| --------------------------------------- | ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Small sample relative to population** | `n/N ≤ 0.05` (sample ≤ 5% of population) | $\sigma_{\bar{X}} = \frac{\sigma}{\sqrt{n}}$,  <br>$\sigma_{\hat{p}} = \sqrt{\frac{pq}{n}}$                                                                     |
| **Large sample relative to population** | `n/N > 0.05` (sample > 5% of population) | $\sigma_{\bar{X}} = \frac{\sigma}{\sqrt{n}} \times \sqrt{\frac{N - n}{N - 1}}$,  <br>$\sigma_{\hat{p}} = \sqrt{\frac{pq}{n}} \times \sqrt{\frac{N - n}{N - 1}}$ |

> 🔑 The term $\sqrt{\frac{N-n}{N-1}}$ is called the **finite population correction factor**.

---

## 📊 CENTRAL LIMIT THEOREM & SAMPLE SIZE (Section 5.1.2, 6)

| Situation                                | Rule                                  | Sampling Distribution of X̄                               | What to Use                                            |
| ---------------------------------------- | ------------------------------------- | --------------------------------------------------------- | ------------------------------------------------------ |
| **Large sample**                         | `n ≥ 30`                              | ✅ Approximately normal **regardless of population shape** | Z-distribution (if σ known) or Z with s (if σ unknown) |
| **Small sample + normal population**     | `n < 30` AND population is normal     | ✅ Exactly normal                                          | t-distribution with `df = n-1` (if σ unknown)          |
| **Small sample + non-normal population** | `n < 30` AND population is NOT normal | ❌ **Not guaranteed** to be normal                         | Use non-parametric methods or collect more data        |

> ⚠️ **Critical**: The `n ≥ 30` rule is for the **sampling distribution of the mean**, NOT for individual data!

---

## 📈 SAMPLE PROPORTION NORMAL APPROXIMATION (Section 5.2.3)

| Condition                       | Rule      | If TRUE → Do This                         | If FALSE → Do This                                                         |
| ------------------------------- | --------- | ----------------------------------------- | -------------------------------------------------------------------------- |
| **Normal approximation for p̂** | `npq > 9` | ✅ p̂ ≈ Normal with `μ = p`, `σ = √(pq/n)` | ❌ Cannot use normal-based confidence intervals; use exact binomial methods |

> 📝 **Z-score for proportion**: `Z = (p̂ - p) / √(pq/n)`

---

## 🎯 CONFIDENCE INTERVALS: WHICH FORMULA? (Chapter 6)

### For Population Mean μ:

| σ Known? | Sample Size | Population Shape | Formula to Use                              |
| -------- | ----------- | ---------------- | ------------------------------------------- |
| ✅ Yes    | Any n       | Normal           | `x̄ ± z_(α/2) · σ/√n`                       |
| ✅ Yes    | n ≥ 30      | Any              | `x̄ ± z_(α/2) · σ/√n` (CLT)                 |
| ❌ No     | n ≥ 30      | Any              | `x̄ ± z_(α/2) · s/√n` (large sample approx) |
| ❌ No     | n < 30      | **Normal**       | `x̄ ± t_(α/2, n-1) · s/√n`                  |
| ❌ No     | n < 30      | **Not normal**   | ❌ Cannot use standard methods               |

### For Population Proportion p:

| Condition | Formula |
|-----------|---------|
| `np̂q̂ > 9` AND large sample | `p̂ ± z_(α/2) · √(p̂q̂/n)` |

### For Difference of Two Means (Independent Samples):

| Variances Known? | Sample Sizes | Formula |
|-----------------|-------------|---------|
| Both σ₁, σ₂ known | Any | `(x̄₁ - x̄₂) ± z_(α/2) · √(σ₁²/n₁ + σ₂²/n₂)` |
| Unknown but **equal** | Any (but prefer n₁+n₂-2 ≥ 30) | `(x̄₁ - x̄₂) ± t_(α/2, df) · s_p·√(1/n₁ + 1/n₂)` <br> where `s_p² = [(n₁-1)s₁² + (n₂-1)s₂²]/(n₁+n₂-2)` |
| Unknown & **unequal** | Both n₁, n₂ ≥ 30 | `(x̄₁ - x̄₂) ± z_(α/2) · √(s₁²/n₁ + s₂²/n₂)` |

### For Difference of Two Proportions:

| Condition | Formula |
|-----------|---------|
| `n₁p̂₁q̂₁ > 9` AND `n₂p̂₂q̂₂ > 9` | `(p̂₁ - p̂₂) ± z_(α/2) · √(p̂₁q̂₁/n₁ + p̂₂q̂₂/n₂)` |

---

## 📐 CHI-SQUARE FOR VARIANCE (Section 5.2 & 6.10)

| Requirement | Rule |
|------------|------|
| **Population distribution** | ✅ **Must be normal** — no sample size exception! |
| **Confidence interval for σ²** | `( (n-1)s² / χ²_(α/2) , (n-1)s² / χ²_(1-α/2) )` |
| **Degrees of freedom** | `df = n - 1` |

> ⚠️ **Warning**: If population isn't normal, chi-square methods for variance are **not reliable**, even with large n.


---

## 🧭 DECISION FLOWCHART: "Which Rule Do I Use?"

```
START: What are you estimating?
│
├─► Mean (μ)?
│   │
│   ├─► Is σ known?
│   │   ├─► YES → Use Z: x̄ ± z·σ/√n
│   │   └─► NO → Is n ≥ 30?
│   │       ├─► YES → Use Z with s: x̄ ± z·s/√n
│   │       └─► NO → Is population normal?
│   │           ├─► YES → Use t: x̄ ± t·s/√n (df = n-1)
│   │           └─► NO → ❌ Cannot use standard methods
│
├─► Proportion (p)?
│   │
│   ├─► Check: npq > 9?
│   │   ├─► YES → Use: p̂ ± z·√(p̂q̂/n)
│   │   └─► NO → ❌ Use exact binomial methods
│
├─► Variance (σ²)?
│   │
│   ├─► Is population normal?
│   │   ├─► YES → Use chi-square with df = n-1
│   │   └─► NO → ❌ Methods not reliable
│
└─► Difference of means/proportions?
    │
    ├─► Check conditions for EACH sample first
    └─► Then apply two-sample formulas above
```

---

## 🚨 COMMON MISTAKES TO AVOID

| Mistake | Correct Approach |
|---------|-----------------|
| Using `np > 10 & nq > 10` when book says `npq > 9` | ✅ **Follow book**: `npq > 9` |
| Forgetting ±0.5 continuity correction for binomial → normal | ✅ **Always add/subtract 0.5** when approximating discrete with continuous |
| Using Z when σ unknown and n < 30 | ✅ Use **t-distribution** with df = n-1 |
| Applying CLT (n ≥ 30) to variance/chi-square problems | ✅ Chi-square for variance **requires normal population**, no n exception |
| Ignoring finite population correction when n/N > 0.05 | ✅ Multiply SE by `√((N-n)/(N-1))` |
| Using sample proportion p̂ in place of p in standard error formula for CI | ✅ For CI: use `√(p̂q̂/n)`; for hypothesis testing with H₀: p = p₀, use `√(p₀q₀/n)` |

---

## 📌 ONE-PAGE CHEAT SHEET

```
✅ BINOMIAL → NORMAL: npq > 9 → use μ=np, σ=√(npq) + ±0.5 correction
✅ CLT for MEAN: n ≥ 30 → X̄ ≈ Normal (any population)
✅ FINITE POP: n/N > 0.05 → multiply SE by √((N-n)/(N-1))
✅ PROPORTION: npq > 9 → p̂ ≈ Normal, SE = √(pq/n)
✅ SMALL SAMPLE MEAN: n < 30 + σ unknown + normal pop → use t_(n-1)
✅ VARIANCE: MUST have normal population → use χ²_(n-1)
✅ CONTINUITY CORRECTION: Always ±0.5 when discrete → continuous
```

> 💡 **Pro Tip**: When in doubt, write down:  
> 1. What parameter? (μ, p, σ², difference?)  
> 2. What's known? (σ? population shape? n?)  
> 3. Check the table above → pick formula → verify conditions ✓

Save this reference — it covers every limitation rule from your book! 🎯