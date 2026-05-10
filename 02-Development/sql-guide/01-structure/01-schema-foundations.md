# SQL Structure: Schema Foundations

## Architecture / Rationale

A clean schema starts with clear entity boundaries and deterministic identifiers.

Principles:
- One table per core entity.
- Surrogate integer primary keys for stable joins.
- Explicit data types and nullability.
- Default timestamps for auditability.

## Query / Code Blocks

```sql
CREATE DATABASE IF NOT EXISTS app_db;
USE app_db;

CREATE TABLE IF NOT EXISTS users (
  user_id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  last_name VARCHAR(150) NOT NULL,
  email VARCHAR(255) NULL,
  age INT NULL,
  created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

## Performance / Optimization Notes

- Keep high-cardinality identity fields indexed through primary keys.
- Use fixed intent in column names (`created_at`, `user_id`) to simplify query plan review and tooling.
