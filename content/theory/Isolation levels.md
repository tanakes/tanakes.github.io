Let’s build this from **zero → clear understanding → differences → anomalies**.

---

# 🧠 1. What are Isolation Levels?

When multiple transactions run at the same time in a database, they can **interfere with each other**.

👉 Example:

- Transaction A is updating a value
- Transaction B reads that value at the same time

Depending on timing, B might see:

- old data
- half-updated data
- different results in the same query

To control this, databases use **Isolation Levels** (part of ACID).

📌 Isolation level = **how “separate” transactions are from each other**

---

# ⚠️ 2. Main Problems (Anomalies)

These are the core issues isolation levels try to prevent:

### 1. Dirty Read

Reading data that **is not committed yet**

👉 Example:

- A changes balance to 0 (but hasn’t committed)
- B reads 0
- A rolls back → balance was never actually 0

💥 B saw fake data

---

### 2. Non-repeatable Read

Reading same row twice → **different values**

👉 Example:

- B reads balance = 100
- A updates it to 200 and commits
- B reads again → 200

💥 Same query, different result

---

### 3. Phantom Read

Re-running a query → **different number of rows**

👉 Example:

- B: SELECT * FROM users WHERE age > 18 → 10 rows
- A inserts new matching row
- B runs again → 11 rows

💥 New “phantom” row appears

---

### 4. Lost Update (important!)

Two transactions overwrite each other

👉 Example:

- A reads value = 10
- B reads value = 10
- A writes 15
- B writes 20

💥 A’s update is lost

---

# 🧱 3. Isolation Levels (from weakest → strongest)

---

## 🟢 1. READ UNCOMMITTED

🔓 Lowest isolation

- Allows **dirty reads**
- Everything else can happen too

👉 Almost no protection

---

## 🔵 2. READ COMMITTED ← your case

```
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

### ✅ What it guarantees:

- You **only read committed data**

### ❌ Still possible:

- Non-repeatable reads
- Phantom reads
- Lost updates (depending on DB)

---

### 💡 How READ COMMITTED behaves:

Every query sees **latest committed data at that moment**

👉 Example:

Transaction B:

```
SELECT balance → 100
```

Transaction A:

```
UPDATE balance = 200
COMMIT
```

Transaction B again:

```
SELECT balance → 200
```

💥 Data changed during same transaction → allowed

---

## 🟡 3. REPEATABLE READ

### ✅ Guarantees:

- No dirty reads
- No non-repeatable reads

### ❌ Still possible:

- Phantom reads (in some DBs)

👉 Rows you read **cannot change**, but new rows can appear

---

## 🔴 4. SERIALIZABLE

🔒 Strongest level

### ✅ Guarantees:

- No dirty reads
- No non-repeatable reads
- No phantom reads

👉 Transactions behave as if they run **one by one**

💥 But:

- Slowest
- More locking

---

# 📊 4. Quick Comparison Table

| Isolation Level  | Dirty Read | Non-repeatable read | Phantom read | Lost Update (PostgreSQL)         |
| ---------------- | ---------- | ------------------- | ------------ | -------------------------------- |
| Read Uncommitted | ✅ Yes      | ✅ Yes               | ✅ Yes        | ✅ Yes (not supported in PG)      |
| Read Committed   | ❌ No       | ✅ Yes               | ✅ Yes        | ✅ Yes (without atomic ops)       |
| Repeatable Read  | ❌ No       | ❌ No                | ✅ Yes        | ❌ No (serialization failure)     |
| Serializable     | ❌ No       | ❌ No                | ❌ No         | ❌ No                             |

---

# 🎯 5. Answer to Your Task

### ❓ “What anomalies can happen with READ COMMITTED?”

👉 In **READ COMMITTED**, you can have:

- ❌ **Dirty reads** → NOT possible
- ⚠️ **Non-repeatable reads** → possible
- ⚠️ **Phantom reads** → possible
- ⚠️ **Lost updates** → possible (depends on DB)

---

# 🔑 6. Key Idea (simple)

- **READ COMMITTED = safe, but not stable**
- You won’t read garbage data…
- …but data can still change while you’re working

---

