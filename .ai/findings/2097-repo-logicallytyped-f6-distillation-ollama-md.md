# F6 distillation-ollama.md names a different audience than distillate.json - two committed artifacts that agree on who reads the repo - detail: migrated from .ai/findings.md (arc…

**Filed:** inbox 2097-repo-logicallytyped-f6-distillation-ollama-md, delivered 2026-10-28.

[repo:LogicallyTyped] **F6 distillation-ollama.md names a different audience than distillate.json** - two committed artifacts that agree on who reads the repo - detail: migrated from .ai/findings.md (architecture ADR 0002), full text in the file. Verified 2026-10-28: distillation-ollama.md Consumers says engineering teams interested in backend systems, distillate.json consumers says anyone browsing the profile page (recruiters, collaborators, visitors). Machine-generated file: re-render or correct it, do not hand-edit.

## Full text (from the hand-kept list, migrated 2026-10-28)

Source: 2026-08-16 Overnight Code Review (Opus high), Status then: Open.

**F6 — `.ai/distillation-ollama.md:11` — consumer audience diverges from distillate.** Ollama says "Engineering teams interested in backend systems"; `distillate.json consumers` says "Anyone browsing github.com/LogicallyTyped — recruiters, collaborators, visitors". Two committed artifacts describing the same repo give materially different audiences; not previously flagged. → Standard: § Fall-back (conflicting artifacts → file a finding).

Review assessment: F6/F7 are ollama-renderer content drift; the ollama artifact is machine-generated and re-rendered, not hand-edited.
