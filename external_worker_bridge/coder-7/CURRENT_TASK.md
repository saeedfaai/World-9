---
schema: W9_EXTERNAL_CODER_CURRENT_TASK/1.5
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
---

# Coder 7 — Current Task

Public repository: `saeedfaai/World-9`
Public branch: `manager/external-grok-bridge-v0-1`

Required reads:
- `external_worker_bridge/coder-7/BRIDGE_MANIFEST.json`
- `external_worker_bridge/coder-7/EXTERNAL_CANDIDATE_PROTOCOL.md`
- `external_worker_bridge/coder-7/RUN_QUEUE.json`
- this `CURRENT_TASK.md`

## Prior-task boundary

`C7-R2-03-SECURITY-POLICY-ALT-CANDIDATE` has been recovered and ingested by Titi as transport evidence. Its tests remain `NOT_EXECUTED`; this is not Bug-Gate/integration/merge/promotion/runtime/production PASS.

Do not modify C7-R2-03 in this Run.

## Goal

Build an independent alternate deterministic append-only StockMovement reconstruction/invariant checker without treating reconstructed evidence as original source provenance and without creating a second inventory truth.

Required semantics:
- append-only StockMovement remains the reconstruction basis;
- current stock is derived from movement history, never directly overwritten;
- deterministic replay for identical ordered evidence;
- detect malformed movements, duplicate/idempotency conflicts, impossible one-sided transfers and inconsistent unit/location references;
- distinguish `OBSERVED_RUNTIME_EVIDENCE`, `RECONSTRUCTED_EVIDENCE`, and `ORIGINAL_SOURCE_PROVENANCE` and never promote one into another;
- replay/test schemas must not be silently treated as canonical;
- unknown/missing provenance fails closed;
- no network, DB, secret, migration, production, merge or promotion effect.

Required candidate bundle:
- `MANIFEST.json`
- `README.md`
- language-neutral reconstruction/invariant schema(s)
- `src/` pure reference implementation/types
- `tests/` positive and negative falsifiers
- `TESTS.json`
- `HANDOFF.json`

## Output transport — changed by HumanRoot

**Do not print the candidate source code or full bundle into chat.**

Use `BRANCH_FILE_OUTBOX` only and write the real candidate files directly under:

`external_worker_bridge/coder-7/candidate_outbox/C7-R2-04-RECONSTRUCTION-ALT-CANDIDATE/**`

Do not probe write capability with dummy/noop/placeholder files.

If branch file create/update capability is unavailable in this Grok room, do not fall back to a full CHAT_RELAY bundle. Return only:

`🟡 YELLOW`

`EXTERNAL_CANDIDATE_STATUS | worker_id=w9-worker-coder-7-001 | task_id=C7-R2-04-RECONSTRUCTION-ALT-CANDIDATE | transport=NONE | output_ref=NONE | tests=NOT_EXECUTED | state=BLOCKED_TRANSPORT_NO_GITHUB_WRITE | runtime_authority=false`

and stop. Do not start a later task.

If branch writes succeed, return only the compact receipt below; do not paste file contents into chat:

`🟢 GREEN`

`EXTERNAL_CANDIDATE_STATUS | worker_id=w9-worker-coder-7-001 | task_id=C7-R2-04-RECONSTRUCTION-ALT-CANDIDATE | transport=BRANCH_FILE_OUTBOX | output_ref=<exact-commit-sha> | tests=<PASS_CANDIDATE|PARTIAL|NOT_EXECUTED> | state=READY_FOR_TITI_INGESTION | runtime_authority=false`

Then stop.
