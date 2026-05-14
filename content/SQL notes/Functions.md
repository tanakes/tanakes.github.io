## 1. Function types

### 1.1 Scalar function

Returns a single value

```sql
CREATE FUNCTION add(a int, b int)
RETURNS int
AS $$
BEGIN
    RETURN a + b;
END;
$$ LANGUAGE plpgsql;
```

Usage:

```sql
SELECT add(2, 3);
```

---

### 1.2 Table function

Returns multiple rows

```sql
CREATE FUNCTION get_members()
RETURNS TABLE(id int, name text)
AS $$
BEGIN
    RETURN QUERY
    SELECT memid, firstname
    FROM cd.members;
END;
$$ LANGUAGE plpgsql;
```

---

### 1.3 VOID function

Returns nothing

```sql
CREATE FUNCTION log_action()
RETURNS void
AS $$
BEGIN
    RAISE NOTICE 'Executed';
END;
$$ LANGUAGE plpgsql;
```


### 1.4 Trigger functions


---

## 2. Structure of a function

```sql
CREATE FUNCTION name(params)
RETURNS type AS $$
DECLARE
    -- variables
BEGIN
    -- logic
    RETURN value;
END;
$$ LANGUAGE plpgsql;
```

---

## 3. RETURN

Depends on function type:

- scalar → `RETURN value`
    
- table → `RETURN QUERY`
    
- void → no return
    

---

## 4. Variables

### Declare + initialize

```sql
DECLARE x int := 5;
```

---

### Assign from query

```sql
SELECT firstname
INTO x
FROM cd.members
WHERE memid = 1;
```

---

## 5. Control flow

### IF statement

```sql
IF x > 10 THEN
    RETURN 'big';
ELSE
    RETURN 'small';
END IF;
```

---

### WHILE loop

```sql
WHILE x < 10 LOOP
    x := x + 1;
END LOOP;
```

---

### FOR loop

```sql
FOR i IN 1..5 LOOP
    RAISE NOTICE '%', i;
END LOOP;
```

---


## 6. Example:

```sql
CREATE FUNCTION process_member(p_memid int)
RETURNS TABLE(member int, status text)
LANGUAGE plpgsql
AS $$
DECLARE
    member_name text;
    counter int := 0;
BEGIN
    SELECT firstname
    INTO member_name
    FROM cd.members
    WHERE memid = p_memid;

    IF member_name IS NULL THEN
        RETURN QUERY SELECT p_memid, 'not found';
        RETURN;
    END IF;

    WHILE counter < 2 LOOP
        RETURN QUERY
        SELECT p_memid, member_name;

        counter := counter + 1;
    END LOOP;
END;
$$;
```

---

## 7. Key rules

- `RETURNS` defines output type
- `DECLARE` is for variables
- `BEGIN ... END` contains logic
- `RETURN` used for scalar results
- `RETURN QUERY` used for multiple rows
- `SELECT ... INTO` assigns query result to variable
- variables can be initialized with `:=`


