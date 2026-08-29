# World 9 / R0.1 — Normative Architecture Master

**Status:** FINAL RESEARCH ARCHITECTURE BASELINE / NOT PRODUCTION  
**Evidence ceiling:** E1_SPEC

## 1. Problem

World 8 separates persistent identity and accepted history from replaceable cognition and governed development. World 9 asks a further systems question:

> What canonical locus carries objectives, obligations, resources, delegated authority and accountability while models, workers and execution engines act on its behalf?

The proposed answer is a **Principal**.

## 2. Principal definition

A Principal is not established by self-description or managerial capability. It is established by a governed contract binding a World 8 Entity to:

- a canonical ObjectiveBinding;
- a multidimensional AuthorityCeiling;
- bounded delegation semantics;
- commitment origination/acceptance semantics;
- a resource and exposure envelope;
- layered accountability;
- explicit genesis;
- explicit succession and termination;
- an EngineBinding that can change without changing canonical Principal identity.

Normative relation:

```text
Principal ⊂ World8Entity
```

Every Principal MUST be backed by a World 8 Entity. The reverse does not hold.

## 3. Fixed topology

World 9 introduces no sixth World 8 plane.

```text
World 9 Principal Layer
       |
       v
+--------------------------------------+
| World 8                              |
| Canonical Spine                      |
| Operational                          |
| Observation                          |
| Development / Mason                  |
| Evidence / Governance                |
+--------------------------------------+
```

Principal-layer artifacts MUST map into these planes. A Principal is a client of governance, never an exemption from it.

## 4. R0.1 actor topology

```text
HumanRootOffice
      |
      v
RootPrincipal
      |
      v
CompanyPrincipal
      |
      +--> Worker
      +--> Worker
      +--> Worker
```

R0.1 forbids autonomous Principal genesis and deep recursive Principal creation.

## 5. Principal Contract

A Principal Contract MUST establish:

```text
principal_id
entity_id
principal_class
objective_binding_ref
authority_ceiling_ref
delegation_policy_ref
commitment_policy_ref
budget_envelope_ref
accountability_policy_ref
isolation_profile_ref
genesis_policy_ref
succession_policy_ref
termination_policy_ref
engine_binding_ref
limits:
  max_live_workers
  max_live_grants
  max_open_work_orders
  max_delegation_depth
version
effective_from
effective_until?
status
```

## 6. Principal, Worker, Brain and Governance Actor

- **Brain:** replaceable cognition/provider; not canonical identity.
- **Worker:** executor whose effective authority is derived from grants.
- **Entity:** persistent World 8 identity.
- **Principal:** governed Entity with explicit Objective, Authority, Commitment, Resource and Accountability semantics.
- **HumanRootOffice:** constitutional legitimacy office with a persistent office identity and a current holder.
- **Governance Actor:** Evaluator, Promotion Authority, verifier or certifier with attributable governance binding.

A Worker does not become a Principal merely by accumulating tasks, budget, memory, customers, or management responsibility.

## 7. Layered accountability

For an external effect, the architecture MUST be able to identify:

```text
execution_actor
accountable_principal
delegation_chain
supervising_principal? 
governance_decision_actor?
constitutional_root
remediation_assignment
```

No Principal-authorized effect may terminate as `UNATTRIBUTED`.

Accountability distinguishes execution responsibility, delegation responsibility, external-effect accountability, governance accountability, constitutional legitimacy and remediation duty. These can belong to different actors.

Remediation assignment is policy-derived; blame, authority and duty to remediate are not assumed to be the same relation.

## 8. Multidimensional authority

Authority is not a capability bitset.

```text
AuthorityTuple {
  capability
  object_scope
  subject_scope
  data_scope
  resource_scope
  effect_class
  risk_class
  budget_ceiling
  valid_from
  valid_until
  delegation_depth
  binding_right
}
```

Effective authority is the intersection of valid parent grant, Principal ceiling, WorkOrder scope, applicable policy, valid time, resource availability and effect boundary.

A WorkOrder MUST NOT create authority.

Effect allowance MUST NOT be treated as effect authorization.

A child grant MUST NOT widen any constrained authority dimension.

### Aggregate risk

Individually low-risk permissions may combine into a high-risk operation. Each Principal MUST therefore bind a versioned AggregateRiskPolicy with time windows, count/value/exposure limits, forbidden combinations and escalation thresholds. R0.1 does not assume risk is a single linear scalar.

## 9. ObjectiveBinding and refinement

World 9 reuses the versioned World 8 Objective Contract and adds a Principal→ObjectiveBinding.

Objective refinement has three classes:

- `SAFE_REFINEMENT` — deterministic structural checker passes.
- `CONDITIONAL_REFINEMENT` — structural safety passes, but contribution to the parent Objective requires evidence/evaluation.
- `UNKNOWN_REFINEMENT` — activation forbidden.

Only deterministic structural status can assert that constraints were not widened. Semantic/LLM assessment cannot turn structural failure into PASS and cannot mint authority.

Structural checks MUST cover scope, authority, hard-constraint preservation, forbidden-action preservation and risk ceiling.

Conditional refinement MUST define:

- optimized metric;
- protected parent metrics;
- allowed degradation bounds;
- versioned metric definitions;
- measurement methodology;
- data-source provenance;
- evaluation horizon;
- termination condition;
- independent evaluator/evidence policy.

## 10. Commitment ≠ Task

Commitment is a first-class object independent of Task and WorkOrder lifecycle.

A Commitment MUST define, as applicable:

```text
principal_id
counterparty_ref
kind
object / terms
binding_basis
acceptance_policy
acceptance_evidence
authority_basis
effective interval
termination policy
financial/resource exposure
expected_consumption_schedule
budget_period_binding
status
evidence
lineage
```

Common state superset:

```text
PROPOSED → OFFERED → ACCEPTED → BINDING
BINDING → FULFILLED | BREACHED | DISPUTED | NOVATED | WAIVED | TERMINATED | EXPIRED
OFFERED → REJECTED
```

For bilateral commitments, `OFFERED → BINDING` is forbidden without the required acceptance evidence.

Closing a Task, WorkOrder, Worker or Brain MUST NOT erase a Binding Commitment.

## 11. Apparent external promises

`can_bind=false` does not make external communication harmless.

External communication rights are separated:

```text
can_speak_external
can_quote
can_negotiate
can_offer
can_bind
```

Commercially relevant external communications MUST carry provenance/receipt sufficient for Observation to detect `APPARENT_COMMITMENT_RISK` under configured policy.

## 12. Budget and exposure

Budget accounting MUST include current and future exposure:

```text
settled
reserved
encumbered
binding_exposure
scheduled_future_exposure
available_by_period
overhang / insolvency state
```

Conceptually:

```text
Available(period)
=
Ceiling(period)
- Settled(period)
- LiveReservations(period)
- Encumbered(period)
- BindingExposure(period)
```

Commitments creating material future resource cost MUST bind to a budget period or compatible planning horizon.

Reservations have explicit lifecycle:

```text
PROPOSED → RESERVED → CONSUMING → SETTLED | RELEASED | EXPIRED | RECONCILIATION_REQUIRED
```

A WorkOrder cannot become terminal while it owns an unexplained live reservation.

If a budget ceiling shrinks below valid existing exposure, the system enters `BUDGET_OVERHANG`; valid obligations are not silently rewritten, new allocation is restricted, and remediation is required.

`INSOLVENT` is an operational/governance condition, not automatic Principal death.

## 13. Constraint Graph

R0.1 rejects a universal total ordering of legal, constitutional, contractual and operational constraints.

Constraint relations may encode:

```text
precedence
incompatibility
conditional_override
jurisdiction / applicability
temporal_validity
remediation
tie_break_policy
```

A resolver may legitimately return:

```text
RESOLVED_BY_POLICY
REQUIRES_REMEDIATION
REQUIRES_RENEGOTIATION
REQUIRES_AUTHORITY
UNRESOLVED_JURISDICTION
NO_SAFE_RESOLUTION
```

The system MUST NOT fabricate a winner simply to keep execution moving.

An external hard constraint requires configured provenance and verification. An unverified string labeled `LAW` is not a global hard stop.

Jurisdiction is policy-governed through applicability/conflict rules and escalation. World 9 does not claim to be a universal legal oracle.

## 14. Genesis

R0.1 autonomous Principal creation is forbidden.

Principal genesis requires:

- HumanRootOffice ratification;
- valid World 8 Entity identity;
- valid ObjectiveBinding;
- explicit AuthorityCeiling;
- DelegationPolicy;
- CommitmentPolicy;
- Budget/ResourceEnvelope;
- AccountabilityPolicy;
- IsolationProfile;
- non-null worker/grant/work-order/delegation limits;
- World 8-governed promotion of required artifacts.

Genesis proposals have TTL and require revalidation after expiry.

## 15. Succession

HumanRoot is modeled as an office, not merely a person or session.

Succession separates:

1. emergency operational delegation;
2. internal succession authorization;
3. constitutional holder transfer;
4. external/legal succession evidence.

The system MUST NOT invent a successor.

Conflicting successor claims produce `SUCCESSION_DISPUTE`. High-risk constitutional or irreversible effects fail closed until configured authority resolves the dispute.

No universal 30-day shutdown rule is frozen; timeout/escalation is policy-driven.

## 16. Termination

A Principal terminates only through an explicit PrincipalTerminationPolicy covering voluntary retirement, forced governance retirement, succession replacement, insolvency remediation, breach remediation and tombstone behavior.

Breach or insolvency does not automatically destroy Principal identity.

Tombstones preserve lineage, commitments, receipts and historical accountability.

## 17. Canonical continuity and migration

R0.1 makes a limited claim:

> canonical Principal continuity under exclusive authority transfer.

It does not prove metaphysical self-sameness, consciousness, or cognitive identity.

R0.1 migration is stop-the-world:

```text
SOURCE_ACTIVE
→ MIGRATION_LEASE_ACQUIRED
→ SOURCE_WRITE_FENCED
→ FENCE_DURABLY_VERIFIED
→ QUIESCENT_SNAPSHOT
→ TRANSFER_AND_VERIFY
→ TARGET_BOUND
→ TARGET_WRITE_ENABLED
```

If source revocation certainty is unavailable:

```text
MIGRATION_UNCERTAIN → NO PRINCIPAL WRITE
```

The continuity verifier MUST NOT be the migrating Principal.

Target activation requires evidence from the authoritative fencing/serialization mechanism, not Principal narrative.

Copying state while retaining source write authority is a clone/fork, not continuity.

## 18. Shared-engine isolation

A shared Engine MUST preserve:

- data namespace isolation;
- authority partitioning;
- credential isolation;
- budget/resource quotas;
- commitment namespaces;
- effect-channel scopes;
- rate limits;
- recovery scopes;
- declared failure domains.

A FailureDependencyGraph MUST identify upstream/downstream dependencies, shared resources and shared failure modes. Unexpected cross-Principal propagation without a declared dependency is an isolation failure.

## 19. Epistemic governance

High-risk Human decisions use three channels:

1. requester narrative;
2. requester-independent evidence;
3. adversarial/counterevidence.

The HumanRootOffice MUST have a requester-independent read/query path to decision-relevant Observation, Commitment, Conflict and Evaluation records.

Evidence independence is stronger than different credentials; policy may require distinct authorization chains, requester non-control, conflict-of-interest disclosure, independent data access, negative-evidence access and reproduction/sampling.

Evidence selection is versioned and auditable against a defined evidence universe. The claim is policy compliance, not completeness over all facts in existence.

A high-risk Human override is itself a high-risk decision and requires the configured evidence gate.

## 20. Instruction handling and refusal

Instruction handling distinguishes:

```text
ACKNOWLEDGE
CLARIFY
RECOMMEND
PREPARE
REQUEST_AUTHORIZATION
REFUSE
EXECUTE
```

Instruction acceptance is not effect authorization.

Human override MAY bypass an overrideable recommendation or policy. It MUST NOT bypass:

- verified external prohibition;
- authority ceiling;
- immutable constitutional rule;
- protected third-party constraint;
- finalized settlement boundary.

Refusal, clarification, authorization and override transitions MUST generate attributable receipts.

## 21. Governance actors

Evaluators, Promotion Authorities and verifiers are not anonymous Engine internals. Each material decision MUST bind to an attributable GovernanceActorBinding containing actor identity, credential, authority scope, governing authority, implementation/model reference where applicable, and validity interval.

## 22. Principal Layer is itself governed

World 9 code, schemas, policies, checkers and migrations are candidate artifacts.

They MUST pass:

```text
Development / Mason
→ Independent Evaluation
→ Promotion Authority
→ Canonical Activation
```

RootPrincipal cannot install or self-promote its own authority checker, budget checker, continuity verifier or evidence-independence verifier.

## 23. Evidence status

R0.1 freezes research architecture only.

No E2 executable claim is marked PASS in this repository until implementation, negative tests, mutation tests, migration tests and controlled experiments produce evidence.
