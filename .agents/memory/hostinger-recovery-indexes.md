---
name: Hostinger recovery archive indexes
description: SQLite recovery archives may preserve rows and tables without source indexes.
---

When the Hostinger builder falls back to a recovery SQLite archive, do not assume source indexes exist; archive preparation must remain valid without them.

**Why:** A damaged source index can trigger recovery even when the required table rows are readable, and `ON CONFLICT` statements then fail if the recovery copy omitted the unique constraint.

**How to apply:** Prefer explicit update-then-insert logic or recreate required indexes before any archive-only metadata update. Never rewrite the source database as part of archive recovery.