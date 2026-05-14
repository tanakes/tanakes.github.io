# `CASE`

Used for conditional logic inside queries.

## Syntax

```sql
CASE
    WHEN condition1 THEN result
    WHEN condition2 THEN result
    ELSE result
END
```

---

## Example — Multiple conditions

```sql
SELECT name,
       membercost,
       CASE
           WHEN membercost = 0 THEN 'free'
           WHEN membercost < 10 THEN 'low'
           ELSE 'high'
       END AS price_type
FROM cd.facilities;
```

---

