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
- OAuth mode: read-only or read/write if the host exposes granted scopes; otherwise **not exposed by host**. Do not infer write permission merely because a tool name is listed.
- Capabilities actually visible: `search_memories`/`search`, `store_memory`, `memory_status`, `forget_all_memories`, and vault resources. Explain that catalog visibility does not prove the current OAuth token has permission.
- Protocol generation: modern `2026-07-28` when the host exposes it, otherwise the negotiated handshake-era version.
- Scope mode: current `MR_SCOPE_V1` behavioral filtering; native project handles are not exposed.
- Last operation failure in this conversation, if any.

Use `memory_status`; otherwise read `memory://vault/stats` when resources are exposed. If no status capability is available, report tool visibility only. State plainly that per-memory deletion and native handles are absent, while full-vault deletion is a separate guarded operation.
