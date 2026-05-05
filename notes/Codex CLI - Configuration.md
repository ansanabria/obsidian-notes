---
notebook:
  - "[[Codex]]"
tags:
  - guide
---

# Codex CLI - Configuration

Back to [[Codex CLI Fundamentals]].

Persistent config lives at:

```bash
~/.codex/config.toml
```

Override config per command:

```bash
codex -c model='"gpt-5.5"'
codex -c shell_environment_policy.inherit=all
```

Use profiles for reusable modes:

```bash
codex --profile work
codex --profile review
```

Common config areas:

- Model.
- Sandbox mode.
- Approval policy.
- Writable roots.
- Environment inheritance.
- MCP servers.
- Plugins and skills.
