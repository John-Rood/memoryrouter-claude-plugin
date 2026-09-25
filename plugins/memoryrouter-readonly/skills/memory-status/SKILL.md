---
name: memory-status
description: This skill should be used when the user invokes /memory-status or asks whether MemoryRouter is connected, which vault/scope is active, what permissions are available, or which MCP version/capabilities are present.
disable-model-invocation: true
metadata:
  version: "2.0.0"
---

# Memory Status

Produce a read-only status report. Never test status by writing or deleting data.

Report:

- Connector: connected, authentication required, offline, or unknown.
- OAuth-selected vault: display only a server-provided name or masked identifier; otherwise say “selected during OAuth; name not exposed.”
- Active conversation scope: exact handle or **unset**. State that it does not reliably carry to new conversations.
- OAuth mode: this package requests only `memories:read`; if the host exposes granted scopes, verify that value. Catalog visibility does not grant write/delete authority.
- Capabilities actually visible: `search_memories`/`search`, `store_memory`, `memory_status`, `forget_all_memories`, and vault resources; state that write/delete calls are forbidden in this mode.
- Protocol generation: modern `2026-07-28` when the host exposes it, otherwise the negotiated handshake-era version.
- Scope mode: current `MR_SCOPE_V1` behavioral filtering; native project handles are not exposed.
- Last operation failure in this conversation, if any.

Use `memory_status`; otherwise read `memory://vault/stats` when resources are exposed. If no status capability is available, report tool visibility only. State plainly that per-memory deletion and native handles are absent.
