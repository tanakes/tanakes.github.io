# Why is z = 1.96 for 95% Confidence?
*Explained from absolute scratch*

---

## First: What do all these terms mean?

| Term | Meaning | Simple Example |
|------|---------|---------------|
| **Standard Normal Distribution** | A bell curve with mean = 0 and standard deviation = 1 | Like a "universal ruler" for probabilities |
| **Confidence Level** | The percentage of times our method would capture the true value if we repeated the study | 95% confidence = "If we did this 100 times, ~95 intervals would be correct" |
| **Critical Value (z*)** | The cutoff point on the standard normal curve that matches our confidence level | For 95% confidence, z* = 1.96 |
| **Tail Area** | The portion of the curve in the extreme ends (left or right) | If 95% is in the middle, 5% is split into two tails of 2.5% each |
| **Cumulative Probability** | The area under the curve to the *left* of a given z-value | F(1.96) = 0.975 means 97.5% of the area is left of z = 1.96 |

---

## Let's Build Understanding, Step by Step

### 🔹 What does "95% confidence" actually mean visually?

Imagine the standard normal curve (mean = 0, SD = 1):

```
        ▲
        |
    0.4 |           ***
        |         **   **
        |        *       *
    0.3 |       *         *
        |      *           *
        |     *             *
    0.2 |    *               *
        |   *                 *
        |  *                   *
    0.1 | *                     *
        |*                       *
        +----+----+----+----+----+----► z
       -3   -2   -1    0    1    2    3
```

**Key idea**: For 95% confidence, we want to capture the *middle 95%* of this curve.

➡️ That means 5% is left over, split equally between the two tails.

**Concrete example**:  
If the total area = 100%, and we keep 95% in the middle:
- Left tail = 2.5% = 0.025
- Right tail = 2.5% = 0.025
- Middle = 95% = 0.95 ✓

---

### 🔹 How do we find the z-value that cuts off 2.5% in the right tail?

We use the **cumulative distribution function** (CDF), which tells us:  
*"What's the area to the LEFT of this z-value?"*

$$\boxed{\text{For 95\% confidence: Find } z \text{ such that } P(Z \leq z) = 0.975}$$

**Why 0.975?**  
- We want 2.5% in the *right* tail
- So area to the *left* = 1 − 0.025 = **0.975** ✓

**Concrete example using the standard normal table** (from your Appendix, Table 2):

| z | F(z) = P(Z ≤ z) |
|---|-----------------|
| 1.94 | 0.9738 |
| 1.95 | 0.9744 |
| **1.96** | **0.9750** ← Bingo! |
| 1.97 | 0.9756 |
| 1.98 | 0.9761 |

✓ At z = 1.96, exactly 97.5% of the area is to the left → 2.5% is to the right.

By symmetry, z = −1.96 cuts off 2.5% on the *left*.

---

### 🔹 Comparing: Common Confidence Levels and Their z* Values

| Confidence Level | α (total tail area) | α/2 (one tail) | Cumulative Area | Critical Value z* |
|-----------------|---------------------|----------------|-----------------|------------------|
| 90% | 0.10 | 0.05 | 0.95 | **1.645** |
| 95% | 0.05 | 0.025 | 0.975 | **1.96** |
| 98% | 0.02 | 0.01 | 0.99 | **2.33** |
| 99% | 0.01 | 0.005 | 0.995 | **2.575** |

**✓ Key takeaway**: Higher confidence → larger z* → wider interval (more "net" to catch the truth).

---

### 🔹 Common Myth vs. Fact

| Myth | Fact |
|------|------|
| "z = 1.96 means there's a 95% chance the true mean is in my interval." | ❌ The true mean is fixed. The *method* has 95% success rate over many repetitions. |
| "1.96 is magic—it works for any data." | ❌ z = 1.96 only applies when: (1) population is normal OR sample is large, AND (2) σ is known. |
| "If I use z = 2 instead of 1.96, it's basically the same." | ✓ For quick mental math, yes! 2 is a handy approximation (error < 2%). But for precise work, use 1.96. |

---

### 🔹 Worked Example: Finding z* for 95% Confidence (Step-by-Step)

*Scenario*: You need the critical value for a 95% confidence interval. You have Table 2 (standard normal CDF) from the Appendix.

**Step 1**: Identify the tail area  
Confidence = 95% → α = 1 − 0.95 = 0.05  
One tail = α/2 = 0.025

**Step 2**: Find the cumulative area to look up  
Area to the LEFT = 1 − 0.025 = **0.9750**

**Step 3**: Search Table 2 for 0.9750  
Scan the body of the table for the value closest to 0.9750:

```
z = 1.9 → look across row:
1.90 → 0.9713
1.91 → 0.9719
...
1.95 → 0.9744
1.96 → 0.9750 ← FOUND IT!
```

**Step 4**: Read the z-value  
z = 1.9 (row) + 0.06 (column) = **1.96** ✓

**Step 5**: Interpret  
✓ We are 95% confident that a standard normal variable falls between −1.96 and +1.96.

---

## 📋 Summary: Why z = 1.96 for 95% Confidence

| Concept | Explanation |
|---------|-------------|
| **Goal** | Capture the middle 95% of the standard normal curve |
| **Tail area** | 5% total → 2.5% in each tail |
| **Cumulative area** | 1 − 0.025 = 0.975 (area to the left of z*) |
| **Table lookup** | Find z where F(z) = 0.9750 → z = 1.96 |
| **Symmetry** | −1.96 cuts off 2.5% on the left; +1.96 cuts off 2.5% on the right |
| **Result** | P(−1.96 < Z < 1.96) = 0.95 ✓ |

**Bold takeaways**:  
✓ **1.96 is not arbitrary**—it's the exact z-value that leaves 2.5% in each tail.  
✓ **Always match α/2 to the cumulative area**: 1 − α/2 = 0.975 for 95% confidence.  
✓ **Use your Appendix Table 2** to verify: find 0.9750 in the body, read z = 1.96.  
✓ **Memorize the big four**: 90%→1.645, 95%→1.96, 98%→2.33, 99%→2.575.

---

## 🛠️ How to Find z* for Any Confidence Level: Checklist

1. **Start with confidence level** (e.g., 95%)
2. **Compute α**: α = 1 − confidence level  
   ✓ Example: α = 1 − 0.95 = 0.05
3. **Split α for two tails**: α/2  
   ✓ Example: 0.05 / 2 = 0.025
4. **Find cumulative area**: 1 − α/2  
   ✓ Example: 1 − 0.025 = 0.9750
5. **Look up in standard normal table** (Appendix Table 2):  
   - Find the value closest to your cumulative area in the *body* of the table  
   - Read the corresponding z from the row + column headers
6. **Verify symmetry**: −z* should give cumulative area = α/2  
   ✓ Example: F(−1.96) = 0.0250 ✓
7. **Double-check**: P(−z* < Z < z*) should equal your confidence level  
   ✓ Example: 0.9750 − 0.0250 = 0.95 ✓

**Final checkmark**: ✓ If you can explain *why* 1.96 corresponds to 95% (not just memorize it), you've mastered this!
