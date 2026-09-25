---
name: recall
description: This skill should be used when the user invokes /recall, asks what MemoryRouter remembers, or requests prior decisions, preferences, people, project status, or earlier work.
argument-hint: "<topic> [--legacy]"
disable-model-invocation: true
metadata:
  version: "2.0.0"
---

# Recall

Search MemoryRouter for `$ARGUMENTS`, following the `memoryrouter-memory` policy.

1. Require an active scope for project or organization recall. If unset and the topic is not clearly personal, ask for `/memoryrouter:memory-scope ...` and stop.
2. The current server exposes no native scope/handle argument. Include `MR_SCOPE_V1 <active-handle>` in the query and discard every result without the exact marker.
3. Use at most 6 results. Retry once with alternate wording if nothing matches.
4. `--legacy` explicitly permits unscoped legacy results. Label each such result **legacy/unscoped** and do not treat it as project-scoped.
5. Return a concise synthesis followed by provenance bullets containing scope, source/platform, and timestamp when supplied. If unavailable/offline, say so and continue without inventing results.
