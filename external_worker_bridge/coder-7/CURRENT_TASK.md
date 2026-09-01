---
schema: W9_EXTERNAL_CODER_CURRENT_TASK/2.0
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
transport_state: GOOGLE_DRIVE_DURABLE_CODE_OUTBOX
private_task_ref: project_control/task_feed/tasks/TASK-C7-R2-05-COMPACT-RECIPE.md
private_task_blob_sha: 73a23af8e3abd93b7de30b8ea55513e77523e113
drive_outbox_protocol_ref: external_worker_bridge/coder-7/DRIVE_CODE_OUTBOX_PROTOCOL.md
drive_outbox_folder_id: 1HuS7zWoG7uiEoFZRko699r6Z4At2jpCP
drive_outbox_document_id: 1a2XVoa1rBMR60rODT2I4sm4Abc6FnS62xvMKIFtVym0
---

# Coder 7 — Current Task

Public repository: `saeedfaai/World-9`

Public branch: `manager/external-grok-bridge-v0-1`

Required reads:

- `external_worker_bridge/coder-7/BRIDGE_MANIFEST.json`
- `external_worker_bridge/coder-7/EXTERNAL_CANDIDATE_PROTOCOL.md`
- `external_worker_bridge/coder-7/DRIVE_CODE_OUTBOX_PROTOCOL.md`
- `external_worker_bridge/coder-7/RUN_QUEUE.json`
- this `CURRENT_TASK.md`

## Source binding

Private Project Control exact task:

`project_control/task_feed/tasks/TASK-C7-R2-05-COMPACT-RECIPE.md`

Exact current blob:

`73a23af8e3abd93b7de30b8ea55513e77523e113`

Task id/generation did not change. Only the external transport was upgraded from recipe relay to durable exact-source outbox.

## Goal

Author the complete exact source candidate for an alternate provider/language-neutral local/offline Runtime Host preserving governed World 9 authority/effect boundaries and no second truth.

Required semantics remain: small Runtime Host, replaceable modules, long-lived worker/session model, ACTIVE/SHADOW/FALLBACK roles, proposal/receipt outputs, no self-authorization, fail-closed authority/state, opaque refs instead of raw secrets, deterministic correlation/idempotency, explicit crash/timeout/stale/malformed/unavailable recovery, no second truth, no sixth W8 plane.

## Output transport — durable exact source

Do not retry GitHub mutation; its 403 write limitation is already confirmed.

Use Google Drive write tools instead. Write the complete exact candidate into this pre-created bound document:

`1a2XVoa1rBMR60rODT2I4sm4Abc6FnS62xvMKIFtVym0`

Folder:

`1HuS7zWoG7uiEoFZRko699r6Z4At2jpCP`

Follow `DRIVE_CODE_OUTBOX_PROTOCOL.md`. Under the existing marker, write deterministic `=== FILE: path ===` / `=== END FILE ===` sections containing MANIFEST.json, README.md, implementation source, tests, TESTS.json and HANDOFF.json.

This is full exact source output to a durable transport, not a compact recipe. Do not place complete source in HumanRoot chat.

Project Control will import the exact Drive-authored bytes into the private candidate root without semantic edits. If revision attribution and byte preservation verify, provenance may state `grok_exact_source_authorship=true`.

## Safety

No private-source copying, secrets, production data, DB writes, migrations, provider mutation, merge, promotion, canonical effects or runtime authority. Tests must remain `NOT_EXECUTED` unless actually executed.

## Completion

Return only:

`🟢 GREEN`

`EXTERNAL_CANDIDATE_STATUS | worker_id=w9-worker-coder-7-001 | task_id=C7-R2-05-LOCAL-RUNTIME-ALT-CANDIDATE | task_generation=8 | transport=GOOGLE_DRIVE_CODE_OUTBOX | output_ref=1a2XVoa1rBMR60rODT2I4sm4Abc6FnS62xvMKIFtVym0 | tests=<executed-status-or-NOT_EXECUTED> | state=READY_FOR_TITI_INGESTION | runtime_authority=false`

If and only if Google Drive write is unavailable in your worker environment, return a short `BLOCKED_TRANSPORT_NO_DRIVE_WRITE` receipt and stop. Never dump the source into chat.
