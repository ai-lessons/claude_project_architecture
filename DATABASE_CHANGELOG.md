# Database Changelog

**Project:** `{{PROJECT_NAME}}`  
**Database:** `{{DB_ENGINE}}` (e.g., PostgreSQL, MySQL, SQLite)  
**Last Updated:** YYYY-MM-DD

> **Purpose:** This file tracks the evolution of database schema.  
> **For Claude Code:** Read this to understand current DB structure without querying the database.  
> **Update:** After every migration, update the "Current Schema" section and add entry to "Migration History".

---

## 🎯 Quick Reference

**Current Schema Version:** `{{CURRENT_VERSION}}`  
**Migrations Location:** `{{MIGRATIONS_DIR}}` (e.g., `supabase/migrations/`, `prisma/migrations/`, `db/migrations/`)  
**Total Tables:** `{{TABLE_COUNT}}`

---

## 📊 Current Schema

> This section reflects the **current state** of the database as of the last update date above.

### Table: `{{table_name_1}}`

**Purpose:** Brief description of what this table stores

| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| id | uuid / bigint / int | NO | gen_random_uuid() / auto_increment | Primary key |
| created_at | timestamp | NO | now() | Record creation time |
| updated_at | timestamp | NO | now() | Last update time |
| user_id | uuid | NO | - | Foreign key to users table |
| name | text / varchar(255) | NO | - | Entity name |
| description | text | YES | NULL | Optional description |
| metadata | jsonb / json | YES | NULL | Flexible metadata storage |
| status | text / enum | NO | 'active' | Current status |

**Indexes:**
- `PRIMARY KEY (id)`
- `INDEX idx_{{table_name_1}}_user_id ON {{table_name_1}}(user_id)`
- `INDEX idx_{{table_name_1}}_status ON {{table_name_1}}(status)`
- `GIN INDEX idx_{{table_name_1}}_metadata ON {{table_name_1}}(metadata)` _(if JSONB)_

**Foreign Keys:**
- `user_id` REFERENCES `users(id)` ON DELETE CASCADE

**RLS Policies:** _(if using Supabase or similar)_
- `enable_read_own`: Users can read their own records
- `enable_insert_own`: Users can insert their own records
- `enable_update_own`: Users can update their own records
- `enable_delete_own`: Users can delete their own records

**Triggers:**
- `update_{{table_name_1}}_updated_at`: Auto-update `updated_at` on row modification

---

### Table: `{{table_name_2}}`

**Purpose:** Brief description

| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| {{table_name_1}}_id | uuid | NO | - | Foreign key |
| name | text | NO | - | Item name |
| file_path | text | YES | NULL | Path to associated file |
| file_size | bigint | YES | NULL | File size in bytes |

**Indexes:**
- `PRIMARY KEY (id)`
- `INDEX idx_{{table_name_2}}_{{table_name_1}}_id ON {{table_name_2}}({{table_name_1}}_id)`

**Foreign Keys:**
- `{{table_name_1}}_id` REFERENCES `{{table_name_1}}(id)` ON DELETE CASCADE

---

### Special Data Types

**JSONB Structure Examples:**

```typescript
// metadata column in {{table_name_1}}
interface Metadata {
  tags?: string[];
  settings?: {
    theme: 'light' | 'dark';
    notifications: boolean;
  };
  custom_fields?: Record<string, any>;
}

// Example query:
// SELECT * FROM {{table_name_1}} WHERE metadata @> '{"tags": ["important"]}';
```

---

## 📜 Migration History

> Reverse chronological order (newest first)

### Migration: YYYY-MM-DD - Description of changes

**Version:** `{{VERSION_NUMBER}}`  
**Migration File:** `{{MIGRATION_FILE_PATH}}`  
**Applied:** YYYY-MM-DD HH:MM:SS

**Changes:**
- Added column `{{table_name_1}}.new_column` (type: text, nullable: YES)
- Created index `idx_{{table_name_1}}_new_column` on `{{table_name_1}}(new_column)`
- Updated RLS policies to include new column

**Reason:**
Brief explanation of why this change was needed.

**Rollback:**
```sql
-- To rollback this migration:
DROP INDEX IF EXISTS idx_{{table_name_1}}_new_column;
ALTER TABLE {{table_name_1}} DROP COLUMN IF EXISTS new_column;
```

**Verification:**
```sql
-- Verify the migration:
SELECT column_name, data_type, is_nullable 
FROM information_schema.columns 
WHERE table_name = '{{table_name_1}}' AND column_name = 'new_column';
```

---

### Migration: YYYY-MM-DD - Initial schema

**Version:** `1.0.0`  
**Migration File:** `{{MIGRATIONS_DIR}}/001_initial_schema.sql`  
**Applied:** YYYY-MM-DD HH:MM:SS

**Changes:**
- Created table `{{table_name_1}}`
- Created table `{{table_name_2}}`
- Set up RLS policies
- Created initial indexes

**Reason:**
Initial database setup for the project.

---

## 🔍 Query Patterns & Tips

### Common Queries

**Get records with JSON filtering:**
```sql
-- PostgreSQL JSONB
SELECT * FROM {{table_name_1}} 
WHERE metadata @> '{"status": "active"}';

-- MySQL JSON
SELECT * FROM {{table_name_1}} 
WHERE JSON_EXTRACT(metadata, '$.status') = 'active';
```

**Full-text search (if enabled):**
```sql
-- PostgreSQL
SELECT * FROM {{table_name_1}} 
WHERE to_tsvector('english', name || ' ' || description) 
      @@ to_tsquery('english', 'search_term');
```

**Aggregate with joins:**
```sql
SELECT 
  t1.id,
  t1.name,
  COUNT(t2.id) as item_count
FROM {{table_name_1}} t1
LEFT JOIN {{table_name_2}} t2 ON t2.{{table_name_1}}_id = t1.id
GROUP BY t1.id, t1.name;
```

### Performance Tips

- Use indexes for frequently filtered columns
- GIN indexes for JSONB queries in PostgreSQL
- Avoid `SELECT *` in production queries
- Use EXPLAIN ANALYZE to check query plans

---

## 🛠️ Maintenance Notes

### Scheduled Tasks

**Daily:**
- Automatic backups (configured in infrastructure)

**Weekly:**
- Index maintenance (REINDEX if needed)
- Vacuum analysis (PostgreSQL)

**Monthly:**
- Review slow queries
- Check index usage statistics

### Database Size Monitoring

```sql
-- PostgreSQL: Check table sizes
SELECT 
  schemaname,
  tablename,
  pg_size_pretty(pg_total_relation_size(schemaname||'.'||tablename)) AS size
FROM pg_tables
WHERE schemaname NOT IN ('pg_catalog', 'information_schema')
ORDER BY pg_total_relation_size(schemaname||'.'||tablename) DESC;
```

---

## 📚 Related Documentation

- **PROJECT_ARCHITECTURE.md** — Overall architecture and decisions
- **CLAUDE.md** — Development patterns and guidelines
- **README.md** — Project setup and overview
- **{{MIGRATIONS_DIR}}/README.md** — Migration execution guide (if exists)

---

## ⚠️ Important Notes

### Data Integrity Rules

1. **Never modify schema outside migrations** — Always use migration files
2. **Test migrations in dev/staging first** — Never run untested migrations in production
3. **Keep types in sync** — Update TypeScript/Python types after schema changes
4. **Document breaking changes** — Note in migration history if changes affect existing code

### Security Considerations

- RLS policies enforce row-level security (if applicable)
- Sensitive data should be encrypted at application level
- Use prepared statements to prevent SQL injection
- Regular security audits of database access

---

*Maintain this file after every migration. Last updated: YYYY-MM-DD*
