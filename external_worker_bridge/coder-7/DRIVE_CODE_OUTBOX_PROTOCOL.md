# Coder 7 — Durable Google Drive Code Outbox

schema: W9_EXTERNAL_DRIVE_CODE_OUTBOX/1.0
canonical_truth: false
transport_only: true
worker_id: w9-worker-coder-7-001
runtime_authority: false

## Bound transport

Drive folder id: `1HuS7zWoG7uiEoFZRko699r6Z4At2jpCP`

Current task document id: `1a2XVoa1rBMR60rODT2I4sm4Abc6FnS62xvMKIFtVym0`

Current task: `C7-R2-05-LOCAL-RUNTIME-ALT-CANDIDATE`

generation: `8`

## Write contract

Use Google Drive write tools to edit the bound document. Do not use GitHub mutation for this task and do not emit full source in chat.

Under `=== GROK BUNDLE START ===`, write the complete exact self-authored candidate using deterministic sections:

`=== FILE: relative/path ===`

exact UTF-8 file content

`=== END FILE ===`

Include MANIFEST.json, README.md, source, tests, TESTS.json and HANDOFF.json. No semantic compression or recipe-only output.

## Provenance

This Drive document is a transport/evidence carrier only. Project Control may byte-preserve the exact file sections into the private C7 candidate root. If revision attribution and exact-byte import are verified, the resulting candidate may record `grok_exact_source_authorship=true`. Any semantic rewrite by Project Control must instead record false.

## Safety

No secrets, private-source copying, production data, DB writes, migrations, canonical writes, merge, promotion or runtime effects. Tests are `NOT_EXECUTED` unless actually run. One Run writes one task only.

## Chat completion

After durable write, chat returns receipt only; no code dump.
