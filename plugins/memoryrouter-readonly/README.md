# MemoryRouter (Read Only)

Least-privilege, model-directed recall for Claude Cowork and Claude Code. OAuth is pinned to `memories:read`, so the server rejects write/delete calls; the package also contains no remember or forget workflow. The current Cowork package installs no deterministic capture hook.

## Install

In Claude Code:

```
/plugin marketplace add John-Rood/memoryrouter-claude-plugin
/plugin install memoryrouter-readonly@memoryrouter
```

Then run `/mcp` and complete MemoryRouter OAuth. The plugin connects to `https://mcp.memoryrouter.ai/mcp` and requests only `memories:read`.

## Commands

- `/memoryrouter-readonly:memory-scope personal|project <handle>|org <handle>|show|clear`
- `/memoryrouter-readonly:recall <topic> [--legacy]`
- `/memoryrouter-readonly:memory-status`
- `/memoryrouter-readonly:memory-vault show|switch`
- `/memoryrouter-readonly:memory-help`

Do not install this alongside the read/write plugin: both target the same endpoint, and host duplicate-resolution may keep only one configuration. Disconnect any prior MemoryRouter OAuth grant before switching modes so the narrower scope is actually re-consented.

See `INSTALL.md` and `COMPATIBILITY.md` inside this package.
