# F1 internal pipeline footer renders on the public profile - the public GitHub profile shows no schema_version and SHA lines to visitors - detail: migrated from .ai/findings.md (…

**Filed:** inbox 2093-repo-logicallytyped-f1-internal-pipeline-footer, delivered 2026-10-28.

[repo:LogicallyTyped] **F1 internal pipeline footer renders on the public profile** - the public GitHub profile shows no schema_version and SHA lines to visitors - detail: migrated from .ai/findings.md (architecture ADR 0002), full text in the file. Verified 2026-10-28: README.md still ends with an unfenced block (schema_version, distilled_from_sha, verified_sha, verified_at) after the horizontal rule; GitHub renders it as a paragraph. Fence or delete it.
