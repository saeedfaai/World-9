---
schema: W9_EXTERNAL_CODER_CURRENT_TASK/1.2
canonical_truth: false
transport_only: true
worker_id: w9-worker-coder-7-001
logical_role_id: coder-7
specialist_identity_id: W9-CODER-7-CROSS-IMPLEMENTATION
task_id: C7-R2-02-INVENTORYPORT-ALT-CANDIDATE
task_generation: 5
candidate_output_authority: true
runtime_authority: false
---

# Coder 7 — Current Task

## Exact transport binding

Public repository: `saeedfaai/World-9`

Public branch: `manager/external-grok-bridge-v0-1`

Required reads:

- `external_worker_bridge/coder-7/BRIDGE_MANIFEST.json`
- `external_worker_bridge/coder-7/EXTERNAL_CANDIDATE_PROTOCOL.md`
- this `CURRENT_TASK.md`

Preferred exact branch candidate root:

`external_worker_bridge/coder-7/candidate_outbox/C7-R2-02-INVENTORYPORT-ALT-CANDIDATE/**`

Fallback issue outbox:

`https://github.com/saeedfaai/World-9/issues/9`

If the platform exposes no GitHub mutation action, `CHAT_RELAY_OUTBOX` is authorized for this task only. It must return one complete structured candidate bundle to HumanRoot for relay to Titi. No probe write is allowed.

## Prior-task boundary

`C7-R2-01-MESSENGER-ALT-CANDIDATE` was delivered through `CHAT_RELAY_OUTBOX` and ingested by Titi as `INGESTED_TRANSPORT_EVIDENCE_UNVERIFIED` with tests `NOT_EXECUTED`. That is enough to consume the bounded output task, but it is not Bug-Gate PASS, integration, merge, promotion, runtime or production evidence.

Do not self-review or modify C7-R2-01 in this Run.

## Goal

Build an independent alternate provider-neutral `InventoryPort` candidate for `W9-INVENTORY/1` without copying private implementation code.

The candidate must keep the canonical writer intentionally unbound and fail closed when writer authority/state is unknown.

Required operation surface:

- `production_receipt`
- `goods_receipt`
- `goods_issue`
- `transfer`
- `adjustment_request`
- `inventory_read`
- `movement_history_read`
- `pending_approval_read`

## Required semantics

- no client-supplied runtime authority;
- actor/authority is an input from a trusted host boundary, never inferred from display text;
- no direct stock overwrite or second inventory truth;
- inventory reads are derived/reconstructable from governed movement history semantics;
- command success must return a deterministic receipt/reference;
- idempotency fingerprint/collision must fail closed;
- unknown writer state must never be reported as success;
- `transfer` contract must be atomic at the authoritative writer boundary, but this candidate must not claim the current runtime already provides that property;
- `adjustment_request` creates an approval request only and must not itself create stock movement;
- provider/database/session details must not leak into the language-neutral contract;
- no network, database, secret, migration or production effect in this candidate.

## Required candidate file set

Produce a self-contained candidate bundle containing at minimum:

- `MANIFEST.json`
- `README.md`
- `schemas/inventory-port.schema.json` or equivalent language-neutral contract documents
- `src/` pure reference implementation/types
- `tests/` positive and negative contract tests
- `TESTS.json`
- `HANDOFF.json`

Preferred implementation shape is language-neutral JSON contracts plus a dependency-light TypeScript reference implementation. Another portable language is allowed if recorded in the manifest and the external contract remains language-neutral.

## Required negative cases

At minimum cover/reject:

- missing trusted actor/authority context for command operation;
- unknown/unbound canonical writer;
- duplicate idempotency key with different semantic payload;
- malformed operation payload;
- adjustment request attempting direct stock movement;
- transfer with partial/one-sided completion representation;
- provider-specific raw error leaking past the port boundary;
- read result that claims committed state when source status is unknown/stale.

## Transport selection for this Run

Do not test write capability by writing anything.

Inspect available actions only:

- If exact branch file create/update is available, use `BRANCH_FILE_OUTBOX` and write only the real candidate files inside the exact root above.
- Else if GitHub issue-comment mutation is available, use `ISSUE_COMMENT_OUTBOX` and post one complete structured candidate bundle as one comment on issue #9.
- Else use `CHAT_RELAY_OUTBOX` and return one complete structured bundle in chat.

The inability to use one provider action is not permission to weaken architecture.

## Architecture boundaries

Do not invent runtime authority, secrets, DB state or canonical writer bindings.
Do not access or reconstruct private source code.
Do not merge or promote.
Do not call your own candidate Bug-Gate PASS or independent-review PASS.
A successful local test is candidate evidence only.

## Completion and traffic light

One `Run` performs only this task and then stops.

Return a receipt beginning with exactly one light:

- `🟢 GREEN` if the real candidate bundle was produced through one authorized transport and required evidence exists;
- `🟡 YELLOW` if completion is blocked but exact cause + next safe fix are known;
- `🔴 RED` if completion failed and cause/evidence is still unknown or insufficient.

Then return:

`EXTERNAL_CANDIDATE_STATUS | worker_id=w9-worker-coder-7-001 | task_id=C7-R2-02-INVENTORYPORT-ALT-CANDIDATE | transport=<BRANCH_FILE_OUTBOX|ISSUE_COMMENT_OUTBOX|CHAT_RELAY_OUTBOX|NONE> | output_ref=<exact-commit|issue-comment-url|CHAT_RELAY> | tests=<PASS_CANDIDATE|PARTIAL|NOT_EXECUTED> | state=<READY_FOR_TITI_INGESTION|BLOCKED_...> | runtime_authority=false`

If using `CHAT_RELAY_OUTBOX`, include the complete candidate bundle immediately below the receipt. Do not start C7-R2-03 in the same Run.
