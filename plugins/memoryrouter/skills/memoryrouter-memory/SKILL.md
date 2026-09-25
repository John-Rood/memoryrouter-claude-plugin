---
name: memoryrouter-memory
description: >-
  This skill should be used when the user refers to prior conversations, a known person or project,
  earlier decisions or preferences, asks Claude to remember or forget something, starts relevant
  continuing work, or asks for MemoryRouter status, vault, or scope information.
metadata:
  version: "2.0.0"
  author: "MemoryRouter"
---

# MemoryRouter Memory

Use the connected MemoryRouter MCP server as portable long-term memory. This skill coordinates **model-directed** tool use in Claude Cowork; it is not a lifecycle hook and cannot guarantee a call on every turn.

## Primary first-run proof

Lead with: **“Use MemoryRouter to show the profile I transferred from ChatGPT, then continue from there.”** Search the selected MemoryRouter vault for the reviewed profile transferred from ChatGPT, summarize only returned memories with compact receipts or provenance, and ask what the user wants to continue. This is cross-AI recall from MemoryRouter, not direct access to ChatGPT or untransferred private history.

## 1. Establish the active memory scope

Maintain one visible, conversation-local scope before project or organization recall or any write:

- `personal/default`
- `project/<handle>`
- `org/<handle>`

A handle is lowercase, 2 to 64 characters, and contains only letters, numbers, `.`, `_`, or `-`. Never derive a handle from a mounted folder, filename, repository, or guessed company name. The user sets it explicitly with the `memory-scope` skill. Scope does not carry reliably into a new conversation.

If a write is requested and no scope is active, stop and ask the user to choose personal, project, or organization scope. Do not call a write tool. For organization scope, also confirm that the OAuth-selected vault is the intended organization/team vault.

## 2. Resolve server capabilities without pretending

Use the best tool the connected server actually exposes:

| Operation | Current server capability | Behavior |
|---|---|---|
| Search | `search_memories` | Prefer for shared-memory recall; `search` is a compatibility alias |
| Time-window recall | `date_search_memories` | Read-only recall for a date range |
| Write | `store_memory` | Requires `memories:write` plus explicit user request or approval |
| Status | `memory_status` | Read-only status and opaque vault reference |
| Full-vault delete | `forget_all_memories` | Requires `memories:delete` and exact `DELETE ALL MEMORIES` confirmation |
| Resources | `memory://vault/stats`, `memory://vault/recent` | Read-only fallback when the host exposes resources |
| Native project scope | not exposed | use the scoped envelope below |

Never claim a tool exists because this skill mentions it. Per-memory deletion (`delete_memories`) needs the separate `memories:delete` scope, which this plugin does not request; direct item curation to the MemoryRouter dashboard. Never treat a store receipt as a deletion ID.

## 3. Search before relevant work

Search before answering when earlier context could materially change the work: prior decisions, named projects or people, preferences, status, corrections, or phrases such as “as discussed” and “where did we leave off?”

1. Require the relevant active scope for project/org work. Personal preference recall may use `personal/default` only when the work is clearly personal rather than project-specific.
2. If the tool supports a native handle, pass the active handle.
3. Otherwise query for both the exact marker and topic: `MR_SCOPE_V1 <kind>/<handle> <topic>`.
4. Request at most 6 results. Keep at most 5 relevant results and at most about 4,800 characters of recalled text in working context.
5. In compatibility mode, use only results containing the exact marker `[MR_SCOPE_V1 kind=<kind> handle=<kind>/<handle>]`. Ignore unscoped and differently scoped results unless the user explicitly asks for legacy/all-scope recall.
6. If the first search misses, retry once with different wording. Never loop.
7. On timeout, authentication failure, or offline service, continue the task without memory and say briefly that recall was unavailable when it matters. Never invent a memory.

When recalled facts materially affect the answer, show compact provenance: active scope, source/platform, and timestamp supplied by the tool. Describe results as recalled notes, not verified current facts.

## 4. Store concise durable outcomes

Store only after the user explicitly asks to remember something or explicitly approves a proposed concise memory. A meaningful durable outcome, such as a decision, preference, named project status/blocker, role, correction, or commitment, may be proposed, but must not be saved until the user approves it. Do not save routine chatter, transient plans, chain-of-thought, tool logs, or entire transcripts.

Before writing:

- Require a current explicit request or approval for the exact concise content; earlier blanket consent is not enough.
- Require an explicit active scope as above.
- Use a native handle if supported.
- Refuse secrets, passwords, API keys, tokens, private keys, financial account numbers, government identifiers, authentication cookies, or raw confidential documents. Offer to store a non-sensitive summary instead.
- Summarize raw documents to the decision or conclusion; never dump the source document.
- Keep one memory self-contained and normally under 700 characters. Include names and absolute dates where useful.

In compatibility mode, write exactly this envelope:

```text
[MR_SCOPE_V1 kind=<personal|project|org> handle=<kind>/<handle>]
<concise, self-contained memory>
```

Add tags `mr-scope-v1`, `mr-kind-<kind>`, `mr-handle-<normalized-handle>`, and topic tags. Set `source_context` to `Claude Cowork; explicit scope <kind>/<handle>` when available. Confirm only after the tool reports success. If a write fails, say it was not saved; never silently treat it as durable.

## 5. Forget safely

This plugin does not request the `memories:delete` scope that per-memory deletion needs. For a request to forget or curate one item, direct the user to the MemoryRouter dashboard and say that nothing was deleted through Claude. Never use a store call as a “tombstone.”

`forget_all_memories` is a separate, irreversible full-vault operation that cannot delete one item. Standard packages omit delete scope. Call it only when the user explicitly requests deletion of every memory in the OAuth-selected vault, after warning in one turn that the action is permanent and item deletion is not available through this plugin, after the user supplies the exact phrase `DELETE ALL MEMORIES` in a later turn, only with a separate `memories:delete` grant, and only after destructive host confirmation. Never reinterpret “forget that” as consent to erase a vault.

## 6. Vaults and permissions

OAuth chooses the authoritative MemoryRouter vault. Skills cannot switch it. To change vaults, disconnect/reconnect MemoryRouter in **Customize → Connectors** and choose another vault during OAuth.

Treat OAuth scope as the enforcement boundary. In read-only mode, never attempt writes or deletions. A 403/insufficient-scope response means the operation is forbidden, not retriable. Never broaden permissions without the user reconnecting and consenting.

## 7. Quiet, visible behavior

Do not narrate every model-directed search. Do show the active scope in explicit `/recall`, `/remember`, `/forget`, and `/memory-status` flows. Keep receipts short and identify compatibility-scope behavior when useful.
