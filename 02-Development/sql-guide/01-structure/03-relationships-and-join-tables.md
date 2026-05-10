# SQL Structure: Relationships and Join Tables

## Architecture / Rationale

Relational consistency requires explicit foreign keys and controlled join-table uniqueness.

Pattern coverage:
- 1:1 via `UNIQUE` foreign key.
- 1:N via standard foreign key.
- N:M via join table plus composite unique constraint.

## Query / Code Blocks

```sql
CREATE TABLE IF NOT EXISTS companies (
  company_id INT AUTO_INCREMENT PRIMARY KEY,
  company_name VARCHAR(150) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS users (
  user_id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  company_id INT NULL,
  CONSTRAINT fk_users_company FOREIGN KEY (company_id) REFERENCES companies(company_id)
);

CREATE TABLE IF NOT EXISTS dni (
  dni_id INT AUTO_INCREMENT PRIMARY KEY,
  dni_number BIGINT NOT NULL UNIQUE,
  user_id INT NOT NULL UNIQUE,
  CONSTRAINT fk_dni_user FOREIGN KEY (user_id) REFERENCES users(user_id)
);

CREATE TABLE IF NOT EXISTS languages (
  language_id INT AUTO_INCREMENT PRIMARY KEY,
  language_name VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS users_languages (
  users_languages_id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT NOT NULL,
  language_id INT NOT NULL,
  CONSTRAINT fk_ul_user FOREIGN KEY (user_id) REFERENCES users(user_id),
  CONSTRAINT fk_ul_language FOREIGN KEY (language_id) REFERENCES languages(language_id),
  CONSTRAINT uq_ul_user_language UNIQUE (user_id, language_id)
);
```

## Performance / Optimization Notes

- Foreign keys protect integrity and improve join selectivity assumptions.
- Composite uniqueness on join tables prevents duplicate edges and reduces read-side deduplication.
- Keep foreign key types identical across parent and child columns to avoid planner penalties.
