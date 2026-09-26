# Changelog

All notable changes to this marketplace and its plugins are documented here. Versions follow [Semantic Versioning](https://semver.org/).

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
