<!-- type: findings | status: active | since: 2026-08-16 | applies-to: LogicallyTyped -->

# Findings: LogicallyTyped

## repo_distiller — docs_index self-listing inconsistency

`deterministic.docs_index` (parser-produced, not hand-edited) lists:

```
.ai/CONTEXT.md
.ai/distillate.json
.ai/distillation-ollama.md
```

i.e. it lists its own two output files (`distillate.json`, `distillation-ollama.md`) alongside `CONTEXT.md`. In `work-activity-log` (same pipeline run), `docs_index` lists only `.ai/CONTEXT.md` even though that repo's `.ai/` directory also holds all three files at read time. The apparent cause: the parser lists whatever is on disk under `.ai/` at scan time, so a repo whose distillate/ollama-md files already existed from a prior pass self-lists them, while a repo distilled fresh in the same run does not yet have them on disk when `docs_index` is computed. This is a parser-ordering artifact, not a content error — recorded here per the Stage 2 rule (deterministic fields are never hand-edited); field left as parsed.

## repo_distiller — distillation-ollama.md / distillate.json integration_points mismatch

`.ai/distillation-ollama.md § Integration Points` renders:

```
- UNKNOWN
```

while `.ai/distillate.json interpretive.integration_points` is `[]` (empty array, correctly reflecting a documentation-only repo with zero integration points). The Markdown renderer appears to emit a literal `UNKNOWN` bullet for an empty integration-points list instead of an explicit "none" statement or omitting the section. Minor renderer inconsistency, not a content error in the distillate itself; `distillation-ollama.md` is a rendered pipeline artifact, not hand-edited here.

---

### 2026-08-16 — Overnight Code Review (Opus high)
- **Status:** Open
- **Standard:** `STANDARDS/conventions/code-quality.md` — § Priority order #1 (human-centric: content must be readable/correct for its *actual* audience), § Anti-patterns (gold-plating / YAGNI — applying a code-project contract verbatim to a non-code repo), and § Fall-back rules (two artifacts conflict → file a finding). No secrets found in the diff, but the public `README.md` leaks internal doc-machinery identifiers (see F1) — a public-hygiene violation of the same audience principle.

**Scope:** `main...HEAD` on `chore/2026-08-16-doc-pilot` — a docs-only change (working tree clean). Adds `.ai/distillate.json`, `.ai/distillation-ollama.md`, `.ai/findings.md`; appends the 7-section ops-doc contract to the public GitHub *profile* `README.md`. 7 findings, none blocking a public-only-harm assessment but several audience-inappropriate.

**F1 — `README.md:78` (highest) — internal metadata leaked to public profile.** The pipeline footer (`schema_version` / `distilled_from_sha` / `verified_sha` / `verified_at`) is appended *unfenced* after an `<hr>`. Because it is not top-of-file YAML front matter, GitHub does not hide it — it renders as a bare paragraph of internal doc-machinery SHAs on `github.com/LogicallyTyped`, visible to any recruiter/visitor. `distillate.json operational_notes` confirms edits go live immediately with no staging. → Standard: human-centric for the *actual* audience (recruiters), not the pipeline.

**F2 — `README.md:66` — self-contradictory dependency claim.** "Dependencies: none (stdlib/BCL only)" contradicts lines 41–42 and the distillate, which state there is no source/build/test suite and zero dependencies. "(stdlib/BCL only)" falsely implies a compiled .NET project. → Standard: correctness / no self-contradiction on a human-read surface.

**F3 — `README.md:36` — wrong-audience contract applied mechanically.** The 7-section ops/code-project contract (Quickstart `git clone`, Entrypoints, Configuration, Dependencies, Operational surface, Deeper docs) is applied verbatim to a *profile* README whose audience is visitors, not operators. "Entrypoints: none — see Quickstart", "Operational surface: N/A", etc. degrade the profile for its real readers. The contract should have *exempted* the profile repo (generalize the mechanism) rather than being force-fit. → Standard: § Anti-patterns (gold-plating), YAGNI.

**F4 — `.ai/distillate.json:7` — stale verification SHA.** `distilled_from_sha` / `verified_sha` pin to `e64c8f6`, but this same PR (commit `7d1ac0a`) rewrites `README.md` *after* that SHA. The distillate's `purpose` ("short bio plus a pointer") no longer describes the committed tree, and the README footer repeats the same stale SHA as if current. A consumer trusting `verified_sha` assumes it reflects HEAD. → Standard: correctness; distillate must describe the tree it ships with.

**F5 — `.ai/distillate.json:21` — `docs_index` omits `findings.md`.** `deterministic.docs_index` lists `CONTEXT.md`, `distillate.json`, `distillation-ollama.md` but not `.ai/findings.md`, which ships in this same PR. Self-documented in this file as a scan-order artifact, but the shipped index still disagrees with actual `.ai/` contents. → Standard: consistency (noted as a deterministic-field parser artifact per the Stage-2 rule; recorded, not hand-corrected).

**F6 — `.ai/distillation-ollama.md:11` — consumer audience diverges from distillate.** Ollama says "Engineering teams interested in backend systems"; `distillate.json consumers` says "Anyone browsing github.com/LogicallyTyped — recruiters, collaborators, visitors". Two committed artifacts describing the same repo give materially different audiences; not previously flagged. → Standard: § Fall-back (conflicting artifacts → file a finding).

**F7 — `.ai/distillation-ollama.md:7` — purpose conflates this repo with `work-activity-log`.** Ollama purpose says this repo *is* "Christian's public engineering patterns and activity log", but README (42–44) and the distillate both state the activity log lives in the separate `work-activity-log` repo and this one only points to it. → Standard: correctness (mis-describes the repo).

**Assessment / recommendation:** F1 is the only externally-visible harm (internal SHAs on a public bio) and should be fixed before this branch reaches the public profile — fence or delete the footer. F2/F3 are audience-quality issues on the same public surface. F4–F7 are internal `.ai/` consistency issues; F5 is a known parser artifact (leave as parsed per Stage-2 rule), F6/F7 are ollama-renderer content drift consistent with the two mismatches already logged above — the ollama artifact is machine-generated and re-rendered, not hand-edited here. No code, no secrets, no injection/authz surface (documentation-only repo).
