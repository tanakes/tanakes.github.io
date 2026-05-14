Absolutely, I’ll replace the airline example with a much simpler everyday one: **tennis players, tournaments, and personal coaches**. The rest of the 1NF, 2NF, and 3NF examples stay the same (they were logical), but I’ll include them again for a complete, consistent explanation.

---

## 1NF – First Normal Form
**Rule:** A table is in 1NF if every column contains only atomic (indivisible) values and there are no repeating groups.

### Example – Student Phone Numbers
A university stores student contact details.

| student_id | name  | phone_numbers        |
|------------|-------|----------------------|
| 1          | Alice | 555-0101, 555-0102  |
| 2          | Bob   | 555-0202            |

The `phone_numbers` column can hold multiple values – it’s not atomic.  
**Violation:** not in 1NF.

**Fix (1NF):** Give each phone number its own row.

| student_id | name  | phone_number |
|------------|-------|--------------|
| 1          | Alice | 555-0101     |
| 1          | Alice | 555-0102     |
| 2          | Bob   | 555-0202     |

Now every cell contains exactly one value – the table is in 1NF.

---

## 2NF – Second Normal Form
**Prerequisite:** The table is in 1NF.  
**Rule:** No non‑prime attribute (an attribute not part of any candidate key) is partially dependent on a candidate key. If the primary key is a single column, 2NF is automatically satisfied.

### Logical Scenario – Order Details
A shop records orders. Business rules:
- Each **order** has a single **order date**.
- Each **product** has a **product name** and **product category**.
- For each line in an order, we record the **quantity** sold.

Everything is kept in one table with composite primary key `{order_id, product_id}`.

| order_id | product_id | quantity | order_date | product_name | product_category |
|----------|------------|----------|------------|----------------|------------------|
| 100      | P1         | 2        | 2026-05-10 | Laptop         | Electronics      |
| 100      | P2         | 1        | 2026-05-10 | Mouse          | Accessories      |
| 101      | P1         | 1        | 2026-05-11 | Laptop         | Electronics      |

**Real-world dependencies:**
- `order_id → order_date` – an order has one date.
- `product_id → product_name, product_category` – a product ID determines its details.
- `{order_id, product_id} → quantity` – quantity depends on both.

**Violation of 2NF:** `order_date` depends on part of the key (`order_id`), not the whole key. Similarly `product_name` and `product_category` depend only on `product_id`. They are **partially dependent** – causing redundancy and anomalies.

**Fix – Decompose to 2NF:**
- `Orders(order_id, order_date)`
- `Products(product_id, product_name, product_category)`
- `Order_Details(order_id, product_id, quantity)`

Now every non‑prime attribute depends on the **whole** key of its table – 2NF achieved.

---

## 3NF – Third Normal Form
**Prerequisite:** The table is in 2NF.  
**Rule:** A table is in 3NF if, for **every non‑trivial functional dependency** `X → A`, at least one of the following holds:

1. `X` is a **superkey**, or
    
2. `A` is a **prime attribute** (i.e., part of some candidate key).

### Logical Scenario – Students and Advisors
A university assigns each student exactly **one faculty advisor**. Each advisor has a name and an office. Business rules:
- A student has `student_id`, `student_name`, and is linked to an advisor.
- An advisor has `advisor_id`, `advisor_name`, and `office`.

We might store everything in one table:

| student_id | student_name | advisor_id | advisor_name | office   |
|------------|--------------|------------|--------------|----------|
| 1          | Alice        | A01        | Dr. Smith    | Room 101 |
| 2          | Bob          | A02        | Dr. Jones    | Room 205 |
| 3          | Carol        | A01        | Dr. Smith    | Room 101 |

**Functional dependencies:**
- `student_id → student_name, advisor_id` – each student ID yields their name and assigned advisor.
- `advisor_id → advisor_name, office` – an advisor ID determines the advisor’s name and office.

Candidate key: `{student_id}`.  
Non‑prime attributes: `student_name`, `advisor_id`, `advisor_name`, `office`.

`student_id → advisor_name` happens **transitively** through `advisor_id`. A non‑prime attribute (`advisor_name`) depends on another non‑prime attribute (`advisor_id`). This violates 3NF and creates redundancy: advisor details are repeated for every student advised by the same person.

**Fix – Decompose to 3NF:**
- `Students(student_id, student_name, advisor_id)` – foreign key to Advisors.
- `Advisors(advisor_id, advisor_name, office)`

Now every non‑prime attribute depends directly on the primary key of its table. 3NF satisfied.

---

## BCNF – Boyce–Codd Normal Form
**Prerequisite:** Usually 3NF, though some 3NF tables still violate BCNF.  
**Rule:** For every non‑trivial functional dependency `X → Y`, `X` must be a **superkey**. (BCNF tightens 3NF by removing the exception that allowed a non‑superkey determinant if the right‑hand side is a prime attribute.)

### Simple Logical Scenario – Tennis Coaching
Imagine a tennis academy where:
- Each **player** is assigned exactly **one personal coach** who travels with them.
- A **coach** trains **exactly one player** (strict one‑to‑one relationship – a personal coach only works with a single player).
- A player can participate in many **tournaments**, and for every tournament they enter, we record who their coach is (since the coach always accompanies them).

We record this in a table: `Player_Tournament(player_name, tournament_name, coach_name)`

| player_name | tournament_name | coach_name |
|-------------|-----------------|------------|
| Alice       | Wimbledon       | Coach X    |
| Alice       | US Open         | Coach X    |
| Bob         | Wimbledon       | Coach Y    |
| Carol       | Australian Open | Coach Z    |
| Carol       | Wimbledon       | Coach Z    |

**Real‑world functional dependencies:**
- `coach_name → player_name`
- `player_name → coach_name`
- `{player_name, tournament_name} → coach_name` (and thus all attributes).
- `{coach_name, tournament_name} → player_name`

We have **two candidate keys**:
- `{player_name, tournament_name}`
- `{coach_name, tournament_name}`

**Prime attributes:** `player_name`, `tournament_name`, `coach_name` – all three are prime because each appears in at least one candidate key.

**Check 3NF:**
- The only non‑trivial FD we have (apart from those implied by keys) is `coach_name → player_name`.
- The right‑hand side `player_name` is a prime attribute.  
- 3NF has a special exception: if a dependency’s right side is a prime attribute, it does not need to come from a superkey. So this table **is in 3NF**.

**Check BCNF:**
- BCNF does **not** allow that exception. For the dependency `coach_name → player_name`, we ask: **is `coach_name` a superkey?**
- `coach_name` alone cannot determine `tournament_name` (a coach goes to many tournaments with their player). Therefore, `coach_name` is **not** a superkey.  
- The table **violates BCNF**.

**Fix – Decompose into BCNF:**
We split the table so that the offending dependency becomes a superkey in its own relation.
- `Coach_Player(coach_name, player_name)` – here `coach_name` **is** a candidate key (determines the player).
- `Player_Entry(player_name, tournament_name)` – here `{player_name, tournament_name}` is a candidate key.

Now every functional dependency has a superkey on its left side. Redundancy is eliminated, and BCNF is achieved.

---

## Summary

| Normal Form | Core Rule (simplified)                                                                 | Typical Anomalies Prevented                       |
|-------------|----------------------------------------------------------------------------------------|---------------------------------------------------|
| 1NF         | Atomic columns, no multi‑valued or repeating groups.                                   | Basic data entry and querying problems.           |
| 2NF         | No partial dependency of a non‑prime attribute on part of a composite key.             | Redundancy when an attribute depends only on part of a key. |
| 3NF         | No transitive dependency of a non‑prime attribute through another non‑prime attribute. | Redundancy and anomalies from indirect dependencies. |
| BCNF        | Every functional dependency’s left side must be a superkey.                            | Remaining anomalies caused by overlapping candidate keys, even when all attributes are prime. |

The tennis coaching example shows how a table can be in 3NF but not BCNF, and how decomposition resolves the hidden redundancy.