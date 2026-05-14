# `UNION`

`UNION` combines results of multiple `SELECT` queries into one result set.

It automatically removes duplicates.

---

## Syntax

```sql
SELECT column1 FROM table1
UNION
SELECT column1 FROM table2;
```

Both queries must have:

- same number of columns
    
- compatible data types
    

---

## Example

```sql
SELECT surname
FROM cd.members

UNION

SELECT name
FROM cd.facilities;
```

This returns one combined list of:

- member surnames
    
- facility names
    

Duplicates are removed automatically.

---

## `UNION ALL`

Keeps duplicates and is faster ⚡

```sql
SELECT surname
FROM cd.members

UNION ALL

SELECT name
FROM cd.facilities;
```

---

## Difference

| Operation | Removes duplicates |
| --------- | ------------------ |
| UNION     | Yes                |
| UNION ALL | No                 |







