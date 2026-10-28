# F4 distillate.json verified_sha is stale - a verified_sha that matches HEAD, and a purpose that describes the committed tree - detail: migrated from .ai/findings.md (architectur…

**Filed:** inbox 2096-repo-logicallytyped-f4-distillate-json-verifiedsha, delivered 2026-10-28.

[repo:LogicallyTyped] **F4 distillate.json verified_sha is stale** - a verified_sha that matches HEAD, and a purpose that describes the committed tree - detail: migrated from .ai/findings.md (architecture ADR 0002), full text in the file. Verified 2026-10-28: distilled_from_sha and verified_sha are still e64c8f6, older than the README rewrite in 7d1ac0a, and the README footer repeats that SHA. Also see inbox 1177 on the distillation file rename.

## Full text (from the hand-kept list, migrated 2026-10-28)

Source: 2026-08-16 Overnight Code Review (Opus high), Status then: Open.

**F4 — `.ai/distillate.json:7` — stale verification SHA.** `distilled_from_sha` / `verified_sha` pin to `e64c8f6`, but this same PR (commit `7d1ac0a`) rewrites `README.md` *after* that SHA. The distillate's `purpose` ("short bio plus a pointer") no longer describes the committed tree, and the README footer repeats the same stale SHA as if current. A consumer trusting `verified_sha` assumes it reflects HEAD. → Standard: correctness; distillate must describe the tree it ships with.

Review assessment: F4-F7 are internal `.ai/` consistency issues.
