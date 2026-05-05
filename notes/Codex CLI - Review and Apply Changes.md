---
notebook:
  - "[[Codex]]"
tags:
  - guide
---

# Codex CLI - Review and Apply Changes

Back to [[Codex CLI Fundamentals]].

Inspect changes yourself:

```bash
git status
git diff
git diff --stat
```

Apply the latest Codex-produced patch:

```bash
codex apply
```

Ask Codex to review local changes:

```bash
codex review --uncommitted
```

Simple final loop:

```bash
git status
git diff
codex review --uncommitted
npm test
git add .
git commit -m "..."
```
