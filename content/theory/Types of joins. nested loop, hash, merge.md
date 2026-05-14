## Problem:

**Scenario:** Table A is very small Table B is very large No index Question:

- Which join is best? (Nested Loop / Hash / Merge)
- Explain why

### 1. Nested Loop Join

**How it works:**

- It is like two `for` loops in code.
- For **every row** in Table A, the database checks **every row** in Table B to find a match.

**When it is good:**

- When Table A is **very, very small** AND Table B has an **index** on the join column.

**When it is bad:**

- In your scenario: No index + Large Table B = Very slow. It would read the big table many times.

**Simple explanation:**

> "Look at one student. Check every single class in the school. Now look at the next student. Check every class again." This takes too much time if there are many classes.

---

### 2. Hash Join

**How it works:**

1. **Build Phase:** The database takes the **smaller table** (Table A) and puts it in a special fast box called a **Hash Table** in memory.
2. **Probe Phase:** The database reads the **larger table** (Table B) **one time**. For each row in B, it looks inside the fast box to see if there is a match.

**When it is good:**

- Your scenario exactly: One small table, one large table, **no index**. The small table fits in memory.

**When it is bad:**

- If both tables are too big for memory, it gets slow (must use disk).

**Simple explanation:**

> "Put the small list of students in a fast lookup box. Read the long list of classes one time. For each class, check the box: 'Is this student here?' Done."

---

### 3. Merge Join

**How it works:**

- The database **sorts** Table A and Table B on the join column first.
- Then it reads both tables together like a zipper. It moves forward only. It never looks back.

**When it is good:**

- When **both tables are already sorted** (for example, if there is an index on both join columns).
- Or when you need the final result in sorted order.

**When it is bad:**

- Your scenario: There are **no indexes**. Sorting a **very large Table B** takes a long time. Hash Join is faster because it **does not sort**.

**Simple explanation:**

> "Put both lists in A-B-C order first. That takes time. Then walk through both lists together. If the lists are not sorted already, you waste time sorting them."

---

### Summary for Your Scenario (Small A, Big B, No Index)

|Join Type|Performance in this scenario|Why?|
|---|---|---|
|**Nested Loop**|Very Bad|Reads big table many times.|
|**Merge Join**|Slow|Must spend time sorting the big table first.|
|**Hash Join**|**Best** ✅|Small table fits in memory. Scans big table **one time only**.|