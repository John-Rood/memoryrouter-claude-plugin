# Changelog

All notable changes to this marketplace and its plugins are documented here. Versions follow [Semantic Versioning](https://semver.org/).

## 2.1.0 (2026-11-04)

- The memory skill now carries MemoryRouter's universal "when to use memory" instructions, the same text the hosted MCP server sends every client: search before responding to each new message, save useful details after it, and never mention either unless asked. Read-only installs follow the retrieve half only.
- Mapped the instructions to the real tools: `search_memories` with all tiers by default, `inspect_memory` for sources, `date_search_memories` for time windows, `store_memory` one memory per call (there is no update tool). Credentials and sensitive identifiers are never saved, and Claude can ask you to confirm each save.

## 2.0.2 (2026-09-26)

- Added a MemoryRouter icon to the marketplace and to each plugin folder.
- Added `SECURITY.md`, this changelog, and a plugin-folder disclosure of everything the plugins run, send, and fetch.
- Added an install screenshot to the README.
- Completed plugin and marketplace metadata (author URL, keywords, category).

## 2.0.1 (2026-09-25)

- Published the marketplace publicly on GitHub.
- Corrected the forget workflow text: the plugins never request delete permission for single memories and point to the dashboard for item-level curation.
- Verified `claude plugin validate` passes and the plugin installs from GitHub and connects to `https://mcp.memoryrouter.ai/mcp`.

## 2.0.0 (2026-08-05)

- Two plugins: `memoryrouter` (read and write) and `memoryrouter-readonly` (read only), both backed by the hosted MemoryRouter MCP connector over OAuth.
- Skills for recall, remember, memory status, conversation scope, vault selection, and guarded forget.
