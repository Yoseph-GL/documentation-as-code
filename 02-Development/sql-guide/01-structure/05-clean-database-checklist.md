# SQL Structure: Clean Database Checklist

## Architecture / Rationale

This checklist standardizes schema quality for public learning and production portability.

Acceptance criteria:
- Names are consistent and semantic.
- Keys and constraints enforce business rules.
- Relationship paths are unambiguous.
- DDL is migration-ready and reviewable.

## Query / Code Blocks

```sql
-- Integrity verification examples
SHOW CREATE TABLE users;
SHOW CREATE TABLE users_languages;

-- Duplicate edge check in N:M table
SELECT user_id, language_id, COUNT(*) AS duplicates
FROM users_languages
GROUP BY user_id, language_id
HAVING COUNT(*) > 1;

-- Orphan detection check
SELECT ul.users_languages_id
FROM users_languages ul
LEFT JOIN users u ON u.user_id = ul.user_id
WHERE u.user_id IS NULL;
```

## Performance / Optimization Notes

- Run integrity checks before shipping schema updates.
- Keep schema review checklists versioned with migrations to preserve audit traceability.
- Fail deployment gates when duplicate edges or orphans are detected.
