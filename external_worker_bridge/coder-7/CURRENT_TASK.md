---
schema: W9_EXTERNAL_CODER_CURRENT_TASK/1.4
canonical_truth: false
transport_only: true
worker_id: w9-worker-coder-7-001
logical_role_id: coder-7
specialist_identity_id: W9-CODER-7-CROSS-IMPLEMENTATION
task_id: C7-R2-03-SECURITY-POLICY-ALT-CANDIDATE
task_generation: 6
candidate_output_authority: true
runtime_authority: false
queue_ref: external_worker_bridge/coder-7/RUN_QUEUE.json
queue_depth: 24
state: RELAY_RECOVERY_REQUIRED
---

# Coder 7 — Current Task

## Exact transport binding

Public repository: `saeedfaai/World-9`

Public branch: `manager/external-grok-bridge-v0-1`

Required reads:

- `external_worker_bridge/coder-7/BRIDGE_MANIFEST.json`
- `external_worker_bridge/coder-7/EXTERNAL_CANDIDATE_PROTOCOL.md`
- `external_worker_bridge/coder-7/RUN_QUEUE.json`
- this `CURRENT_TASK.md`

## Recovery state

Project Control observed your receipt stating that the complete candidate bundle for `C7-R2-03-SECURITY-POLICY-ALT-CANDIDATE` was already emitted through `CHAT_RELAY_OUTBOX`, but Titi does not currently possess a retrievable exact copy of that bundle for ingestion.

This does **not** authorize new implementation work and does **not** consume C7-R2-03.

The next HumanRoot `Run` is a bounded **transport recovery only** cycle.

## Required action for the next Run

Re-emit the complete previously produced `C7-R2-03-SECURITY-POLICY-ALT-CANDIDATE` candidate bundle through `CHAT_RELAY_OUTBOX` **without changing its semantics or files**.

Do not:

- redesign, patch or improve the prior candidate;
- start `C7-R2-04` or any later queue item;
- self-review;
- claim Bug-Gate, integration, merge, promotion, runtime or production PASS;
- change `tests=NOT_EXECUTED` unless you actually execute tests in an independently permitted environment, which this recovery cycle does not authorize.

The recovered relay must contain the complete structured bundle that was previously produced, including its receipt and all candidate files/material needed for Titi ingestion.

## Completion

Return exactly one light, then:

`EXTERNAL_CANDIDATE_STATUS | worker_id=w9-worker-coder-7-001 | task_id=C7-R2-03-SECURITY-POLICY-ALT-CANDIDATE | transport=CHAT_RELAY_OUTBOX | output_ref=CHAT_RELAY_RECOVERED | tests=NOT_EXECUTED | state=READY_FOR_TITI_INGESTION | runtime_authority=false`

Then include the complete recovered candidate bundle immediately below the receipt.

After that, stop. Project Control will ingest it and advance the queue if evidence is sufficient.
