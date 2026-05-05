---
notebook:
  - "[[Codex]]"
tags:
  - guide
---

# Codex CLI - Sandbox and Approvals

Back to [[Codex CLI Fundamentals]].

Codex has two safety controls:

- Sandbox: what the agent can read, write, or execute.
- Approval policy: when the agent must ask before running commands.

Common sandbox modes:

- `read-only`: inspect only.
- `workspace-write`: edit inside the workspace.
- `danger-full-access`: no sandbox restrictions.

Common approval policies:

- `untrusted`: only trusted commands run without asking.
- `on-request`: agent asks when it needs more access.
- `never`: agent never asks; failures return to the model.

Typical local mode:

```bash
codex --sandbox workspace-write --ask-for-approval on-request
```

Avoid this unless the environment is externally sandboxed:

```bash
codex --dangerously-bypass-approvals-and-sandbox
```
