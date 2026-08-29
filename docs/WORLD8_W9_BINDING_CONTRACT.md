# World 8 ↔ World 9 Binding Contract

Purpose: bind World 9 Principal semantics to the fixed five-plane World 8 architecture without creating a sixth plane.

## Binding rule

Every World 9 object MUST declare:

```text
W8 plane
canonical vs operational status
authoritative writer
allowed readers
activation / promotion path
enforcement point
recovery / replay behavior
evidence requirements
```

Exact database table and RPC names MUST be resolved against the active World 8 implementation before schema work. R0.1 deliberately does not fabricate table names.

## PrincipalRecord / PrincipalContract

**World 8 basis:** Entity identity and canonical governance namespace.

- Principal identity is backed by an existing World 8 Entity identity.
- Principal activation is canonical.
- Direct Principal writes to canonical activation state are forbidden.
- Activation follows governance/promotion.
- Operational read models may exist but cannot redefine canonical Principal status.

**Pre-schema question:** identify the exact active Entity persistence surface and decide whether Principal fields are represented by a dedicated canonical aggregate or governed extension artifact.

## ObjectiveBinding

**World 8 basis:** versioned canonical Objective Contract.

- ObjectiveBinding references an immutable Objective Contract version.
- Binding activation/change is canonical.
- Structural refinement checker artifacts are governed.
- Constitutional objective replacement uses the existing constitutional/governance path.

## AuthorityGrant

**World 8 basis:** authority/grant/policy enforcement and effect authorization.

Requirements:

- grant creation/revocation is attributable;
- commit/effect enforcement validates all applicable authority dimensions;
- effect executor cannot create its own grant;
- WorkOrder is not authority;
- stale/expired grants fail according to `IMMEDIATE | DRAIN` policy.

**Pre-schema question:** name the exact commit-time and effect-time enforcement hooks in the active World 8 implementation.

## WorkOrder

**Plane:** Operational.

A WorkOrder coordinates execution and may reference a Gap, Human request, Commitment remediation, Objective refinement or other authorized trigger.

A WorkOrder does not automatically become a Mason proposal. If it requests code/schema/policy change, the resulting candidate MUST enter Development/Mason and independent evaluation.

## Commitment

**Placement:** canonical obligation state/history in Canonical Spine; operational read models MAY exist.

Requirements:

- binding transitions are canonical;
- external communication receipts may live operationally/evidence-side until a binding transition occurs;
- Task/WorkOrder closure cannot delete a binding commitment;
- recovery must reconstruct active commitments.

Exact aggregate/event representation is resolved only after the active Spine implementation is inspected.

## Budget / Reservation / Exposure

**Plane:** Operational coordination; policy/ceiling changes are governed.

- reservation/settlement transitions are durable and replayable;
- budget ceiling changes are governed;
- overhang/insolvency observations feed Observation/Governance;
- no hidden in-memory reservation is authoritative after restart.

## Observation

**Plane:** Observation.

Observer emits attributable measurements/signals and cannot directly mutate Commitment or Principal canonical state.

Examples include protected-metric degradation, repeated refusal, apparent external promise, budget overhang, dual-active attempts and evidence-suppression indicators.

## EvidencePack

**Plane:** Evidence/Governance, built from references originating in Observation, Canonical Spine and operational receipts.

- producer identity and policy versions are recorded;
- requester cannot be sole evidence producer where high-risk independence policy requires separation;
- pack digest and source refs become immutable once used for a governed decision.

## GovernanceActorBinding

**Plane:** Evidence/Governance.

Every evaluator, verifier and Promotion Authority decision used by World 9 binds to accountable identity/credential/build/model references as applicable.

## CanonicalPrincipalContinuityCertificate

**Planes:** Canonical Spine + Evidence/Governance + fencing/recovery runtime evidence.

Requirements:

- verifier ≠ migrating Principal;
- source fencing evidence comes from enforcement infrastructure;
- target activation cannot precede durable source revocation;
- stale source writes are rejected by the authoritative fencing boundary.

## RootOffice / Succession

**Placement:** constitutional/canonical governance state.

Operational absence detection may be non-canonical, but holder transfer and succession resolution are canonical governance actions.

Timeout detection MUST NOT create a new holder by itself.

## PrincipalIsolationProfile

A governed policy/artifact spanning Operational enforcement, Evidence/Governance definition and canonical binding to Principal.

Isolation checkers themselves are governed artifacts.

## Principal Layer bootstrap

All Principal Layer code, policy, schema, checkers and migrations are World 8 governed candidates:

```text
candidate
→ Development / Mason
→ independent evaluator
→ Promotion Authority
→ activation / release
```

No RootPrincipal exception exists.

## Plane placement summary

| W9 concern | W8 plane(s) |
|---|---|
| Principal identity/activation | Canonical Spine |
| ObjectiveBinding | Canonical Spine + Evidence/Governance |
| WorkOrders/runtime coordination | Operational |
| Grants/effect execution | Operational + canonical authorization |
| Commitments | Canonical Spine + operational read models |
| Budget reservations | Operational; policy changes governed |
| Drift/breach/apparent promises | Observation |
| Candidate code/checkers | Development/Mason |
| Evaluation/evidence/promotion | Evidence/Governance |
| Continuity activation | Canonical Spine + Evidence/Governance + fencing runtime |

## No-sixth-plane test

If a proposed World 9 component cannot be assigned to one or more existing World 8 planes with an explicit writer and governance path, it cannot be admitted to R0.1 implementation without architecture revision.
