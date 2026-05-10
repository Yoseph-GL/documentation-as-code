# SQL Structure: Constraints and Keys

## Architecture / Rationale

Constraints are the primary mechanism to keep data valid under concurrent writes.

Constraint model:
- `PRIMARY KEY` for row identity.
- `UNIQUE` for business uniqueness.
- `NOT NULL` for required fields.
- `CHECK` for domain rules.

## Query / Code Blocks

```sql
CREATE TABLE IF NOT EXISTS users (
  user_id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(255) UNIQUE,
  age INT NULL,
  CONSTRAINT chk_users_age CHECK (age IS NULL OR age >= 18)
);
```

## Performance / Optimization Notes

- `UNIQUE` creates an index and accelerates equality filters.
- `CHECK` removes invalid data before it reaches read paths and reporting pipelines.
- Use constraints to reject bad writes early and reduce repair jobs later.
