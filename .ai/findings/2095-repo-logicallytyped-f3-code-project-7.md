# F3 code-project 7-section contract forced onto a profile README - the profile README serves visitors instead of operators - detail: migrated from .ai/findings.md (architecture A…

**Filed:** inbox 2095-repo-logicallytyped-f3-code-project-7, delivered 2026-10-28.

[repo:LogicallyTyped] **F3 code-project 7-section contract forced onto a profile README** - the profile README serves visitors instead of operators - detail: migrated from .ai/findings.md (architecture ADR 0002), full text in the file. Verified 2026-10-28: README.md still has What this is, Quickstart, Entrypoints, Configuration, Dependencies, Operational surface and Deeper docs sections below the bio. Exempt the profile repo from the contract.

## Full text (from the hand-kept list, migrated 2026-10-28)

Source: 2026-08-16 Overnight Code Review (Opus high), Status then: Open.

**F3 — `README.md:36` — wrong-audience contract applied mechanically.** The 7-section ops/code-project contract (Quickstart `git clone`, Entrypoints, Configuration, Dependencies, Operational surface, Deeper docs) is applied verbatim to a *profile* README whose audience is visitors, not operators. "Entrypoints: none — see Quickstart", "Operational surface: N/A", etc. degrade the profile for its real readers. The contract should have *exempted* the profile repo (generalize the mechanism) rather than being force-fit. → Standard: § Anti-patterns (gold-plating), YAGNI.
