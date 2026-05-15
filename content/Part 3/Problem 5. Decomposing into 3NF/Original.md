## Statement
5. Decompose R(A, B, C, D) with FDs {A -> B, B -> C} into 3NF. Ensure it is
dependency-preserving

## Solution
## What does "dependency-preserving" mean?

A decomposition is **dependency-preserving** if we can check every original functional dependency (FD) without having to join the decomposed tables back together.  
In other words, each FD can be verified on a *single* table in the decomposition – not across multiple tables.

**Example:**  
Suppose you have an FD `X → Y`. After splitting the big table into smaller tables, there should be at least one table that contains **all** attributes of `X ∪ Y`. Then you can check `X → Y` directly on that table. If you need to join two or more tables to see if `X → Y` holds, the decomposition does **not** preserve that dependency.

---

## Step-by-step decomposition of `R(A, B, C, D)` with FDs `{A → B, B → C}` into 3NF (dependency‑preserving)

### 1. Find the candidate key(s) of the original relation
- `A → B` and `B → C` imply `A → C` (transitivity).  
- But **no FD** involves `D`. So `D` is not determined by any other attribute.  
- To uniquely identify a row, you need `A` (which gives `B` and `C`) **plus** `D`.  
- **Candidate key = {A, D}**.  
  - `{A, D}⁺ = {A, B, C, D}` (all attributes).  
  - No smaller subset determines everything.

### 2. Check 3NF violations
A relation is in 3NF if for every non‑trivial FD `X → Y`:
- either `X` is a **superkey**,  
- or every attribute in `Y` is **prime** (i.e., part of *some* candidate key).

**Violations:**
- `A → B`  
  - `A` is **not** a superkey (it doesn’t determine `D`).  
  - `B` is **not** prime (prime attributes are only `A` and `D`). → violates 3NF.
- `B → C`  
  - `B` is not a superkey.  
  - `C` is not prime. → violates 3NF.

### 3. Apply the 3NF synthesis algorithm

**Step A – Create a relation for each FD from the canonical cover**  
Canonical cover is the same: `{A → B, B → C}`.

- For `A → B` → create `R₁(A, B)`  
- For `B → C` → create `R₂(B, C)`

**Step B – Ensure at least one relation contains a candidate key**  
Candidate key `{A, D}` is **not** present in `R₁` or `R₂`.  
So we add a new relation `R₃(A, D)` (just the candidate key attributes).

**Resulting decomposition:**  
- `R₁(A, B)`  
- `R₂(B, C)`  
- `R₃(A, D)`

### 4. Verify 3NF and dependency preservation

| Relation | Functional Dependencies | 3NF? | Why? |
|----------|------------------------|------|------|
| `R₁(A,B)` | `A → B` | ✅ | `A` is the key of this table (superkey). |
| `R₂(B,C)` | `B → C` | ✅ | `B` is the key of this table. |
| `R₃(A,D)` | (no non‑trivial FDs) | ✅ | All attributes are prime (both `A` and `D` form the key). |

**Dependency preservation check:**  
- `A → B` can be checked directly on `R₁`.  
- `B → C` can be checked directly on `R₂`.  
- No FD requires joining two tables.  

✅ **Preserved.**

---

## Final answer

The relation `R(A, B, C, D)` with FDs `{A → B, B → C}` is decomposed into the following 3NF schema (dependency‑preserving):

```
R₁(A, B)
R₂(B, C)
R₃(A, D)
```