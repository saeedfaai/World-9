---
schema: W9_EXTERNAL_CODER_CURRENT_TASK/1.3
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

The public queue now carries a deep 24-item backlog so this worker does not need to wait for unrelated lanes. Queue membership grants no extra authority. Each HumanRoot `Run` still performs exactly one bounded current task.

Preferred exact branch candidate root:

`external_worker_bridge/coder-7/candidate_outbox/C7-R2-03-SECURITY-POLICY-ALT-CANDIDATE/**`

Fallback issue outbox:

`https://github.com/saeedfaai/World-9/issues/9`

If the platform exposes no GitHub mutation action, `CHAT_RELAY_OUTBOX` is authorized for this task only. It must return one complete structured candidate bundle to HumanRoot for relay to Titi. No probe write is allowed.

## Prior-task boundary

`C7-R2-02-INVENTORYPORT-ALT-CANDIDATE` was delivered through `CHAT_RELAY_OUTBOX` and ingested by Titi as transport evidence with worker tests `NOT_EXECUTED`. That is enough to consume the bounded external-output task; it is not Bug-Gate PASS, integration, merge, promotion, runtime or production evidence.

Do not self-review or modify C7-R2-02 in this Run.

## Goal

Build an independent provider-neutral deny-by-default security policy / identity adapter candidate and falsifiers for inventory semantics, without copying private implementation code.

The candidate must treat identity, role, scope, grant freshness and authorization as host/governance inputs. Display text, client payload claims or provider session details must never mint authority.

## Required semantics

- deny by default when required identity/authority evidence is missing, stale, revoked, unknown or out of scope;
- server/host-derived actor identity is distinct from client-supplied command payload;
- client-supplied `actor`, `role`, `permission`, `capability`, `service_role` or equivalent authority-looking fields must not grant access;
- stale or revoked grants must fail closed;
- warehouse/SKU/location scope escalation must be rejected;
- transfer authorization must cover both source and destination scopes; one-sided scope is insufficient;
- `adjustment_request` must not permit requester self-approval through the policy layer;
- AI/read-only identity must not acquire write/effect capabilities;
- provider/database/session-specific authorization details must not leak into the language-neutral contract;
- no network, DB, secret, migration or production effect.

## Required candidate file set

Produce a self-contained bundle containing at minimum:

- `MANIFEST.json`
- `README.md`
- language-neutral policy/identity schema document(s)
- `src/` pure reference implementation/types
- `tests/` positive and negative falsifiers
- `TESTS.json`
- `HANDOFF.json`

Preferred implementation shape is language-neutral JSON contracts plus dependency-light TypeScript. Another portable language is allowed if recorded and the external contract remains language-neutral.

## Required negative cases

At minimum cover/reject:

- forged actor identity in client payload;
- forged role/capability in client payload;
- missing trusted host actor context;
- stale grant;
- revoked grant;
- warehouse/SKU/location scope escalation;
- transfer with authority on only one side;
- requester attempting self-approval;
- AI/read-only actor attempting any command/effect operation;
- unknown authorization state.

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

Return exactly one light, then:

`EXTERNAL_CANDIDATE_STATUS | worker_id=w9-worker-coder-7-001 | task_id=C7-R2-03-SECURITY-POLICY-ALT-CANDIDATE | transport=<BRANCH_FILE_OUTBOX|ISSUE_COMMENT_OUTBOX|CHAT_RELAY_OUTBOX|NONE> | output_ref=<exact-commit|issue-comment-url|CHAT_RELAY> | tests=<PASS_CANDIDATE|PARTIAL|NOT_EXECUTED> | state=<READY_FOR_TITI_INGESTION|BLOCKED_...> | runtime_authority=false`

If using `CHAT_RELAY_OUTBOX`, include the complete candidate bundle immediately below the receipt. Do not start C7-R2-04 in the same Run.
