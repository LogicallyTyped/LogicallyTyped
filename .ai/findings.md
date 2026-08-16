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
