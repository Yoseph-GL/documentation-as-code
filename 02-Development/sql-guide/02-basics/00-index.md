# SQL Level 2: Basics

## Architecture / Rationale

This level defines baseline SQL operations required for day-to-day backend work.

Scope:
- Read queries (`SELECT`, filters, sorting, limits).
- Aggregation patterns (`COUNT`, `SUM`, `AVG`, `GROUP BY`, `HAVING`).
- Expressions and null handling (`CASE`, `IFNULL`).
- Safe write operations (`INSERT`, `UPDATE`, `DELETE`).

## Query / Code Blocks

```sql
-- Module pages
-- 01-select-filter-sort.md
-- 02-aggregation-and-grouping.md
-- 03-expressions-and-null-handling.md
-- 04-safe-mutations.md
-- 05-baseline-performance.md
```

## Performance / Optimization Notes

- Keep basic queries explicit and bounded to avoid accidental hot-path regressions.
- Use this level as the minimum standard before moving into dedicated joins and advanced tuning modules.
