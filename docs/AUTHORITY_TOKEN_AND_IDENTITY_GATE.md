# World 9 Authority Token & Identity Gate

Status: **R0.2 DESIGN CANDIDATE / E1_SPEC / C0-D0 PUBLIC CONCEPT ONLY**

## Purpose

World 9 requires delegated authority to remain attributable, bounded, identity-bound and monotonically attenuating as it moves from a Principal toward Workers or Contractors.

This document adds the architectural concept of a **World 9 Authority Token (W9-AT)** and a strict **Identity + Qualification Issuance Gate**. It intentionally does not publish the restricted runtime token format, signing implementation, key-management design, deployment recipe or live enforcement code.

## Core distinction

The Authority Token is **not a second authority truth store** and possession of a token is not sufficient by itself.

Canonical authority remains in the governed World 8 authority system. A W9-AT is a derived, integrity-protected capability envelope that references current governed authority and must be validated at the relevant enforcement boundary.

Therefore:

`Qualification != Authorization != Credential != Authority Token`

- Identity answers **who is acting**.
- Qualification answers **what competence was independently established**.
- Authorization answers **whether that subject may perform that action on that resource under current conditions**.
- The Authority Token carries the bounded delegated authority context to an authorized execution boundary.
- Credentials, when needed, are separately brokered and never become authority merely because they exist.

## Issuance gate

A Worker/AI MUST NOT receive a W9-AT unless all applicable evidence is valid at issuance time:

1. persistent Actor identity exists and is ACTIVE;
2. the concrete provider/session Execution is bound to that Actor;
3. required access-identity assurance is verified where the action requires it;
4. the capability-specific Academy qualification/checkride evidence is ACTIVE and unexpired;
5. when the task is governed development, the current Academy Coding Entry is valid for the exact Actor + Execution + Work + Workspace + Session context;
6. the underlying World 8 authorization decision is ALLOW for the requested action/resource/scope/conditions;
7. the issuer itself holds authority to delegate that subset;
8. the resulting token is no broader than the issuer/parent authority.

Academy success never creates authority by itself. It is a mandatory competence/admission precondition where policy requires it.

## Monotonic attenuation

Delegation is one-way narrowing.

For every child token:

`EffectiveChildAuthority ⊆ EffectiveParentAuthority`

A child MUST NOT widen any constrained dimension, including capability, object/subject/data/resource scope, effect class, risk class, budget ceiling, validity window, delegation depth or binding rights.

If a dimension cannot be proven to be equal-or-narrower, issuance fails closed.

A WorkOrder cannot mint authority and cannot widen a token.

## Identity binding

A W9-AT is bound to an accountable Actor and, where applicable, to the concrete Execution receiving it. A provider/model/session identifier alone is not identity.

Engine/model replacement does not inherit an old token merely because it continues the same task. The new Execution must be re-bound and revalidated according to policy.

Identity evidence must remain separate from self-asserted model text. An AI saying "I am actor X" is not identity proof.

## Integrity and non-bypass requirement

The restricted runtime implementation MUST make token modification detectable and MUST reject tokens that cannot be validated under the active issuer/key/authority policy.

No claim of absolute unforgeability is made: security depends on the integrity of keys, verifiers, canonical authority state and enforcement coverage. The design obligation is that forgery, widening, stale replay, subject substitution and verifier bypass are explicit falsifiers.

Critically, a valid-looking token MUST still fail when its referenced authority has been revoked, expired, superseded, fenced or otherwise invalidated by current canonical state.

## Enforcement rule

Where policy requires delegated authority, the operation MUST fail closed if any of the following is absent or invalid:

- token integrity;
- Actor/Execution binding;
- required Academy qualification/admission evidence;
- current underlying authorization;
- parent/delegation lineage;
- validity/epoch/fencing state;
- scope attenuation proof.

Possession of credentials, a WorkOrder, a model session, a Git branch, a tool connection or Academy qualification does not substitute for this gate.

## World 8 binding discovered before implementation

The active World 8 runtime already contains the pieces this design must reuse rather than duplicate:

- persistent Actor identity: `world8_actor_registry`;
- provider/session Execution identity: `world8_actor_executions`;
- access identity assurance: `world8_access_identity_bindings`;
- Academy checkride evidence and persistent qualification: `world8_academy_checkride_receipts` + `world8_actor_qualifications`;
- short-lived coding-context entry: `world8_academy_coding_entry_receipts`;
- unified authorization evaluation: `world8_authorize_v1`;
- immutable authorization evidence: `world8_authorization_receipts`;
- governed development path: `world8_dev_admission_check_v3` -> recovery -> `world8_dev_acquire_lease_v5`.

World 9 MUST bind to these surfaces or their governed successors. It MUST NOT create a parallel Actor registry, qualification truth or authority ledger.

## Design obligations / falsifiers

### AT-01 — No authority from qualification alone
Falsifier: a Worker with Academy qualification but no current authorization receives an effective W9-AT.

### AT-02 — Monotonic attenuation
Falsifier: any child token has a wider constrained dimension than its parent/effective issuer authority.

### AT-03 — Identity-bound authority
Falsifier: a token issued to Actor/Execution A can be used by Actor/Execution B without governed re-issuance.

### AT-04 — Current-state validation
Falsifier: a cryptographically intact token remains effective after the underlying authority is revoked/expired/fenced when policy requires immediate invalidation.

### AT-05 — No bearer-token bypass
Falsifier: token possession alone bypasses current identity, qualification, authorization or enforcement checks.

### AT-06 — Delegation lineage
Falsifier: an externally material effect executes without reconstructable Principal -> delegator -> Worker authority lineage.

### ID-01 — No self-asserted identity
Falsifier: provider/model/session text or caller-supplied actor name is accepted as sufficient identity proof.

### ID-02 — Academy-before-qualified delegation
Falsifier: policy requires a capability qualification but a token is issued without active evidence for that exact qualification/version.

## Disclosure boundary

The public architecture may state these invariants and interfaces. Exact token serialization, signing/key management, anti-replay mechanics, verifier hardening and capability-bearing integration remain subject to CDRF disclosure classification and may stay in the private runtime repository.
