# SQL Basics: Aggregation and Grouping

## Architecture / Rationale

Aggregation turns row-level data into operational metrics and summaries.

Pattern rules:
- Filter before aggregation when possible.
- Group only by required dimensions.
- Use `HAVING` to filter aggregated results.

## Query / Code Blocks

```sql
SELECT COUNT(*) AS total_users
FROM users;

SELECT AVG(age) AS avg_age
FROM users
WHERE age IS NOT NULL;

SELECT age, COUNT(*) AS total_by_age
FROM users
WHERE age > 15
GROUP BY age
HAVING COUNT(*) > 1
ORDER BY age ASC;
```

## Performance / Optimization Notes

- Large group operations can allocate temporary structures; keep pre-filters selective.
- Monitor planner output for `Using temporary` on large datasets.
