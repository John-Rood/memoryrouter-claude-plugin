# MCP compatibility

The production endpoint supports modern MCP `2026-07-28` and handshake-era versions `2025-11-25`, `2025-06-18`, and `2025-03-26` over Streamable HTTP.

| Capability | Current server | Plugin behavior |
|---|---|---|
| Discovery | `server/discover` on `2026-07-28`; `initialize` for legacy clients | Uses server instructions and advertised versions |
| Search | `search_memories`, `date_search_memories`, `inspect_memory`; `search` compatibility alias | Supported with `memories:read` |
| Write | `store_memory` | Only after explicit request/approval and with `memories:write` |
| Status | `memory_status`; `memory://vault/stats` and `memory://vault/recent` | Read-only |
| Item delete | `delete_memories` (requires `memories:delete`) | Scope not requested by this plugin; direct to dashboard; never fake deletion |
| Full-vault delete | `forget_all_memories` | Requires `memories:delete`, warning, and exact phrase |
| Project/org handle | Not in tool schema | Exact `MR_SCOPE_V1` envelope; behavioral partition only |
| Read-only | Server OAuth scope enforcement | `memoryrouter-readonly` requests only `memories:read` |

Modern requests require `MCP-Protocol-Version`, `Mcp-Method`, matching request `_meta`, and `Mcp-Name` on named operations. The release live probe sends those fields and checks the exact catalog.

Compatibility markers reduce accidental cross-project use but are not a server-enforced authorization boundary. Use a separate OAuth-selected vault for hard isolation. Store receipts are not deletion identifiers.
