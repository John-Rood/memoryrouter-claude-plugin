---
name: memory-help
description: This skill should be used when the user invokes /memory-help or asks how to use the MemoryRouter plugin commands, scopes, vault selection, read-only mode, or current limitations.
disable-model-invocation: true
metadata:
  version: "2.0.0"
---

# MemoryRouter Help

Show this concise command guide:

- `/memoryrouter-readonly:memory-scope personal|project <handle>|org <handle>|show|clear`
- `/memoryrouter-readonly:recall <topic> [--legacy]`
- `/memoryrouter-readonly:memory-status`
- `/memoryrouter-readonly:memory-vault show|switch`

Explain that Cowork memory behavior is model-directed and this MemoryRouter package installs no deterministic capture hook. This read-only package requests only `memories:read`; server-enforced OAuth scope, not prose, prevents writes and deletion. The current server lacks native project handles and per-memory deletion, so recall uses exact scope markers for behavioral filtering, strict isolation uses separate vaults, and item curation uses the dashboard.
