---
schema: W9_EXTERNAL_CODER_CURRENT_TASK/1.7
canonical_truth: false
transport_only: true
worker_id: w9-worker-coder-7-001
logical_role_id: coder-7
specialist_identity_id: W9-CODER-7-CROSS-IMPLEMENTATION
task_id: C7-R2-04-RECONSTRUCTION-ALT-CANDIDATE
task_generation: 7
candidate_output_authority: true
runtime_authority: false
queue_ref: external_worker_bridge/coder-7/RUN_QUEUE.json
queue_depth: 24
full_chat_bundle_policy: DISABLED
transport_state: COMPACT_RECIPE_MODE_AFTER_CONFIRMED_GITHUB_WRITE_FAILURE
---

# Coder 7 — Current Task

Public repository: `saeedfaai/World-9`
Public branch: `manager/external-grok-bridge-v0-1`

Required reads:
- `external_worker_bridge/coder-7/BRIDGE_MANIFEST.json`
- `external_worker_bridge/coder-7/EXTERNAL_CANDIDATE_PROTOCOL.md`
- `external_worker_bridge/coder-7/COMPACT_RECIPE_PROTOCOL.md`
- `external_worker_bridge/coder-7/RUN_QUEUE.json`
- this `CURRENT_TASK.md`

## Confirmed transport condition

The external worker already returned:

`BLOCKED_TRANSPORT_NO_GITHUB_WRITE`

Branch mutation returned authorization failure and issue-comment mutation was unavailable. Do not repeat GitHub capability attempts in this task and do not generate dummy/probe writes.

## Goal

Produce the design for an independent alternate deterministic append-only StockMovement reconstruction/invariant checker without treating reconstructed evidence as original source provenance and without creating a second inventory truth.

Required semantics:
- append-only StockMovement remains the reconstruction basis;
- current stock is derived from movement history, never directly overwritten;
- deterministic replay for identical ordered evidence;
- detect malformed movements, duplicate/idempotency conflicts, impossible one-sided transfers and inconsistent unit/location references;
- distinguish `OBSERVED_RUNTIME_EVIDENCE`, `RECONSTRUCTED_EVIDENCE`, and `ORIGINAL_SOURCE_PROVENANCE` and never promote one into another;
- replay/test schemas must not be silently treated as canonical;
- unknown/missing provenance fails closed;
- no network, DB, secret, migration, production, merge or promotion effect.

## Output transport — compact recipe only

Do NOT print source code, full files, a unified diff, base64, compressed source, or the full candidate bundle into chat.

For this exact Run, output one compact `W9_C7_COMPACT_RECIPE/1.0` recipe only, following `COMPACT_RECIPE_PROTOCOL.md`.

The recipe must contain:
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

Keep it concise; target <= 6000 characters. No complete function/class/file bodies.

Project Control/Titi will materialize real source separately and will label that code as Titi-materialized from the Grok recipe. You must not claim authorship of exact materialized bytes and must not claim their tests passed.

## Completion

Return:

`🟢 GREEN`

`EXTERNAL_RECIPE_STATUS | worker_id=w9-worker-coder-7-001 | task_id=C7-R2-04-RECONSTRUCTION-ALT-CANDIDATE | task_generation=7 | transport=CHAT_COMPACT_RECIPE_OUTBOX | state=READY_FOR_TITI_MATERIALIZATION | tests=<executed-status-or-NOT_EXECUTED> | runtime_authority=false`

Then include only the compact recipe, not source code, and stop. Do not start C7-R2-05 in the same Run.
