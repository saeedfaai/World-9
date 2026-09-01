---
schema: W9_EXTERNAL_CODER_CURRENT_TASK/1.8
canonical_truth: false
transport_only: true
worker_id: w9-worker-coder-7-001
logical_role_id: coder-7
specialist_identity_id: W9-CODER-7-CROSS-IMPLEMENTATION
task_id: C7-R2-05-LOCAL-RUNTIME-ALT-CANDIDATE
task_generation: 8
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

## Prior-task boundary

`C7-R2-04-RECONSTRUCTION-ALT-CANDIDATE` compact recipe was received and Titi/Project Control materialized it into durable private Development evidence. Grok did not author the exact materialized bytes and did not execute their tests. Independent gate remains separate.

Do not modify or re-emit C7-R2-04 in this Run.

## Goal

Produce the design recipe for an alternate provider/language-neutral **local/offline Runtime Host** candidate that preserves governed World 9 authority/effect boundaries and never creates a second truth.

The design must support replaceable executable modules behind a stable protocol without making Python, TypeScript, Node, Grok, GitHub, Supabase, a cloud provider, or any particular process launcher part of the architecture.

## Required architecture semantics

- Small Runtime Host; executable modules are replaceable implementations behind a language-neutral protocol.
- Long-lived worker/session model preferred; do not require spawn-per-call.
- Explicit module execution roles: `ACTIVE`, `SHADOW`, `FALLBACK`.
- Only a separately governed ACTIVE path may later feed canonical effects; SHADOW/FALLBACK outputs are evidence/proposals only until governed selection.
- Runtime Host/modules emit proposals/receipts; they do not directly write canonical truth and do not self-authorize.
- Host-supplied authority context is explicit. Missing, stale or unknown authority/state fails closed.
- Stable opaque refs/handles only; no raw secret values in protocol payloads.
- Deterministic request/receipt correlation and idempotency/reconciliation semantics.
- Unknown execution/writer state is never reported as committed success.
- Explicit restart/recovery behavior for worker crash, timeout, stale worker, malformed output and unavailable implementation.
- No second inventory truth, no sixth W8 plane, no production/runtime authority granted by this design task.
- No network, DB write, migration, secret access, provider mutation, merge, promotion or production effect.

## Required compact recipe content

Follow `COMPACT_RECIPE_PROTOCOL.md` and include, concisely:

- `implementation_language`
- `proposed_file_manifest` (paths only)
- `public_interface_summary`
- `module_host_protocol_summary`
- `authority_effect_boundaries`
- `active_shadow_fallback_semantics`
- `long_lived_worker_lifecycle`
- `receipt_and_proposal_model`
- `failure_recovery_state_machine`
- `invariants`
- `deterministic_algorithm_steps`
- `positive_test_vectors`
- `negative_falsifiers`
- `assumptions`
- `blockers`
- `tests_executed` / `tests_not_executed`
- `provenance_note=DESIGN_RECIPE_ONLY_NOT_SOURCE`

## Output transport — compact recipe only

The external worker has already confirmed that both available GitHub mutation paths are unavailable. Do not retry GitHub write capability and do not create probe/dummy writes.

Do NOT print complete source code, full function/class bodies, full files, unified diffs, base64/hex/compressed source, or a complete candidate bundle into chat.

Output exactly one compact design recipe for this task. Titi/Project Control will materialize exact source separately and record authorship/provenance accurately.

## Completion

Return:

`🟢 GREEN`

`EXTERNAL_RECIPE_STATUS | worker_id=w9-worker-coder-7-001 | task_id=C7-R2-05-LOCAL-RUNTIME-ALT-CANDIDATE | task_generation=8 | transport=CHAT_COMPACT_RECIPE_OUTBOX | state=READY_FOR_TITI_MATERIALIZATION | tests=<executed-status-or-NOT_EXECUTED> | runtime_authority=false`

Then include only the compact recipe and stop. Do not start C7-R2-06 in the same Run.
