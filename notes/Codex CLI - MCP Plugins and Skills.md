---
notebook:
  - "[[Codex]]"
tags:
  - guide
---

# Codex CLI - MCP Plugins and Skills

Back to [[Codex CLI Fundamentals]].

MCP servers give Codex extra tools, such as docs, GitHub, browsers, databases, or custom services.

Manage MCP servers:

```bash
codex mcp list
codex mcp get <name>
codex mcp add <name> ...
codex mcp remove <name>
codex mcp login <name>
codex mcp logout <name>
```

## Enable MCPs Only For Specific Sessions

To avoid bloating every Codex session, keep optional MCP servers registered but disabled in `~/.codex/config.toml`:

```toml
[mcp_servers.react-grab-mcp]
enabled = false
command = "npx"
args = ["-y", "@react-grab/mcp", "--stdio"]
```

Then enable that MCP only for the session that needs it:

```bash
codex -c 'mcp_servers.react-grab-mcp.enabled=true'
```

For a one-off non-interactive task:

```bash
codex exec -c 'mcp_servers.react-grab-mcp.enabled=true' "inspect this React UI"
```

You can also disable a normally enabled MCP for a specific session:

```bash
codex -c 'mcp_servers.context7.enabled=false'
```

This keeps the default Codex context lean while still making specialized tools available when the task calls for them.

Plugins package capabilities for Codex. Skills are local workflow instructions.

Skills are useful for repeated tasks like:

- Fixing GitHub CI.
- Addressing pull request comments.
- Working with Obsidian Markdown.
- Creating diagrams.
- Reading PDFs.
