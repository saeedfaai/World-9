# World 9 — Coder 7 Compact Recipe Transport

schema: W9_EXTERNAL_COMPACT_RECIPE_PROTOCOL/1.0
canonical_truth: false
transport_only: true
runtime_authority: false

Purpose: keep external Coder 7 productive when its platform has no GitHub mutation scope, without pasting full source code into HumanRoot chat and without weakening World 9 architecture.

## Model

`Grok design recipe -> Titi/Project Control materializer -> detached candidate capsule -> BUGGER/independent gate`

A recipe is NOT source code, NOT a candidate capsule, NOT canonical truth, and NOT runtime authority. It is a compact implementation specification that Project Control may materialize into a separate candidate while preserving provenance.

## Authorized chat payload

Chat may contain one compact recipe for the exact CURRENT_TASK only. It MUST NOT contain complete source files, full diffs, secrets, private-source copies, or a later queue item.

Maximum intended size: concise enough for direct HumanRoot relay; target <= 6000 characters.

Required fields:
- worker_id
- task_id
- task_generation
- recipe_schema=`W9_C7_COMPACT_RECIPE/1.0`
- implementation_language
- proposed_file_manifest (paths only)
- public_interface_summary
- invariants
- deterministic_algorithm_steps
- positive_test_vectors
- negative_falsifiers
- assumptions
- blockers
- tests_executed / tests_not_executed
- provenance_note=`DESIGN_RECIPE_ONLY_NOT_SOURCE`

## Materialization boundary

Project Control/Titi may translate the recipe into real source in private Development evidence. The materialized code MUST be labeled as materialized by Project Control from a Grok recipe; it must never be misrepresented as exact bytes authored or executed by Grok.

Any materialized candidate requires its own hashes, tests, handoff and independent BUGGER/reviewer gate. `tests=NOT_EXECUTED` on the recipe remains NOT_EXECUTED until materialized code is actually executed.

## Forbidden

- full source code in chat
- base64/hex/compressed source disguised as a recipe
- self-review or Bug Gate claim
- merge/promotion/runtime/DB/migration/production effect
- authority minting
- second inventory truth
- sixth W8 plane
- silently converting reconstructed/runtime evidence into original-source provenance

## Green meaning

A GREEN recipe Run means only: the bounded external design task produced a complete compact recipe that is ready for Titi materialization. It does not mean implementation PASS, candidate PASS, Bug Gate PASS, integration PASS, merge, promotion, runtime or production PASS.
