You're right — the previous two were just variable renames. Here's a more **different** problem with overlapping FDs and a non‑trivial candidate key.

---

## Problem 1

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

#### Final answer for Problem 1

Decompose \(R(A,B,C,D,E)\) with FDs \($AB \rightarrow C$,\; $C \rightarrow D$,\; $D \rightarrow E$\) into:

$R_1(A,B,C),\quad R_2(C,D),\quad R_3(D,E)$

This is in 3NF and dependency‑preserving.

---

## Problem 2

Relation \(R(A, B, C, D)\) with FDs:

$A \rightarrow B,\quad B \rightarrow C,\quad C \rightarrow A$

**Question:** Decompose into 3NF preserving dependencies.

---

### Solution for Problem 2

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

---

Here’s an example where a functional dependency `X → Y` has `Y` as a **prime attribute**, so it does **not** violate 3NF even though `X` is **not** a superkey.

---

## Problem 3

**Relation:** `R(A, B, C, D)`  
**Functional Dependencies:**  
1. `AB → C`  
2. `C → B`  
3. `D → A`

---

### Step 1 – Find candidate keys

Start with `{A, B}⁺` = {A, B, C} (using `AB → C`). Not all attributes (missing D).  
Try `{A, D}`:  
- `A, D` → (D → A gives nothing new), but we have `D → A` so we can derive A.  
Let’s systematically compute closures:

- `{A, D}⁺`: start {A, D}.  
  - Using `D → A`, no new attribute (A already there).  
  - No other FD applies. Missing B, C. So not a key.

- `{B, D}⁺`: start {B, D}.  
  - `D → A` adds A → now {A, B, D}.  
  - `AB → C` adds C → now {A, B, C, D}.  
  → **Candidate key = {B, D}**.

- `{C, D}⁺`: start {C, D}.  
  - `C → B` adds B → now {B, C, D}.  
  - `D → A` adds A → now {A, B, C, D}.  
  → **Candidate key = {C, D}**.

- `{A, B, D}` is a superkey, but not minimal because `{B, D}` is smaller. Similarly `{A, C, D}` etc.

**Candidate keys:** `(B, D)` and `(C, D)`.  

**Prime attributes:** `B, C, D` (each appears in at least one candidate key).  
**Non‑prime attribute:** `A` only.

---

### Step 2 – Check 3NF for each FD

3NF rule: For every non‑trivial FD `X → Y`:
- Either `X` is a superkey,  
- **or** every attribute in `Y` is prime.

---

#### FD1: `AB → C`

- Left side `{A, B}` is **not** a superkey (does not determine D).  
- `C` is prime (appears in candidate key `(C, D)`).  
→ ✅ **Does not violate 3NF** (because right side is prime).

---

#### FD2: `C → B`

- `C` is **not** a superkey (does not determine A or D alone).  
- `B` is prime (appears in candidate key `(B, D)`).  
→ ✅ **Does not violate 3NF** (right side is prime).

---

#### FD3: `D → A`

- `D` is **not** a superkey (does not determine B or C alone).  
- `A` is **non‑prime** (A is not in any candidate key).  
→ ❌ **Violates 3NF** because `X` is not a superkey and `Y` contains a non‑prime attribute.

So the violation comes from `D → A`, not from the ones where `Y` is prime.

---
We continue from the point where we identified the 3NF violation: **D → A** (D not a superkey, A non‑prime).  
Now we apply the **3NF synthesis algorithm** to get a dependency‑preserving decomposition.

---

### Step 3: Find the canonical cover of FDs

Original FDs:  
`AB → C`  
`C → B`  
`D → A`

No redundancy or extraneous attributes.  
**Canonical cover** = same set:  
`{ AB → C,  C → B,  D → A }`

---

### Step 4: Create a relation for each FD in the canonical cover

- For `AB → C` → `R₁(A, B, C)`  
- For `C → B` → `R₂(B, C)`  
- For `D → A` → `R₃(D, A)`

---

### Step 5: Remove redundant relations (if one is a subset of another)

`R₂(B, C)` is a subset of `R₁(A, B, C)`.  
We drop `R₂` because `R₁` already contains both attributes `B` and `C`, so it can enforce `C → B`.  
Now we have:  
`R₁(A, B, C)`  
`R₃(D, A)`

---

### Step 6: Ensure at least one relation contains a candidate key of the original table

Original candidate keys: `{B, D}` and `{C, D}`.  
Neither `R₁` nor `R₃` contains any candidate key fully:  
- `R₁` has `B, C` but no `D`  
- `R₃` has `D, A` but no `B` or `C`

So we add a new relation `R₄` that contains one candidate key, e.g., `{B, D}`.  
**Add `R₄(B, D)`** (no non‑trivial FDs, since no FD has `B` or `D` alone on the left).

---

### Final 3NF decomposition (dependency‑preserving)

```
R₁(A, B, C)   with FDs: AB → C,  C → B
R₃(D, A)      with FD:   D → A
R₄(B, D)      with no non‑trivial FDs
```

- **Preserves all original FDs**  
  - `AB → C` and `C → B` are checked on `R₁`  
  - `D → A` is checked on `R₃`  
- **Each relation is in 3NF** (explanation in earlier reasoning)  
- **No need to join tables to verify any FD**

---

### Alternative (equally valid)

Use the other candidate key `{C, D}` instead of `{B, D}`:

```
R₁(A, B, C)
R₃(D, A)
R₄(C, D)
```

Both are correct.