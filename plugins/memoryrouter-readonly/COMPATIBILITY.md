# MCP compatibility: read only

The production endpoint supports modern MCP `2026-07-28` and handshake-era versions `2025-11-25`, `2025-06-18`, and `2025-03-26` over Streamable HTTP.

| Capability | Current server | Read-only plugin behavior |
|---|---|---|
| Discovery | `server/discover` on `2026-07-28`; `initialize` for legacy clients | Uses server instructions and advertised versions |
| Search | `search_memories`, `date_search_memories`, `inspect_memory`; `search` compatibility alias | Allowed with `memories:read` |
| Status | `memory_status`; `memory://vault/stats` and `memory://vault/recent` | Allowed with `memories:read` |
| Write | `store_memory` | Forbidden by missing `memories:write` scope and package policy |
| Item delete | `delete_memories` (requires `memories:delete`) | Forbidden by missing scope; direct to dashboard |
| Full-vault delete | `forget_all_memories` | Forbidden by missing `memories:delete` scope and package policy |
| Project/org handle | Not in tool schema | Exact `MR_SCOPE_V1` filtering; behavioral partition only |

Modern requests require `MCP-Protocol-Version`, `Mcp-Method`, matching request `_meta`, and `Mcp-Name` on named operations. OAuth scope enforcement, not skill prose, is the security boundary. Use a separate OAuth-selected vault for hard project or organization isolation.
