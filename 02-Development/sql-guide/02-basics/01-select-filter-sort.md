# SQL Basics: Select, Filter, Sort, Limit

## Architecture / Rationale

Read operations should be explicit, deterministic, and bounded by output size.

Query rules:
- Select only required columns.
- Filter with precise predicates.
- Sort only when needed.
- Use `LIMIT` for user-facing lists.

## Query / Code Blocks

```sql
SELECT user_id, name, email
FROM users;

SELECT user_id, name
FROM users
WHERE age BETWEEN 18 AND 30
  AND email IS NOT NULL
ORDER BY created_at DESC
LIMIT 50;

SELECT DISTINCT age
FROM users
WHERE age IS NOT NULL
ORDER BY age ASC;
```

## Performance / Optimization Notes

- Avoid `SELECT *` in application code.
- Keep result sets bounded for endpoint stability.
- Align sort predicates with available indexes on high-traffic paths.
