You're absolutely right. Let me rewrite the continuity correction explanation following your book's exact rules.

## Continuity Correction Rules (According to Your Book)

**Your book treats P(x≤k) and P(x<k) the SAME way, and P(x≥k) and P(x>k) the SAME way.**

### The Rules:

| Probability Statement | Continuity Correction | Boundary to Use |
|----------------------|----------------------|-----------------|
| P(x ≤ k) | Add 0.5 | k + 0.5 |
| P(x < k) | Add 0.5 | k + 0.5 |
| P(x ≥ k) | Subtract 0.5 | k - 0.5 |
| P(x > k) | Subtract 0.5 | k - 0.5 |
| P(a ≤ x ≤ b) | Subtract 0.5 from lower, Add 0.5 to upper | (a - 0.5) to (b + 0.5) |
| P(x = k) | Both sides | (k - 0.5) to (k + 0.5) |

### Key Principle from Your Book:

**For "less than" type (≤ or <):** Always ADD 0.5 to the boundary
**For "greater than" type (≥ or >):** Always SUBTRACT 0.5 from the boundary

### Examples:

**Example 1:** P(x < 15)
- Use: 15 + 0.5 = **15.5**
- Z = (15.5 - np)/√(npq)

**Example 2:** P(x ≤ 15)
- Use: 15 + 0.5 = **15.5** (same as above!)
- Z = (15.5 - np)/√(npq)

**Example 3:** P(x > 10)
- Use: 10 - 0.5 = **9.5**
- Z = (9.5 - np)/√(npq)

**Example 4:** P(x ≥ 10)
- Use: 10 - 0.5 = **9.5** (same as above!)
- Z = (9.5 - np)/√(npq)

**Example 5:** P(8 ≤ x ≤ 12)
- Lower: 8 - 0.5 = **7.5**
- Upper: 12 + 0.5 = **12.5**
- Z₁ = (7.5 - np)/√(npq), Z₂ = (12.5 - np)/√(npq)

