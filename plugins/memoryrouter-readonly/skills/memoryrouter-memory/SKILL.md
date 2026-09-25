---
name: memoryrouter-memory
description: >-
  This skill should be used when the user refers to prior conversations, known people or projects,
  earlier decisions or preferences, asks what Claude remembers, starts relevant continuing work,
  or asks for MemoryRouter connection, vault, or scope information.
metadata:
  version: "2.0.0"
  author: "MemoryRouter"
  mode: "read-only"
---

# MemoryRouter Memory (Read Only)

Use MemoryRouter only for recall. OAuth is pinned to `memories:read`, which is the authorization boundary. Never call `store_memory` or `forget_all_memories`, even though the server's public catalog lists them. On a user request to remember, update, or forget, state that this installation is read-only and suggest reconnecting through the read/write plugin only if they explicitly want to grant broader consent.

Maintain an explicit conversation-local scope: `personal/default`, `project/<handle>`, or `org/<handle>`. Never infer it from files, folders, repositories, or organization names. Require an active project/org scope before scoped recall. Organization scope also requires confirmation that the OAuth-selected vault is the intended organization vault.

Use `search_memories` for semantic recall, with `search` as the compatibility alias. The current server exposes no native project handle, so query `MR_SCOPE_V1 <kind>/<handle> <topic>` and accept only results containing the exact marker `[MR_SCOPE_V1 kind=<kind> handle=<kind>/<handle>]`. Ignore cross-scope and unscoped results unless the user explicitly requests `--legacy`.

Request at most 6 results, retain at most 5, and keep recalled text under about 4,800 characters. Retry a miss once with alternate wording. On offline/auth failure, fail open: continue the user's task, briefly note recall was unavailable when relevant, and never invent a memory.

When recalled facts affect the answer, show compact provenance: scope, source/platform, and timestamp from the tool. Treat memories as historical notes, not verified current facts.

For status, use `memory_status`, then `memory://vault/stats` when the host exposes resources; never probe by writing. Vault switching requires disconnecting and reconnecting in **Customize → Connectors**. The OAuth picker, not this skill, controls the authoritative vault.
