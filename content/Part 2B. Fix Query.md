## Original:
Part 2. Section B: Correct the Query
The following SQL queries contain logical or syntax errors. Provide the corrected version
for each.
Task: Find the department names and their average salaries, but only for
departments where the average salary is greater than $50,000.
```sql
SELECT dept_name, AVG(salary) FROM employees WHERE
AVG(salary) > 50000 GROUP BY dept_name;
```
Task: Update the stock level to 100 for all products that have never been ordered.
```sql
UPDATE Products SET stock = 100 WHERE id NOT IN (SELECT
product_id FROM Orders WHERE product_id IS NULL);
```
Task: List all students who are enrolled in more than 3 courses.
```sql
SELECT student_id, COUNT(course_id) FROM Enrollments
GROUP BY student_id WHERE COUNT(course_id) > 3;
```

### Solution
Here are the corrected SQL queries, with plain explanations and examples after each.

---

#### Task 1: Departments with average salary > $50,000

**Original (incorrect):**
```sql
SELECT dept_name, AVG(salary) FROM employees WHERE AVG(salary) > 50000 GROUP BY dept_name;
```

**Why it’s wrong:**  
The `WHERE` clause runs **before** grouping, so it cannot use aggregate functions like `AVG()`. Aggregates should be filtered using `HAVING`, which runs **after** grouping.

**Corrected:**
```sql
SELECT dept_name, AVG(salary) FROM employees GROUP BY dept_name HAVING AVG(salary) > 50000;
```

**Example to clarify:**  
Imagine the `employees` table:

| dept_name | salary |
|-----------|--------|
| Sales     | 60,000 |
| Sales     | 70,000 |
| IT        | 40,000 |
| IT        | 45,000 |

- `GROUP BY dept_name` creates two groups: Sales (avg 65,000), IT (avg 42,500).
- `HAVING AVG(salary) > 50000` keeps only Sales.  
- `WHERE` would have failed because it tries to check `AVG(salary)` before groups exist.

---

#### Task 2: Update stock to 100 for products never ordered

**Original (incorrect):**
```sql
UPDATE Products SET stock = 100 WHERE id NOT IN (SELECT product_id FROM Orders WHERE product_id IS NULL);
```

**Why it’s wrong:**  
The subquery `WHERE product_id IS NULL` will return only rows where `product_id` is null – that’s usually no rows, or just null values. `NOT IN (null)` behaves unexpectedly (it returns no rows because `x NOT IN (NULL)` is unknown). The intent was to find products that never appear in the `Orders` table at all.

**Corrected (using NOT EXISTS, safest):**
```sql
UPDATE Products SET stock = 100 WHERE NOT EXISTS (SELECT 1 FROM Orders WHERE Orders.product_id = Products.id);
```

**Alternative (using NOT IN, but be careful with nulls):**
```sql
UPDATE Products SET stock = 100 WHERE id NOT IN (SELECT product_id FROM Orders WHERE product_id IS NOT NULL);
```

**Example to clarify:**  
`Products` table:

| id | name       | stock |
|----|------------|-------|
| 1  | Laptop     | 50    |
| 2  | Mouse      | 30    |
| 3  | Keyboard   | 20    |

`Orders` table:

| order_id | product_id |
|----------|------------|
| 101      | 1          |
| 102      | 1          |

- Product 1 appears in orders → exclude.  
- Products 2 and 3 never appear → their stock should be updated to 100.  
- The corrected query checks: “Is there any order with this product id?” If no, update.

---

#### Task 3: Students enrolled in more than 3 courses

**Original (incorrect):**
```sql
SELECT student_id, COUNT(course_id) FROM Enrollments GROUP BY student_id WHERE COUNT(course_id) > 3;
```

**Why it’s wrong:**  
`WHERE` cannot appear **after** `GROUP BY`. Conditions on aggregated values must use `HAVING` after `GROUP BY`.

**Corrected:**
```sql
SELECT student_id, COUNT(course_id) FROM Enrollments GROUP BY student_id HAVING COUNT(course_id) > 3;
```

**Example to clarify:**  
`Enrollments` table:

| student_id | course_id |
|------------|-----------|
| 101        | Math      |
| 101        | Physics   |
| 101        | Chemistry |
| 101        | Biology   |
| 102        | Math      |
| 102        | Physics   |

- Student 101 has 4 courses → count = 4 → included.  
- Student 102 has 2 courses → excluded.  
- `HAVING COUNT(course_id) > 3` filters groups after counting. `WHERE` would have tried to filter before grouping, which makes no sense here.

---



























## Problem 1
TASK: Find all customers and their orders, INCLUDING customers without orders, filtered to orders placed in 2025. WHAT IS WRONG WITH THIS QUERY? Provide the corrected version. 
```sql
SELECT c.name, o.order_date FROM Customers c LEFT JOIN Orders o ON o.customer_id = c.customer_id WHERE o.order_date >= '2025-01-01' AND o.order_date < '2026-01-01';
```

You're running into a classic problem: **filtering on the "right" table of a `LEFT JOIN` turns it into an `INNER JOIN`**.

### What's wrong?

- `LEFT JOIN` keeps all customers, even those with **no matching orders** → for those customers, all `Orders` columns are `NULL`.
- The `WHERE` clause then says: `WHERE o.order_date >= '2025-01-01' …`
- For a customer without orders, `o.order_date` is `NULL`, and comparing `NULL` with a date yields `UNKNOWN` (not `TRUE`).
- SQL only keeps rows where the `WHERE` condition evaluates to `TRUE`. `UNKNOWN` is treated as `FALSE` → **customers without orders are dropped**.
- The result is the same as an `INNER JOIN` – you lose exactly the customers you wanted to include.

### Example to clarify

**Customers table:**
| name | customer_id |
|------|-------------|
| Alice | 1 |
| Bob   | 2 |

**Orders table (only Bob has an order in 2025):**
| order_date | customer_id |
|------------|-------------|
| 2025-06-01 | 2 |

Your original query would return **only Bob**, because Alice has no order → `o.order_date` is `NULL` → `WHERE` condition fails → Alice is excluded.

### Corrected version

Move the date filter into the `JOIN` condition (or use an `OR` allowing `NULL`, but the `JOIN` approach is clearer):

```sql
SELECT c.name, o.order_date
FROM Customers c
LEFT JOIN Orders o 
    ON o.customer_id = c.customer_id
    AND o.order_date >= '2025-01-01'
    AND o.order_date < '2026-01-01';
```

Now:
- For customers with orders in 2025 → you see the order date.
- For customers with orders **outside** 2025 → the `JOIN` condition fails, so `o.order_date` becomes `NULL` (but the customer still appears).
- For customers without any orders → same result: `NULL` in the order columns, but **customer is retained**.

**Result with example data:**
| name  | order_date |
|-------|------------|
| Alice | NULL       |
| Bob   | 2025-06-01 |

That's exactly what "customers **including** those without orders" means.

### Alternatives:
```sql
SELECT c.name, o.order_date
FROM Customers c
LEFT JOIN Orders o ON o.customer_id = c.customer_id
WHERE o.order_date IS NULL
   OR (o.order_date >= '2025-01-01' AND o.order_date < '2026-01-01');
```

```sql
SELECT c.name, o.order_date
FROM Customers c
LEFT JOIN (
    SELECT order_date, customer_id
    FROM Orders
    WHERE order_date >= '2025-01-01'
      AND order_date < '2026-01-01'
) o ON o.customer_id = c.customer_id;
```





# Problem 2
TASK: Create an Orders table with proper constraints. WHAT DESIGN PROBLEMS EXIST IN THIS DDL? Provide the corrected version. 
```sql
CREATE TABLE Orders ( order_id INT, customer_id INT, total DECIMAL(10,2) CHECK (total > 0), status VARCHAR(20) DEFAULT 'new', UNIQUE (order_id) );
```






Let’s go step by step.

## Problems in the given DDL

### 1. **No Primary Key**  
`order_id` is only marked as `UNIQUE`, but not as `PRIMARY KEY`.  
- A primary key guarantees **uniqueness** AND **non-null** for each row.  
- Example: If you insert two rows with `order_id = NULL` and different customers, `UNIQUE` would allow both (because NULLs are not compared as equal). That breaks the rule that every order should have a unique, non‑null identifier.  

### 2. **Missing `NOT NULL` constraints**  
`order_id`, `customer_id`, and `total` should not be allowed to be `NULL` in a real orders table.  
- Example: An order without a customer ID is meaningless – you wouldn’t know who placed the order.  
- Example: `total` being `NULL` would break the `CHECK (total > 0)` because `NULL > 0` is unknown, not false, so the row would be inserted but later cause calculation errors.  

### 3. **No foreign key on `customer_id`**  
`customer_id` should reference a `Customers` table to ensure every order belongs to a real customer.  
- Example: Without a foreign key, you could insert an order for `customer_id = 999` even if no customer with that ID exists. Later joins would silently lose that order.

### 4. **No check on `status`**  
The column `status` has a default `'new'`, but nothing prevents invalid values like `'unknown'` or `'pending'` if those are not allowed.  
- Example: An application bug could set `status = 'finished'` but your business logic expects only `'new'`, `'processing'`, `'shipped'`, `'cancelled'`. Without a `CHECK`, the database would accept it, and reports might break.

### 5. **`total > 0` might be too strict**  
Some real orders can have a total of **0** (e.g., free giveaway items, $0 promotional orders).  
- Example: A bookstore giving away a free bookmark with a purchase might have a separate order line with total $0. The `CHECK` would block it.  
- Better to use `total >= 0` unless your business explicitly forbids $0 orders.

---

## Corrected version

```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    total DECIMAL(10,2) NOT NULL CHECK (total >= 0),
    status VARCHAR(20) NOT NULL DEFAULT 'new'
        CHECK (status IN ('new', 'processing', 'shipped', 'cancelled')),
    CONSTRAINT fk_orders_customer
        FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);
```

### What changed and why

- **`PRIMARY KEY`** instead of `UNIQUE` – ensures `order_id` is both unique and never `NULL`.  
  *Example:* Trying to insert `(NULL, 5, 100, 'new')` will be rejected immediately.

- **`NOT NULL`** on `customer_id` and `total` – prevents incomplete orders.  
  *Example:* `INSERT INTO Orders (order_id, total) VALUES (101, 50)` would fail because `customer_id` is missing.

- **Foreign key** – guarantees every `customer_id` exists in the `Customers` table.  
  *Example:* If you try to insert `customer_id = 999` but `Customers` has no such ID, the database rejects the insert.

- **`CHECK` on `status`** – restricts values to a predefined list.  
  *Example:* `UPDATE Orders SET status = 'shipped'` works, but `SET status = 'delivered'` fails because `delivered` is not in the allowed set.

- **`total >= 0`** – allows zero‑dollar orders if needed.  
  *Example:* A promotional order with free items can have `total = 0.00` without violating the constraint.









# Problem 3
TASK: Delete all rows from Products where the price exceeds the average price of the table. WHAT IS WRONG WITH THIS QUERY? Provide the corrected version. 
```sql
DELETE FROM Products WHERE price > AVG(price);
```


The problem with `DELETE FROM Products WHERE price > AVG(price);` is that **you cannot use an aggregate function like `AVG()` directly in a `WHERE` clause**.  
- `WHERE` evaluates row by row *before* any aggregation.  
- `AVG(price)` needs to look at *all rows* to compute a single value, so it must be calculated separately, typically in a subquery.

**Corrected version:**  
```sql
DELETE FROM Products 
WHERE price > (SELECT AVG(price) FROM Products);
```

**Example to clarify:**  
Suppose the `Products` table has prices: 100, 200, 300.  
- Average = 200.  
- The subquery `(SELECT AVG(price) FROM Products)` returns 200.  
- Then the outer `DELETE` removes rows where price > 200 → only the row with 300 is deleted.  

Without the subquery, the database would throw an error (e.g., "misuse of aggregate function") because it doesn't know how to apply `AVG()` row by row.
>Note, we can't use HAVING here










# Problem 4
TASK: Show customer names along with their orders, sorted by total amount descending. FIND ALL THE BUGS IN THIS QUERY AND FIX THEM. 
```sql
SELECT customer_name, order_id, total FROM Customers JOIN Orders; ORDER BY total DESC;
```



Here are the bugs in the query, explained with plain language and examples.

---

### Bug 1: Missing JOIN condition (Cartesian product)

**What's wrong:**  
You wrote `FROM Customers JOIN Orders` without an `ON` clause. This creates a Cartesian product – every customer is paired with every order. If you have 100 customers and 1,000 orders, you get 100,000 rows, most of them meaningless (e.g., customer "Alice" matched with an order belonging to "Bob").

**Example:**  
Customers table:  
| customer_id | customer_name |  
|-------------|---------------|  
| 1           | Alice         |  
| 2           | Bob           |  

Orders table:  
| order_id | customer_id | total |  
|----------|-------------|-------|  
| 101      | 1           | 200   |  
| 102      | 2           | 150   |  

Without `ON` condition:  
Alice – order 101 (correct)  
Alice – order 102 (wrong, Alice didn't place order 102)  
Bob – order 101 (wrong)  
Bob – order 102 (correct)  

**Fix:** Add `ON Customers.customer_id = Orders.customer_id` (or whatever the foreign key is).

---

### Bug 2: Misplaced semicolon

**What's wrong:**  
You placed a semicolon right after `JOIN Orders;` and then wrote `ORDER BY total DESC;` on the next line. In SQL, a semicolon ends the entire statement. So the database sees two separate commands:  
1. `SELECT ... FROM Customers JOIN Orders;` (no ORDER BY)  
2. `ORDER BY total DESC;` (invalid by itself)

**Example:**  
If you run this, you'll likely get a syntax error because `ORDER BY` without a `SELECT` doesn't make sense.

**Fix:** Remove the semicolon after `Orders` and put a single semicolon at the very end of the query.

---

### Bug 3: Ambiguous column name `total` and `order_id`

**What's wrong:**  
Both `Customers` and `Orders` might have columns named `total`? Usually `total` is in `Orders`. But if later someone adds a `total` column to `Customers`, the query becomes ambiguous and fails. Same for `order_id` (only in `Orders`, but it's good practice to qualify).

**Example:**  
If `Customers` had a column `total` (e.g., lifetime spending), the database wouldn't know whether `ORDER BY total` means the order total or customer total.

**Fix:** Prefix with table name: `Orders.total`, `Orders.order_id`. This also makes the query self-documenting.


---

## Corrected Query

```sql
SELECT 
    Customers.customer_name, 
    Orders.order_id, 
    Orders.total
FROM Customers 
JOIN Orders ON Customers.customer_id = Orders.customer_id
ORDER BY Orders.total DESC;
```

**Explanation of the fix:**  
- `ON` condition ensures each order is linked to the correct customer.  
- No stray semicolon – only one at the end.  
- Table prefixes avoid ambiguity. 
- `ORDER BY Orders.total DESC` sorts from largest total to smallest.


