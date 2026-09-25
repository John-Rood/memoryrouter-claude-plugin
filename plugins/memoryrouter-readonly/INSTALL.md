# Install, upgrade, and uninstall

## Claude Cowork / claude.ai

Open **Cowork → Customize → Plugins → Add** and upload this plugin ZIP, or install it from an administrator-provided marketplace. Enable it, complete MemoryRouter OAuth, select a vault, then set a conversation scope.

Remote connector traffic originates from Anthropic's cloud. `https://mcp.memoryrouter.ai/mcp` must remain publicly reachable.

## Claude Code

Add this repository as a marketplace, then install the plugin:

```
/plugin marketplace add John-Rood/memoryrouter-claude-plugin
/plugin install memoryrouter-readonly@memoryrouter
```

Run `/mcp`, select the MemoryRouter server, and complete OAuth in the browser. The plugin connects to `https://mcp.memoryrouter.ai/mcp`.

## Upgrade

Install/upload the newer ZIP with the same plugin name. Organization manual marketplaces replace by plugin name; GitHub-synced marketplaces require a version bump and sync. Reconnect OAuth when changing read-only/read-write mode or when scopes change.

After upgrading, run `/memoryrouter:memory-status`. Existing unscoped memories remain available only through explicit `--legacy` recall until migrated.

## Uninstall

Disable/uninstall the plugin from **Customize → Plugins**, then disconnect MemoryRouter under **Customize → Connectors** to revoke the Claude-side connection. To revoke third-party authorization at the source, use MemoryRouter account/security settings. Uninstalling the plugin does not delete vault data.
