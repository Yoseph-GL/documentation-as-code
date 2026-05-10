# SQL Basics: Baseline Performance

## Architecture / Rationale

Performance validation is required even for basic SQL patterns. Query quality must be measured before publication or production use.

Validation goals:
- Verify index usage.
- Detect full scans and temporary sorts.
- Keep latency within baseline thresholds.

## Query / Code Blocks

```sql
CREATE INDEX idx_users_created_at ON users (created_at);
CREATE INDEX idx_users_age ON users (age);

EXPLAIN SELECT user_id, name FROM users WHERE age BETWEEN 18 AND 30;
EXPLAIN ANALYZE SELECT age, COUNT(*) FROM users GROUP BY age;
```

```sql
SELECT user_id, name, created_at
FROM users
WHERE created_at >= '2026-01-01'
ORDER BY created_at DESC
LIMIT 100;
```

## Performance / Optimization Notes

- Target access types `const`, `ref`, or `range`; investigate `ALL`.
- Point lookup by primary or unique key should remain under p95 `< 20 ms`.
- Indexed list query (`LIMIT <= 100`) should remain under p95 `< 120 ms`.
- Aggregations on transactional tables should remain under p95 `< 500 ms` or move to pre-aggregated datasets.
