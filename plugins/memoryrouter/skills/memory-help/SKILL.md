---
name: memory-help
description: This skill should be used when the user invokes /memory-help or asks how to use the MemoryRouter plugin commands, scopes, vault selection, read-only mode, or current limitations.
disable-model-invocation: true
metadata:
  version: "2.0.0"
---

# MemoryRouter Help

Show this concise command guide:

- `/memoryrouter:memory-scope personal|project <handle>|org <handle>|show|clear`
- `/memoryrouter:recall <topic> [--legacy]`
- `/memoryrouter:remember <durable fact or decision>`
- `/memoryrouter:memory-status`
- `/memoryrouter:forget <topic or real memory id>`
- `/memoryrouter:memory-vault show|switch`

Explain that Cowork memory behavior is model-directed and this MemoryRouter package installs no deterministic capture hook. Writes require an explicit user request or approval, an explicit scope, and `memories:write`. The current server supports modern `server/discover`, search, store, status, resources, and separately authorized full-vault deletion; it does not expose per-memory deletion or hard project isolation, so item curation uses the dashboard and strict isolation uses separate vaults.
