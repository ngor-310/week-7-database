# PostgreSQL Disaster Recovery and Advanced Patterns Lab

This repository documents a comprehensive hands-on PostgreSQL lab covering physical backups, WAL archiving, Point-in-Time Recovery (PITR), streaming replication, audit logging triggers, recursive CTE tree queries, versioned migrations (Flyway), and least-privilege security.

---

## Part 1: Disaster Recovery & Replication

### Step 1: Take and Verify a Logical Backup
- Created a backup directory and generated a custom-compressed logical dump (`-Fc`) of the `bootcamp` database.
- Verified backup integrity using `pg_restore --list` and test-restored it into a verification database (`bootcamp_check`).

```bash
mkdir -p ~/backups
pg_dump -Fc -f ~/backups/bootcamp.dump bootcamp
pg_restore --list ~/backups/bootcamp.dump | head
createdb bootcamp_check && pg_restore -d bootcamp_check ~/backups/bootcamp.dump
