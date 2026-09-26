# Security Policy

## Reporting a vulnerability

Email **security@memoryrouter.ai** with a description of the issue, steps to reproduce, and the affected component (this plugin repository, the MCP server at `https://mcp.memoryrouter.ai/mcp`, or the OAuth server at `https://auth.memoryrouter.ai`). Please do not open a public GitHub issue for security reports.

We acknowledge reports within 3 business days and keep you updated until the issue is resolved.

## Scope

- The plugin manifests, `.mcp.json` files, and skills in this repository
- The hosted MemoryRouter MCP server and OAuth server these plugins connect to

## How the plugins handle data

- The plugins contain no hooks, scripts, binaries, or package installs. They are connector configuration plus Markdown skills.
- Authentication uses OAuth 2.1 with PKCE. No API key or token is stored in any file in this repository.
- The `memoryrouter` plugin requests `memories:read memories:write`. The `memoryrouter-readonly` plugin requests `memories:read` only. Neither requests `memories:delete`.
- Memories are sent only when the user asks Claude to remember something or approves the exact memory.

More detail: https://memoryrouter.ai/security and https://memoryrouter.ai/privacy.

## Supported versions

Only the latest release on the `main` branch is supported.
