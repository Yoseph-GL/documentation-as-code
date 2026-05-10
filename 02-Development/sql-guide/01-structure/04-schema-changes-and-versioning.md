# SQL Structure: Schema Changes and Versioning

## Architecture / Rationale

Schema evolution must be explicit, reversible when possible, and separated from application deploy risk.

Change policy:
- Prefer additive changes first.
- Backfill and validate before destructive operations.
- Track schema operations in versioned SQL migration files.

## Query / Code Blocks

```sql
-- Additive change
ALTER TABLE users
  ADD COLUMN status VARCHAR(30) NOT NULL DEFAULT 'active';

-- Rename column (engine/version dependent behavior)
ALTER TABLE users
  RENAME COLUMN status TO account_status;

-- Controlled column removal (only after validation and dependency checks)
ALTER TABLE users
  DROP COLUMN account_status;
```

```bash
#!/usr/bin/env bash
# ./02-Development/sql-guide/migrate.sh
set -euo pipefail

usage() {
  echo "Usage: $0 <migration.sql> [--run]" >&2
  exit 2
}

migration_file="${1:-}"
run_flag="${2:-}"

[[ -n "${migration_file}" ]] || usage
[[ -f "${migration_file}" ]] || { echo "Migration file not found: ${migration_file}" >&2; exit 2; }
[[ "${run_flag}" == "--run" ]] || { echo "Refusing schema change without --run" >&2; exit 3; }

mysql --host="${DB_HOST:-127.0.0.1}" --user="${DB_USER:-root}" --password="${DB_PASS:-}" "${DB_NAME:-app_db}" < "${migration_file}"
```

## Performance / Optimization Notes

- Apply index changes during controlled windows for large tables.
- Avoid combining many high-impact DDL operations into a single migration unit.
- Validate query plans before and after schema changes on critical workloads.
