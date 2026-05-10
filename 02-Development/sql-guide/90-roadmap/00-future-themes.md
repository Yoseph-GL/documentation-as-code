# SQL Future Themes Roadmap

## Architecture / Rationale

This roadmap keeps the guide scalable without mixing advanced topics into the foundational levels.

Planned progression:
1. **Joins (next):** `INNER`, `LEFT`, `RIGHT`, anti-joins, join order strategy.
2. **Indexing Deep Dive:** composite index design, covering indexes, cardinality analysis.
3. **Transactions:** isolation levels, lock behavior, deadlock patterns.
4. **Query Optimization:** plan regression controls and workload benchmarking.
5. **Operational SQL:** migrations at scale, backups, restore drills.

## Query / Code Blocks

```sql
-- Example placeholder for upcoming joins module
SELECT u.user_id, u.name, c.company_name
FROM users u
INNER JOIN companies c ON c.company_id = u.company_id;
```

## Performance / Optimization Notes

- Keep advanced topics isolated by level to preserve entry-level readability.
- Promote topics from roadmap to active modules only after baseline examples and performance checks are documented.
