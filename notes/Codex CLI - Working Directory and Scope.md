---
notebook:
  - "[[Codex]]"
tags:
  - guide
---

# Codex CLI - Working Directory and Scope

Back to [[Codex CLI Fundamentals]].

Codex works from a root directory. Usually this is your current directory or Git repository root.

Set it explicitly:

```bash
codex --cd ~/project
codex exec --cd ~/project "find the database migrations"
```

Add another writable directory:

```bash
codex --add-dir ../shared-library
```

Good scope prompt:

```text
In src/auth, add retry handling to token refresh. Keep the public API unchanged. Run the auth tests.
```
