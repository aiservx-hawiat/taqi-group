---
name: Workflow refresh after installs
description: Environment-specific behavior observed after dependency installation in this workspace.
---

After a dependency installation changes workspace packages, restart every affected managed workflow before validating the app. A running process can retain a deleted working directory and continue serving its pre-install bundle, making newly added routes or dependencies appear missing.

**Why:** The workspace package tree can be replaced during installation while an existing managed process remains alive. Its logs may still look healthy even though it is running stale code.

**How to apply:** Treat workflow restart as part of dependency-install verification, then check logs and exercise the affected endpoint or page.