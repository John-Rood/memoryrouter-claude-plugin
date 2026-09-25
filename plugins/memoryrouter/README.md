# MemoryRouter for Claude

Claude starts every session cold: it forgets what you told it yesterday and loses context after compaction. MemoryRouter gives Claude one persistent memory vault that also works with ChatGPT, Cursor, Codex, and any MCP client. 14 days free, then $20 a month, cancel anytime.

Portable long-term memory for Claude Cowork, claude.ai chat, and Claude Code through the hosted MemoryRouter MCP connector. This plugin bundles the connector plus explicit workflows for recall, capture, status, deletion, logical scope, and OAuth vault selection.

## Install

In Claude Code:

```
/plugin marketplace add John-Rood/memoryrouter-claude-plugin
/plugin install memoryrouter@memoryrouter
```

Then run `/mcp` and complete MemoryRouter OAuth. The plugin connects to `https://mcp.memoryrouter.ai/mcp`.

## One-click flow

1. Install and enable the plugin.
2. Claude opens MemoryRouter OAuth. Sign in with GitHub or Google and choose a vault.
3. Set a scope in the conversation: `/memoryrouter:memory-scope personal` or `/memoryrouter:memory-scope project <handle>`.
4. Start with “Use MemoryRouter to show the profile I transferred from ChatGPT, then continue from there.” Then ask Claude explicitly to check MemoryRouter whenever recall matters. Ask it to remember a concise fact, or approve an exact memory it proposes, before any save.

## Commands

| Command | Purpose |
|---|---|
| `/memoryrouter:memory-scope ...` | Set/show/clear the conversation-local personal/project/org handle |
| `/memoryrouter:recall <topic>` | Scoped recall with compact provenance |
| `/memoryrouter:remember <fact>` | Scoped, concise write; refuses ambiguous or sensitive writes |
| `/memoryrouter:memory-status` | Read-only connector/vault/scope/capability report |
| `/memoryrouter:forget <topic>` | Dashboard guidance for one item; guarded full-vault deletion only on an explicit erase-all request |
| `/memoryrouter:memory-vault show|switch` | Show vault info or guide OAuth reconnection |
| `/memoryrouter:memory-help` | Usage and limitations |

Claude namespaces plugin skills. In some Cowork UI versions, type `/` and select the skill by its readable title rather than typing the full name.

## Permission model

This plugin pins OAuth to `memories:read memories:write`. Use the separate `memoryrouter-readonly` plugin for least privilege. Do not install both at once.

## Important platform limit

The current MemoryRouter Cowork package installs no deterministic Claude Code-style prompt/stop/compaction capture hook. The model still chooses whether and when to call connector tools, so recall and saving are not guaranteed on every turn. Saving requires an explicit user request or explicit approval of the exact concise memory.

The production MCP server supports `2026-07-28` `server/discover` plus handshake-era protocol versions. Its current catalog includes `search_memories`, `date_search_memories`, `inspect_memory`, `store_memory`, `memory_status`, `delete_memories`, `forget_all_memories`, the reflection tools, and the `search` compatibility alias, plus vault stats/recent resources. Deletion tools require the separate `memories:delete` scope, which this plugin does not request. The server has no native project handles. This package uses exact scope envelopes as behavioral filtering; strict isolation requires separate OAuth-selected vaults.

See `INSTALL.md` and `COMPATIBILITY.md`.
