---
name: memory-scope
description: This skill should be used when the user invokes /memory-scope to select, inspect, or clear the explicit personal, project, or organization memory handle for the current conversation.
argument-hint: "personal | project <handle> | org <handle> | show | clear"
disable-model-invocation: true
metadata:
  version: "2.0.0"
---

# Memory Scope

Interpret `$ARGUMENTS` exactly:

- `personal` → set `personal/default`.
- `project <handle>` → normalize the handle to lowercase and set `project/<handle>`.
- `org <handle>` → normalize and, before setting, ask the user to confirm the OAuth-selected vault is the intended team/org vault.
- `show` or empty → show the active scope without changing it.
- `clear` → clear the active scope for this conversation.

Valid handles are 2 to 64 characters using only lowercase letters, numbers, `.`, `_`, and `-`. Reject spaces, paths, URLs, secrets, and inferred names. Never derive a handle from local folders, repositories, files, or previous memories.

Display a receipt:

```text
Memory scope: project/example
Lifetime: this conversation (set again in a new conversation)
Write policy: explicit scope required
Boundary: server-enforced when native handles exist; compatibility marker otherwise
```

Do not call a write tool merely to remember the selected scope.
