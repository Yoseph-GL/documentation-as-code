# SQL Level 1: Structure

## Architecture / Rationale

This level defines clean, scalable database structure patterns for production systems.

Goals:
- Enforce integrity with constraints, not application-only logic.
- Keep schema naming and evolution deterministic.
- Prevent duplicate relationships and orphan records.

## Query / Code Blocks

```sql
-- Module pages
-- 01-schema-foundations.md
-- 02-constraints-and-keys.md
-- 03-relationships-and-join-tables.md
-- 04-schema-changes-and-versioning.md
-- 05-clean-database-checklist.md
```

## Performance / Optimization Notes

- Structural decisions define query performance ceilings.
- Correct keys and constraints reduce full scans, duplicate writes, and data cleanup cost.
