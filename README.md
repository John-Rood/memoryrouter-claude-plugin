# MemoryRouter plugins for Claude

Claude starts every session cold. It forgets what you told it yesterday and loses context after compaction. MemoryRouter gives Claude Code, Claude Cowork, and claude.ai one persistent, user-scoped memory vault that also works with ChatGPT, Cursor, Codex, and any other MCP client.

This repository is a Claude plugin marketplace with two plugins. Both connect to the hosted MemoryRouter MCP server at `https://mcp.memoryrouter.ai/mcp` over OAuth. No API key goes in any file.

| Plugin | OAuth scopes | What it adds |
|---|---|---|
| `memoryrouter` | `memories:read memories:write` | Recall, remember, status, scope, vault, and guarded forget workflows |
| `memoryrouter-readonly` | `memories:read` | Recall, status, scope, and vault workflows with no write path |

Install one of them, not both.

## Install in Claude Code

```
/plugin marketplace add John-Rood/memoryrouter-claude-plugin
/plugin install memoryrouter@memoryrouter
```

For least privilege, install `memoryrouter-readonly@memoryrouter` instead.

Then run `/mcp`, select the MemoryRouter server, and complete OAuth in the browser. Sign in with GitHub or Google and pick the vault Claude should use.

## Install in Claude Cowork or claude.ai

Open **Customize > Plugins > Add** and upload a ZIP of the plugin folder (`plugins/memoryrouter` or `plugins/memoryrouter-readonly`), or install it from an administrator-provided marketplace. Enable it, complete MemoryRouter OAuth, and choose a vault.

## Use it

- `/memoryrouter:memory-scope personal` or `/memoryrouter:memory-scope project <handle>` sets the scope for the conversation.
- `/memoryrouter:recall <topic>` searches the vault and shows where each result came from.
- `/memoryrouter:remember <fact>` saves one concise memory after you ask or approve it.
- `/memoryrouter:memory-status` reports the connection, vault, and scope.
- `/memoryrouter:memory-help` explains usage and limits.

Claude decides when to call memory tools, so recall is not guaranteed on every turn. Ask it to check MemoryRouter when earlier context matters. For automatic per-turn recall and capture in Claude Code, use the hook-based `memoryrouter-claude` package described at https://memoryrouter.ai/claude-code.

## Data and permissions

Memories are stored in your MemoryRouter vault and are only reachable with a token you grant through OAuth. The standard plugins never request `memories:delete`, so they cannot delete memories. Item-level curation and deletion live in the dashboard at https://app.memoryrouter.ai. Privacy policy: https://memoryrouter.ai/privacy.

## Pricing

MemoryRouter is free for 14 days, then $20 a month. Cancel anytime. See https://memoryrouter.ai/pricing.

## Links

- Website: https://memoryrouter.ai
- MCP setup guide: https://memoryrouter.ai/mcp
- Docs: https://docs.memoryrouter.ai/mcp
- Support: https://memoryrouter.ai/support or hello@memoryrouter.ai

## License

MIT
