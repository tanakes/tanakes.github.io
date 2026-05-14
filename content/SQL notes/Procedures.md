Procedures are similar to functions, but with one key difference: they are designed for **actions**, not returning values.

---

# 1. What is a procedure?

A **procedure** is a reusable block of PL/pgSQL code that:

- executes logic
    
- can modify data (INSERT/UPDATE/DELETE)
    
- does **NOT have to return a value**
    
- is executed using `CALL`, not `SELECT`
    

---

## Core idea

```text
Function → returns something
Procedure → performs an action
```

---

# 2. Procedure syntax

```sql
CREATE PROCEDURE name(parameters)
AS $$
BEGIN
    -- logic
END;
$$ LANGUAGE plpgsql;
```

---

# 3. How to run a procedure

```sql
CALL name(arguments);
```

Example:

```sql
CALL transfer_money(1, 2, 100);
```

---

# 4. Procedure vs Function (important)

|Feature|Function|Procedure|
|---|---|---|
|Call|SELECT|CALL|
|Returns value|Yes|Optional / usually no|
|Transaction control|No|Yes|
|Purpose|computation|actions|
|Use in SELECT|Yes|No|

---

# 5. Variables in procedures

```sql
CREATE PROCEDURE demo()
LANGUAGE plpgsql
AS $$
DECLARE
    x int := 10;
BEGIN
    x := x + 5;
END;
$$;
```

---

# 6. Example 1 — Simple update procedure

## Problem

Increase salary of all employees by 10%

---

```sql
CREATE PROCEDURE raise_salary()
AS $$
BEGIN
    UPDATE employees
    SET salary = salary * 1.1;
END;
$$ LANGUAGE plpgsql;
```

Run:

```sql
CALL raise_salary();
```

---

# 7. Example 2 — Transfer money (classic interview problem)

## Problem

Move money from account A to B safely.

---

```sql
CREATE PROCEDURE transfer_money(from_id int, to_id int, amount int) AS $$
BEGIN

    UPDATE accounts
    SET balance = balance - amount
    WHERE id = from_id;

    UPDATE accounts
    SET balance = balance + amount
    WHERE id = to_id;

END;
$$ LANGUAGE plpgsql;
```

Run:

```sql
CALL transfer_money(1, 2, 500);
```

---

# 8. Transaction control (major difference)

Procedures can control transactions:

```sql
BEGIN
    UPDATE accounts SET balance = balance - 100;

    COMMIT;

    UPDATE logs SET status = 'done';
END;
```

---

## Important

- Functions ❌ cannot use `COMMIT/ROLLBACK`
    
- Procedures ✅ can manage transactions
    

---

# 9. Example 3 — Safe transaction with rollback

```sql
CREATE PROCEDURE safe_transfer(a int, b int, amt int)
LANGUAGE plpgsql
AS $$
BEGIN

    UPDATE accounts SET balance = balance - amt WHERE id = a;
    UPDATE accounts SET balance = balance + amt WHERE id = b;

    COMMIT;

EXCEPTION
    WHEN OTHERS THEN
        ROLLBACK;
END;
$$;
```

---

# 10. Key rules

- called with `CALL`, not `SELECT`
    
- usually no return value
    
- supports transaction control
    
- used for business workflows
    
- can modify multiple tables safely
    

