---
name: forget
description: This skill should be used when the user invokes /forget or explicitly requests deletion of MemoryRouter memories.
argument-hint: "<topic-or-full-vault-request>"
disable-model-invocation: true
metadata:
  version: "2.0.0"
---

# Forget

Do not conflate item curation with irreversible full-vault deletion.

## One memory or topic

1. If the user asks to forget one item, optionally use `search_memories` to help identify it.
2. Explain: “This MemoryRouter plugin does not request delete permission for single memories. Nothing was deleted.”
3. Direct the user to https://app.memoryrouter.ai for item-level curation.
4. Never create a tombstone memory and never pass a store receipt to a delete tool.

## Every memory in the connected vault

Use `forget_all_memories` only when all of these conditions are true:

1. The user explicitly requests permanent deletion of **every** memory in the OAuth-selected vault; “forget that” or a topic is not enough.
2. Warn that this action is irreversible and affects the whole connected vault.
3. Require the user to provide the exact phrase `DELETE ALL MEMORIES` after the warning. Do not reuse earlier or approximate confirmation.
4. Confirm `memories:delete` is granted. Read/write permission does not imply delete permission.
5. Require the destructive host confirmation, call `forget_all_memories` with that exact phrase, and report success only from the tool result.

In read-only mode or on 403/insufficient-scope, stop. Never widen OAuth permissions without reconnecting and obtaining the user's consent.
