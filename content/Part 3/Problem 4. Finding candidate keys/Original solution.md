4. Given R(A, B, C, D, E) and F = {A -> B, BC -> D, D -> A}. Find all candidate keys.

---

>Tip: Always check right side of dependencies, if some columns missing from there, these columns must appear in candidate keys

---
The candidate keys for R(A, B, C, D, E) with functional dependencies  
F = {A → B, BC → D, D → A} are:

- **(A, C, E)**  
- **(B, C, E)**  
- **(C, D, E)**  

**Explanation**:  

- Attribute **E** never appears on the right side of any FD. That means you cannot derive E from other attributes – you must include E in every candidate key. Think of E as a “loner” that has to be present explicitly.  

- To find keys, we start with sets that include E and see which minimal sets determine all attributes.  

  - **{A, C, E}**:  
    From A → B we get B. Now we have A, B, C, E.  
    From BC → D we get D. Now we have all five attributes.  
    If we remove any one of A, C, or E, we lose the ability to get everything (e.g., without C we never get D; without A we never get B or D; without E we miss E itself).  

  - **{B, C, E}**:  
    From BC → D we get D.  
    From D → A we get A.  
    Then A → B (already have B). All attributes are obtained.  
    Again, removing B, C, or E breaks minimality.  

  - **{C, D, E}**:  
    From D → A we get A.  
    From A → B we get B.  
    We already have C, D, E. So all attributes appear.  
    Removing C, D, or E fails (e.g., without D we cannot get A; without C we cannot get D because BC→D needs B too, but B is not present initially).  

No other combination (like {A, E} or {D, E}) works because they cannot produce all attributes.  