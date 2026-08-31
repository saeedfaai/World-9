---
schema: W9_EXTERNAL_CODER_CURRENT_TASK/1.0
canonical_truth: false
transport_only: true
worker_id: w9-worker-coder-7-001
logical_role_id: coder-7
specialist_identity_id: W9-CODER-7-CROSS-IMPLEMENTATION
task_id: C7-R2-01-MESSENGER-ALT-CANDIDATE
task_generation: 3
candidate_write_authority: true
runtime_authority: false
---

# Coder 7 — Current Task

## Exact transport binding

Repository: `saeedfaai/World-9`

Branch: `manager/external-grok-bridge-v0-1`

Required reads:

- `external_worker_bridge/coder-7/BRIDGE_MANIFEST.json`
- `external_worker_bridge/coder-7/EXTERNAL_CANDIDATE_PROTOCOL.md`
- this `CURRENT_TASK.md`

Exact allowed candidate root:

`external_worker_bridge/coder-7/candidate_outbox/C7-R2-01-MESSENGER-ALT-CANDIDATE/**`

No other write path is authorized by this task.

## Goal

Independently implement a provider-neutral Messenger candidate that repairs three semantic classes without copying private implementation code:

1. **source-bound command provenance** — a material directive must be bound to an exact sender identity/role, immutable message/work reference and integrity material; chat text such as “from Titi” alone is insufficient authority;
2. **schema/version exactness** — incompatible or unknown message/envelope versions fail closed rather than being silently accepted;
3. **ACK recipient binding** — an acknowledgement must prove it acknowledges the exact message intended for the acknowledging recipient; recipient/message mismatch must fail closed.

This is an alternate implementation candidate, not a patch applied to canonical/runtime source.

## Required candidate file set

Create a self-contained, dependency-light candidate under the exact allowed root containing at minimum:

- `MANIFEST.json` — worker/task/source snapshot, file hashes or hash-ready inventory, implementation language/runtime, assumptions, no-authority declaration;
- `README.md` — contract, failure semantics, integration boundary;
- `schemas/message-envelope.schema.json` — language-neutral envelope contract;
- `schemas/ack.schema.json` — ACK contract;
- `src/` — pure reference implementation for provenance validation, version validation and ACK recipient/message binding;
- `tests/` — executable positive and negative tests;
- `TESTS.json` — what was executed, exact command/runtime and results; mark anything not run as `NOT_EXECUTED`;
- `HANDOFF.json` — blockers, integration assumptions, next safe action.

Preferred implementation shape: language-neutral JSON contracts plus a small pure TypeScript reference implementation with no network/database/secret dependency. If the Grok environment cannot execute TypeScript, it may use another portable language only if the manifest records the choice and the JSON contracts remain language-neutral.

## Required negative cases

At minimum include tests that reject:

- sender/role claim not bound to trusted source metadata;
- message integrity/reference mismatch;
- unknown or unsupported schema version;
- ACK for a different message id;
- ACK emitted by or for the wrong recipient;
- missing recipient binding;
- malformed provenance fields;
- replay/duplicate acknowledgement when the contract marks ACK as single logical acknowledgement.

## Architecture boundaries

Do not invent runtime authority, secrets, DB state or canonical writer bindings.
Do not access or reconstruct private source code.
Do not merge or promote.
Do not call your own candidate Bug-Gate PASS or independent-review PASS.
A successful local test is candidate evidence only.

## Completion

One `Run` performs only this task.

After writing the real candidate file set and running whatever local tests are actually available, return only:

`EXTERNAL_CANDIDATE_READY | worker_id=w9-worker-coder-7-001 | task_id=C7-R2-01-MESSENGER-ALT-CANDIDATE | repo=saeedfaai/World-9 | branch=manager/external-grok-bridge-v0-1 | candidate_root=external_worker_bridge/coder-7/candidate_outbox/C7-R2-01-MESSENGER-ALT-CANDIDATE | commit=<exact-commit> | tests=<PASS_CANDIDATE|PARTIAL|NOT_EXECUTED> | state=<READY_FOR_TITI_INGESTION|BLOCKED_...> | runtime_authority=false`

Then stop. Do not start C7-R2-02 in the same Run.
