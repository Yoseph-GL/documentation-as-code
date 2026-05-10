# SQL Basics: Expressions and Null Handling

## Architecture / Rationale

Expression functions provide deterministic derived columns and prevent null-related ambiguity in application code.

Focus:
- Null-safe projections.
- Conditional classification using `CASE`.
- String expression composition with `CONCAT`.

## Query / Code Blocks

```sql
SELECT
  user_id,
  name,
  IFNULL(age, 0) AS age_normalized
FROM users;

SELECT
  user_id,
  CASE
    WHEN age >= 18 THEN 'ADULT'
    ELSE 'MINOR'
  END AS age_class
FROM users;

SELECT CONCAT(name, ' ', last_name) AS full_name
FROM users;
```

## Performance / Optimization Notes

- Expression-heavy projections can increase CPU cost on large scans.
- Push expensive transformations to reporting layers when they are not needed in transactional paths.
