# World 9 Implementation Start Gate

Status: **MANDATORY PRE-IMPLEMENTATION GATE**

No capability-bearing World 9 implementation may begin in the public repository.

## Gate A — publication boundary

Before implementation starts:

1. The public repository remains architecture/governance only at `C0 / D0`.
2. A separate **private** runtime repository exists and its visibility is independently verified as private.
3. The private repository has no public fork/mirror/release automation by default.
4. Secrets and production credentials are excluded from source control.
5. Reviewer/distribution access is handled separately from maintainer access.

## Gate B — initial runtime ceiling

The first executable milestone is constrained to **C1 / controlled sandbox research**:

- no production credentials;
- no live payment, financial, customer, messaging or infrastructure-control authority;
- no irreversible external effects;
- no autonomous replication;
- no unrestricted shell or arbitrary network egress by default;
- no automatic self-promotion of generated code;
- no persistent authority outside test fixtures;
- deterministic shutdown/pause path required;
- complete effect receipts required for every simulated effect.

Advancing beyond C1 requires a new Capability & Disclosure assessment and independent review.

## Gate C — World 8 binding before schema

Implementation must not invent a parallel truth store. Before the first schema is activated, the exact active World 8 bindings must be resolved for:

1. Principal record / World 8 Entity mapping;
2. commitment persistence;
3. WorkOrder entry path;
4. AuthorityGrant enforcement point(s);
5. EvidencePack producer/holder;
6. ContinuityCertificate canonicalization;
7. effect receipt Principal/delegation/provenance binding;
8. exact epoch/fencing mechanism that serializes Principal writes.

Unknown binding => no schema activation.

## Gate D — development governance

Every implementation work item must have:

- exact objective and capability ceiling;
- disclosure classification;
- isolated branch/workspace;
- author/actor identity;
- test obligations and falsifiers;
- error/repair journal and reusable diagnostic record;
- checkpoint with `next_safe_action`;
- independent evaluation before promotion of materially capability-increasing changes.

## Gate E — public-transfer prohibition

No file from the private runtime repository may be copied, mirrored, attached to a public release, pasted into a public issue, or moved into this repository unless it first receives an explicit D0 public classification.

This includes source, configuration, schemas, prompts, tests, diagrams and operational documentation.

## Initial implementation objective

The first allowed implementation objective is limited to a **C1 local/sandbox Principal kernel** proving identity/accountability/authority semantics without live external effect capability.

The first implementation phase MUST NOT attempt general autonomy, self-expansion, autonomous tool acquisition or production deployment.