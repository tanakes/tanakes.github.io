You're right — the previous two were just variable renames. Here's a more **different** problem with overlapping FDs and a non‑trivial candidate key.

---

### Problem 1

Consider the relation schema \( R(A, B, C, D, E) \) with functional dependencies:

$AB \rightarrow C,\quad C \rightarrow D,\quad D \rightarrow E$

**Question:** Decompose \(R\) into 3NF such that the decomposition is **dependency‑preserving**. Show all steps.

---
### Solution

#### Step 1 – Find candidate key(s)
- Start with \(AB\):  
  \($AB^+ = ABC$\) (using \($AB \rightarrow C$\)).  
  Then \($C \rightarrow D$\) gives \($AB^+ = ABCD$\).  
  Then \($D \rightarrow E$\) gives \($AB^+ = ABCDE$\).  
  So \(\{A, B\}\) is a **superkey**.  
- Is it minimal? Yes, neither \(A\) alone nor \(B\) alone determines everything (no FD with single attribute on left).  
- Candidate key = \(\{A, B\}\).

#### Step 2 – Check for 3NF violations
3NF rule: For every non‑trivial FD \($X \rightarrow Y$\):
- either \(X\) is a superkey,  
- or each attribute in \(Y\) is prime (i.e., part of *some* candidate key).  
Prime attributes here are \(A\) and \(B\) (only).

Check each FD:
- \($AB \rightarrow C$\): \(AB\) is a superkey → ✅ OK.
- \($C \rightarrow D$\): \(C\) is **not** a superkey, and \(D\) is **not** prime → ❌ violates 3NF.
- \($D \rightarrow E$\): \(D\) not a superkey, \(E\) not prime → ❌ violates 3NF.

#### Step 3 – Apply 3NF synthesis algorithm
First, find the **canonical cover** (already minimal here, no redundant attributes or FDs).  
We create one relation per FD, plus a relation containing a candidate key if not already covered.

- For \($AB \rightarrow C$\): create \($R_1(A, B, C)$\)  
- For \($C \rightarrow D$\): create \($R_2(C, D)$\)  
- For \($D \rightarrow E$\): create \($R_3(D, E)$\)

Candidate key \(\{A, B\}\) is already present in \($R_1(A,B,C)$\), so we do **not** need an extra relation.

#### Step 4 – Check dependency preservation
- \($AB \rightarrow C$\) can be checked on \($R_1$\) (all attributes \(A,B,C\) are there).  
- \($C \rightarrow D$\) can be checked on \($R_2$\).  
- \($D \rightarrow E$\) can be checked on \($R_3$\).

No join required. ✅ Dependency‑preserving.

#### Step 5 – Check 3NF for each relation
- \($R_1(A,B,C)$\): FD \($AB \rightarrow C$\) holds. Key = \(\{A,B\}\). Left side is superkey → 3NF.  
- \($R_2(C,D)$\): FD \($C \rightarrow D$\) holds. Key = \(\{C\}\). Left side is superkey → 3NF.  
- \($R_3(D,E)$\): FD \($D \rightarrow E$\) holds. Key = \(\{D\}\). Left side is superkey → 3NF.

All good.

---

### Final answer for Problem 1

Decompose \(R(A,B,C,D,E)\) with FDs \($AB \rightarrow C$,\; $C \rightarrow D$,\; $D \rightarrow E$\) into:

$R_1(A,B,C),\quad R_2(C,D),\quad R_3(D,E)$

This is in 3NF and dependency‑preserving.

---

### Problem 2

Relation \(R(A, B, C, D)\) with FDs:

$A \rightarrow B,\quad B \rightarrow C,\quad C \rightarrow A$

**Question:** Decompose into 3NF preserving dependencies.

---

### Solution for Problem 4

#### Step 1 – Candidate keys
- From \($A \rightarrow B$\), \($B \rightarrow C$\), \($C \rightarrow A$\), any of \(A\), \(B\), or \(C\) determines all three.  
- \(D\) is not determined by any FD, so we need \(D\) together with any of them.  
- Candidate keys = \(\{A, D\}\), \(\{B, D\}\), \(\{C, D\}\).  
  Prime attributes = All four attributes are prime because each appears in at least one candidate key: 
  - \(A\) in \(\{A,D\}\) → prime.  
  - \(B\) in \(\{B,D\}\) → prime.  
  - \(C\) in \(\{C,D\}\) → prime.  
  - \(D\) in all keys → prime.  
So **every attribute is prime**.

#### Step 2 – 3NF check
For any FD \($X \rightarrow Y$\), since every attribute in \(Y\) is prime, the condition "each attribute in \(Y\) is part of a candidate key" is automatically satisfied.  
Therefore, **the original relation is already in 3NF** (even though no FD has a superkey on the left, except trivial ones).

No decomposition is needed for 3NF. But the question asks to "decompose into 3NF" – we can just say: the relation is already in 3NF. Decomposition = \(\{R\}\).

#### Step 3 – Dependency preservation (trivial)
Only one relation, so all dependencies are preserved.

**Final answer:** No decomposition necessary; \(R\) is already in 3NF.