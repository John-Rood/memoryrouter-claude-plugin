---
name: memory-vault
description: This skill should be used when the user invokes /memory-vault or asks which MemoryRouter vault is connected, how to select another vault, or how OAuth vault choice works.
argument-hint: "show | switch"
disable-model-invocation: true
metadata:
  version: "2.0.0"
---

# Memory Vault

For `show` or no arguments, use a read-only status capability if available and show only server-provided vault information. Do not expose a raw memory key or token.

For `switch`, explain that a skill cannot alter OAuth credentials. In Claude, open **Customize → Connectors → MemoryRouter**, disconnect, reconnect, and choose the intended vault in the MemoryRouter OAuth picker. Then re-enable MemoryRouter for the conversation and run `/memoryrouter:memory-status`.

Warn that changing the OAuth vault changes the authoritative data boundary. Clear the conversation-local memory scope after a vault switch and require the user to select it again.
