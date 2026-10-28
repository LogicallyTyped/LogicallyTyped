# F2 README says Dependencies: none (stdlib/BCL only) - the profile README stops implying a compiled .NET project - detail: migrated from .ai/findings.md (architecture ADR 0002), …

**Filed:** inbox 2094-repo-logicallytyped-f2-readme-says-dependencies, delivered 2026-10-28.

[repo:LogicallyTyped] **F2 README says Dependencies: none (stdlib/BCL only)** - the profile README stops implying a compiled .NET project - detail: migrated from .ai/findings.md (architecture ADR 0002), full text in the file. Verified 2026-10-28: the Dependencies section of README.md still has that text, while the same README says there is no build or test suite.

## Full text (from the hand-kept list, migrated 2026-10-28)

Source: 2026-08-16 Overnight Code Review (Opus high), Status then: Open.

**F2 — `README.md:66` — self-contradictory dependency claim.** "Dependencies: none (stdlib/BCL only)" contradicts lines 41–42 and the distillate, which state there is no source/build/test suite and zero dependencies. "(stdlib/BCL only)" falsely implies a compiled .NET project. → Standard: correctness / no self-contradiction on a human-read surface.

Review assessment: F2/F3 are audience-quality issues on the same public surface as F1.
