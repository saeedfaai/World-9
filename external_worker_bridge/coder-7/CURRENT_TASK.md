---
schema: W9_EXTERNAL_CODER_CURRENT_TASK/1.1
canonical_truth: false
transport_only: true
worker_id: w9-worker-coder-7-001
logical_role_id: coder-7
specialist_identity_id: W9-CODER-7-CROSS-IMPLEMENTATION
task_id: C7-R2-01-MESSENGER-ALT-CANDIDATE
task_generation: 4
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

`external_worker_bridge/coder-7/candidate_outbox/C7-R2-01-MESSENGER-ALT-CANDIDATE/**`

Fallback issue outbox:

`https://github.com/saeedfaai/World-9/issues/9`

If the platform exposes no GitHub mutation action, `CHAT_RELAY_OUTBOX` is authorized for this task only. It must return one complete structured candidate bundle to HumanRoot for relay to Titi. No probe write is allowed.

## Goal

Independently implement a provider-neutral Messenger candidate that repairs three semantic classes without copying private implementation code:

1. **source-bound command provenance** — a material directive must be bound to an exact sender identity/role, immutable message/work reference and integrity material; chat text such as “from Titi” alone is insufficient authority;
2. **schema/version exactness** — incompatible or unknown message/envelope versions fail closed rather than being silently accepted;
3. **ACK recipient binding** — an acknowledgement must prove it acknowledges the exact message intended for the acknowledging recipient; recipient/message mismatch must fail closed.

This is an alternate implementation candidate, not a patch applied to canonical/runtime source.

## Required candidate file set

The candidate bundle must contain at minimum:

- `MANIFEST.json` — worker/task/source snapshot, file inventory/hashes where available, implementation language/runtime, assumptions, no-authority declaration;
- `README.md` — contract, failure semantics, integration boundary;
- `schemas/message-envelope.schema.json` — language-neutral envelope contract;
- `schemas/ack.schema.json` — ACK contract;
- `src/` — pure reference implementation for provenance validation, version validation and ACK recipient/message binding;
- `tests/` — executable positive and negative tests;
- `TESTS.json` — exact executed command/runtime/results; anything not run is `NOT_EXECUTED`;
- `HANDOFF.json` — blockers, integration assumptions, next safe action.

Preferred shape: language-neutral JSON contracts plus a small pure TypeScript implementation with no network/database/secret dependency. Another portable language is allowed only if the manifest records the choice and JSON contracts remain language-neutral.

## Required negative cases

At minimum reject:

- sender/role claim not bound to trusted source metadata;
- message integrity/reference mismatch;
- unknown or unsupported schema version;
- ACK for a different message id;
- ACK emitted by or for the wrong recipient;
- missing recipient binding;
- malformed provenance fields;
- replay/duplicate acknowledgement when the contract marks ACK as one logical acknowledgement.

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

`EXTERNAL_CANDIDATE_STATUS | worker_id=w9-worker-coder-7-001 | task_id=C7-R2-01-MESSENGER-ALT-CANDIDATE | transport=<BRANCH_FILE_OUTBOX|ISSUE_COMMENT_OUTBOX|CHAT_RELAY_OUTBOX|NONE> | output_ref=<exact-commit|issue-comment-url|CHAT_RELAY> | tests=<PASS_CANDIDATE|PARTIAL|NOT_EXECUTED> | state=<READY_FOR_TITI_INGESTION|BLOCKED_...> | runtime_authority=false`

If using `CHAT_RELAY_OUTBOX`, include the complete candidate bundle immediately below the receipt. Do not start C7-R2-02 in the same Run.
