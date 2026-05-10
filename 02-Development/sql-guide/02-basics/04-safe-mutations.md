# SQL Basics: Safe Mutations

## Architecture / Rationale

Write operations must be auditable and strictly scoped to avoid accidental data loss.

Safety model:
- Explicit column lists on insert.
- Mandatory predicates on update and delete.
- Operator guardrails for state-changing execution.

## Query / Code Blocks

```sql
INSERT INTO users (name, last_name, age, email)
VALUES ('Maria', 'Lopez', 21, 'maria@example.com');

UPDATE users
SET age = 22
WHERE user_id = 11;

DELETE FROM users
WHERE user_id = 11;
```

```bash
#!/usr/bin/env bash
# ./02-Development/sql-guide/run_sql.sh
set -euo pipefail

usage() {
  echo "Usage: $0 <read|write> <sql_file> [--run]" >&2
  exit 2
}

mode="${1:-}"
sql_file="${2:-}"
run_flag="${3:-}"

[[ -n "${mode}" && -n "${sql_file}" ]] || usage
[[ -f "${sql_file}" ]] || { echo "SQL file not found: ${sql_file}" >&2; exit 2; }

case "${mode}" in
  read)
    mysql --host="${DB_HOST:-127.0.0.1}" --user="${DB_USER:-root}" --password="${DB_PASS:-}" "${DB_NAME:-app_db}" < "${sql_file}"
    ;;
  write)
    [[ "${run_flag}" == "--run" ]] || { echo "Refusing write without --run" >&2; exit 3; }
    mysql --host="${DB_HOST:-127.0.0.1}" --user="${DB_USER:-root}" --password="${DB_PASS:-}" "${DB_NAME:-app_db}" < "${sql_file}"
    ;;
  *)
    usage
    ;;
esac
```

## Performance / Optimization Notes

- Use indexed predicates for write targeting to minimize lock scope.
- Keep transaction batches small for predictable replication and rollback behavior.
