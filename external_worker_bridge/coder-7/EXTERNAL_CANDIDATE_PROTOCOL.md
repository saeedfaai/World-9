---
schema: W9_EXTERNAL_CANDIDATE_TRANSPORT/1.0
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

This public branch is a transport/staging surface for an external Development candidate because the current Grok connector cannot see the private Project Control repository.

It is **not** canonical Project Control, runtime source, a sixth W8 plane, or an authority store.

## Identity

- `worker_id=w9-worker-coder-7-001`
- `logical_role_id=coder-7`
- `specialist_identity_id=W9-CODER-7-CROSS-IMPLEMENTATION`
- current transport: Grok/xAI

A GitHub actor, provider, room or session is not sufficient identity proof by itself.

## Write discipline

A Run may write only when the public `CURRENT_TASK.md` explicitly says `candidate_write_authority=true` and names one exact allowed path.

For that Run:

1. re-read `BRIDGE_MANIFEST.json`, `CURRENT_TASK.md`, and this protocol;
2. verify exact worker/task/branch/path bindings;
3. execute exactly one bounded task;
4. write only the real candidate files required by that task inside the exact allowed path;
5. never create dummy/probe/noop/placeholder/scratch/STOP/test-write artifacts;
6. include a candidate manifest identifying worker, task, source snapshot, files, tests actually executed, tests not executed, assumptions, blockers and next safe action;
7. stop after one task.

## Candidate boundary

A public candidate is a **detached Development proposal**. It cannot directly edit private runtime/base/canonical source and cannot self-promote.

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

## Return path

The candidate remains on this bridge branch until Titi/Project Control ingests its exact commit/file hashes into the private evidence/control flow. Ingestion does not equal merge or promotion.

If the platform cannot write the exact allowed public path, return `BLOCKED_EXTERNAL_CANDIDATE_WRITE_TRANSPORT`; do not widen scope or test with another path.
