# Working with DATE datatypes

## Comparing
```sql
/* if it's timestamp */
select * from people where birthdate > '2012-02-04 12:23:52'; 
```

## `EXTRACT`

Used to get parts from `timestamp`, `date`, or `interval`.

### Syntax

```sql
EXTRACT(field FROM source)
```

---

### Common fields

|Field|Meaning|
|---|---|
|YEAR|year|
|MONTH|month|
|DAY|day|
|HOUR|hour|
|MINUTE|minute|
|SECOND|second|
|DOW|day of week|
|EPOCH|seconds|

---

### Example — Get year

```sql
SELECT joindate,
       EXTRACT(YEAR FROM joindate) AS year
FROM cd.members;
```


