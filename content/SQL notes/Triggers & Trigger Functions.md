# 1. What is a trigger?

A **trigger** is a database rule that automatically executes:

- BEFORE or AFTER an `INSERT`
    
- BEFORE or AFTER an `UPDATE`
    
- BEFORE or AFTER a `DELETE`
    

You don’t call triggers manually. PostgreSQL calls them.

---

## Simple idea

```text
Something happens in table
→ PostgreSQL reacts automatically
→ trigger function runs
```

---

# 2. Trigger vs Trigger Function

This is the most important distinction.

|Component|Meaning|
|---|---|
|Trigger|“WHEN to run”|
|Trigger function|“WHAT to do”|

You always need BOTH.

---

# 3. Trigger function

A trigger function is a special PL/pgSQL function that:

- takes no normal arguments
    
- returns `TRIGGER`
    
- uses special variables: `NEW`, `OLD`
    

---

## 3.1 Basic trigger function template

```sql
CREATE FUNCTION example_trigger_func()
RETURNS TRIGGER
AS $$
BEGIN
    -- logic here
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

---

## 3.2 Special variables

### NEW

Row AFTER change / new row

### OLD

Row BEFORE change / old row

|Operation|OLD|NEW|
|---|---|---|
|INSERT|❌|✅|
|DELETE|✅|❌|
|UPDATE|✅|✅|

---

# 4. Example: log inserts

## Step 1: log table

```sql
CREATE TABLE member_log (
    memid int,
    action text,
    created_at timestamp default now()
);
```

---

## Step 2: trigger function

```sql
CREATE FUNCTION log_member_insert()
RETURNS TRIGGER
AS $$
BEGIN
    INSERT INTO member_log(memid, action)
    VALUES (NEW.memid, 'INSERT');

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

---

## Step 3: trigger

```sql
CREATE TRIGGER trg_member_insert
AFTER INSERT ON cd.members
FOR EACH ROW
EXECUTE FUNCTION log_member_insert();
```

---

# 5. How it works (step-by-step)

When you run:

```sql
INSERT INTO cd.members(memid, firstname)
VALUES (100, 'Alex');
```

PostgreSQL does:

```text
1. Insert row into cd.members
2. Trigger fires automatically
3. NEW = inserted row
4. Trigger function runs
5. Log row inserted into member_log
```

---

# 6. BEFORE vs AFTER triggers

## BEFORE trigger

Used to modify data before saving

```sql
BEFORE INSERT
```

Example:

```sql
NEW.firstname := upper(NEW.firstname);
```

---

## AFTER trigger

Used for side effects:

- logging
    
- auditing
    
- notifications
    

```sql
AFTER INSERT
```

---

# 7. Example: data validation (BEFORE trigger)

```sql
CREATE FUNCTION check_name()
RETURNS TRIGGER
AS $$
BEGIN
    IF NEW.firstname IS NULL THEN
        RAISE EXCEPTION 'firstname cannot be null';
    END IF;

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

Trigger:

```sql
CREATE TRIGGER trg_check_name
BEFORE INSERT ON cd.members
FOR EACH ROW
EXECUTE FUNCTION check_name();
```

---

# 8. UPDATE trigger example

```sql
CREATE FUNCTION track_update()
RETURNS TRIGGER
AS $$
BEGIN
    INSERT INTO member_log(memid, action)
    VALUES (NEW.memid, 'UPDATED');

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

---

Trigger:

```sql
CREATE TRIGGER trg_member_update
AFTER UPDATE ON cd.members
FOR EACH ROW
EXECUTE FUNCTION track_update();
```

---

# 9. DELETE trigger example

```sql
CREATE FUNCTION track_delete()
RETURNS TRIGGER
AS $$
BEGIN
    INSERT INTO member_log(memid, action)
    VALUES (OLD.memid, 'DELETED');

    RETURN OLD;
END;
$$ LANGUAGE plpgsql;
```

---

# 10. Trigger execution rules

- One trigger function can be used by multiple triggers
    
- Triggers run automatically
    
- You cannot call them manually
    
- Execution depends on event type
    

---

# 11. Trigger timing options

|Timing|Meaning|
|---|---|
|BEFORE|runs before change|
|AFTER|runs after change|
|INSTEAD OF|replaces operation (views only)|

---

# 12. Row-level vs Statement-level

## Row-level

```sql
FOR EACH ROW
```

Runs once per row.

Example:

- insert 3 rows → trigger runs 3 times
    

---

## Statement-level

```sql
FOR EACH STATEMENT
```

Runs once per query.

Example:

- insert 3 rows → trigger runs 1 time
    

---

# 13. Key rules (must remember)

- trigger function must return `TRIGGER`
    
- use `NEW` for INSERT/UPDATE
    
- use `OLD` for UPDATE/DELETE
    
- triggers fire automatically
    
- logic is separated: trigger ≠ function
    

