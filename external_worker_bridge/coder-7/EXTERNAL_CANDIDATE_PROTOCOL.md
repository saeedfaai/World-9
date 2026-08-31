---
schema: W9_EXTERNAL_CANDIDATE_TRANSPORT/1.1
canonical_truth: false
transport_only: true
worker_id: w9-worker-coder-7-001
logical_role_id: coder-7
specialist_identity_id: W9-CODER-7-CROSS-IMPLEMENTATION
runtime_authority: false
merge_authority: false
promotion_authority: false
---

# World 9 — Coder 7 External Candidate Transport

This public surface exists because the current Grok connector cannot see the private Project Control repository. It is transport/staging only. It is not canonical Project Control, runtime source, a sixth W8 plane, or an authority store.

## Identity

- `worker_id=w9-worker-coder-7-001`
- `logical_role_id=coder-7`
- `specialist_identity_id=W9-CODER-7-CROSS-IMPLEMENTATION`
- current transport: Grok/xAI

Provider, room, session, GitHub actor and connector are replaceable transport surfaces and are not sufficient identity or authority proof.

## Transport selection — no probes

At the start of a Run, inspect only the tools/actions already exposed by the platform. Do not create any object merely to test capability.

For a task that explicitly authorizes candidate output, select the first available transport below:

1. `BRANCH_FILE_OUTBOX`: create the real candidate files only inside the exact allowed branch/path named by `CURRENT_TASK.md`.
2. `ISSUE_COMMENT_OUTBOX`: if branch file mutation is unavailable but issue-comment mutation is available, post exactly one real structured candidate bundle as a comment on the exact issue named by `CURRENT_TASK.md`.
3. `CHAT_RELAY_OUTBOX`: if no GitHub mutation action is available, return exactly one real structured candidate bundle in chat for HumanRoot relay to Titi.

Capability inspection is read-only. Never use dummy/probe/noop/placeholder/scratch/STOP/test-write objects.

## Candidate discipline

For every Run:

1. re-read `BRIDGE_MANIFEST.json`, `CURRENT_TASK.md`, and this protocol;
2. verify exact worker/task/transport bindings;
3. execute exactly one bounded task;
4. create only the real files/content required by that task;
5. include a candidate manifest identifying worker, task, source snapshot, files, tests actually executed, tests not executed, assumptions, blockers and next safe action;
6. stop after one task.

A GitHub issue comment or chat bundle is transport-only evidence, not a weaker architecture. Titi must ingest it into the governed private evidence flow before any later gate can use it.

## Candidate boundary

A candidate is a detached Development proposal. It cannot directly edit private runtime/base/canonical source and cannot self-promote.

Forbidden:

- direct runtime or canonical integration;
- DB writes, migrations, production effects;
- secret/private credential access;
- changing private Task Feed or Work Permits;
- modifying another worker candidate;
- self-review, Bug Gate acceptance, merge or promotion;
- claiming `NOT_EXECUTED` as PASS;
- publishing private source copied from inaccessible repositories.

External research is allowed read-only and must be labeled `EXTERNAL_EVIDENCE`. Independent implementation must be based only on the public task contract and public standards/research, not guessed private code.

## Traffic-light completion status

Every completed Run must report exactly one execution light:

- `🟢 GREEN`: the bounded task completed and required evidence/output exists. This does not mean Bug Gate, merge, promotion, runtime or production PASS.
- `🟡 YELLOW`: the task did not fully complete, but the exact cause and next safe fix are known.
- `🔴 RED`: the task did not complete and the cause/evidence is still insufficient or unknown.

The light describes this Run only.
