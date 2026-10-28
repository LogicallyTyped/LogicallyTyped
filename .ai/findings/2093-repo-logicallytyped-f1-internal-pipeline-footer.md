# F1 internal pipeline footer renders on the public profile - the public GitHub profile shows no schema_version and SHA lines to visitors - detail: migrated from .ai/findings.md (…

**Filed:** inbox 2093-repo-logicallytyped-f1-internal-pipeline-footer, delivered 2026-10-28.

[repo:LogicallyTyped] **F1 internal pipeline footer renders on the public profile** - the public GitHub profile shows no schema_version and SHA lines to visitors - detail: migrated from .ai/findings.md (architecture ADR 0002), full text in the file. Verified 2026-10-28: README.md still ends with an unfenced block (schema_version, distilled_from_sha, verified_sha, verified_at) after the horizontal rule; GitHub renders it as a paragraph. Fence or delete it.

## Full text (from the hand-kept list, migrated 2026-10-28)

Source: 2026-08-16 Overnight Code Review (Opus high), scope `main...HEAD` on `chore/2026-08-16-doc-pilot`, a docs-only change. Standard: `STANDARDS/conventions/code-quality.md` § Priority order #1 (human-centric: content must be readable/correct for its actual audience), § Anti-patterns (gold-plating / YAGNI), § Fall-back rules (two artifacts conflict, file a finding). Status then: Open.

**F1 — `README.md:78` (highest) — internal metadata leaked to public profile.** The pipeline footer (`schema_version` / `distilled_from_sha` / `verified_sha` / `verified_at`) is appended *unfenced* after an `<hr>`. Because it is not top-of-file YAML front matter, GitHub does not hide it — it renders as a bare paragraph of internal doc-machinery SHAs on `github.com/LogicallyTyped`, visible to any recruiter/visitor. `distillate.json operational_notes` confirms edits go live immediately with no staging. → Standard: human-centric for the *actual* audience (recruiters), not the pipeline.

Review assessment: F1 is the only externally-visible harm (internal SHAs on a public bio) and should be fixed before this branch reaches the public profile — fence or delete the footer.
