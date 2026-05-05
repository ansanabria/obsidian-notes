---
notebook:
  - "[[Codex]]"
tags:
  - guide
---

# Codex CLI - Core Modes

Back to [[Codex CLI Fundamentals]].

## Interactive

```bash
codex
```

Best for iterative work where you want to steer the agent.

## One-Shot Prompt

```bash
codex "summarize this repository"
```

Starts an interactive session with an initial task.

## Non-Interactive

```bash
codex exec "summarize the public API"
```

Best for automation, reports, and tasks that should run and exit.

## Review

```bash
codex review --uncommitted
codex review --base main
codex review --commit <sha>
```

Best for finding bugs, regressions, risky behavior, and missing tests.
