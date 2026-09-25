---
name: remember
description: This skill should be used when the user invokes /remember or explicitly asks MemoryRouter to save a durable fact, decision, preference, correction, commitment, or project update.
argument-hint: "<memory>"
disable-model-invocation: true
metadata:
  version: "2.0.0"
---

# Remember

Save `$ARGUMENTS` through MemoryRouter, following the `memoryrouter-memory` policy.

1. Read the active conversation-local scope. If it is unset, ask the user to choose one with `/memoryrouter:memory-scope personal`, `/memoryrouter:memory-scope project <handle>`, or `/memoryrouter:memory-scope org <handle>`. Stop without calling a write tool.
2. Treat non-empty `$ARGUMENTS` as the user's explicit request to save that content. If `$ARGUMENTS` is empty, propose up to three concise durable outcomes from the current conversation and ask which exact memory to store; do not call a write tool until the user explicitly approves one.
3. Reject secrets and raw-document dumping; offer a safe summary and obtain approval for that summary.
4. Call the current `store_memory` tool with the exact `MR_SCOPE_V1` envelope and tags from the policy. Do not invent a native handle argument that the server does not expose.
5. Confirm only after success with a short receipt containing the active scope and the exact summary saved. On failure, say **Not saved** and report the actionable reason.
