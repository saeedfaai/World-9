# State Machines and Forbidden Transitions

## Principal existence

```text
PROPOSED → GENESIS_PENDING → ACTIVE → RETIRED → TOMBSTONED
```

Forbidden:
- `PROPOSED → ACTIVE`
- expired `GENESIS_PENDING → ACTIVE`
- tombstone that erases commitments/history/accountability

## Operational state

```text
RUNNING ↔ PAUSED
RUNNING → QUARANTINED
PAUSED → MAINTENANCE
```

A Principal cannot unilaterally remove governance quarantine on itself.

## Migration state

```text
NONE → PREPARING → FENCED → TRANSFERRING → VERIFYING → NONE
                       \→ UNCERTAIN
```

Forbidden:
- target write before durable source fencing;
- source write after certified fence;
- Principal self-verification;
- activation with stale/equal epoch;
- continuation claim while both engines retain canonical write authority.

## Succession state

```text
NORMAL → TEMPORARY_ABSENCE → SUCCESSION_HOLD → TRANSFER_PENDING → TRANSFERRED
                                             \→ SUCCESSION_DISPUTE
```

Forbidden:
- timeout → invented holder;
- RootPrincipal → HumanRootOffice holder by self-appointment;
- unauthorized high-risk constitutional effect during unresolved dispute.

## Commitment state

Type-aware superset:

```text
PROPOSED → OFFERED → ACCEPTED → BINDING
BINDING → FULFILLED | BREACHED | DISPUTED | NOVATED | WAIVED | TERMINATED | EXPIRED
OFFERED → REJECTED
```

Forbidden:
- Task close → Commitment deletion;
- bilateral `OFFERED → BINDING` without required acceptance evidence;
- Worker without `can_bind` → binding transition;
- waiver/termination without type-required authority/evidence.

## Reservation state

```text
PROPOSED → RESERVED → CONSUMING → SETTLED
RESERVED/CONSUMING → RELEASED | EXPIRED | RECONCILIATION_REQUIRED
```

Forbidden:
- terminal WorkOrder with unexplained active reservation;
- silent reservation deletion after crash;
- new reservation over valid available envelope.

## Objective refinement

```text
DRAFT → STRUCTURAL_CHECK → SAFE_REFINEMENT | CONDITIONAL_REFINEMENT | UNKNOWN_REFINEMENT
```

- SAFE may continue through normal governance.
- CONDITIONAL requires semantic assessment/evidence and configured governance decision.
- UNKNOWN cannot activate.

Semantic/LLM assessment MUST NOT convert structural FAIL into PASS.

## Grant state

```text
DRAFT → ACTIVE → DRAINING | EXPIRED | REVOKED | CLOSED
```

Forbidden:
- effect after expiry/revoke outside configured drain semantics;
- child grant wider on any constrained dimension;
- WorkOrder-only authority;
- self-minted Principal authority.

## High-risk decision

```text
REQUESTED
→ NARRATIVE_AVAILABLE
→ EVIDENCE_PACK_AVAILABLE
→ COUNTEREVIDENCE_AVAILABLE_OR_POLICY_SATISFIED
→ DECISION
```

Forbidden:
- high-risk approval/override without required EvidencePack;
- requester-only evidence where independence policy requires separation.

## Global forbidden paths

1. Brain/provider/session/engine becomes canonical Principal identity.
2. Principal directly edits committed canonical history.
3. Principal promotes its own checker/change without independent evaluation.
4. World 9 creates a sixth governance plane by implementation accident.
5. External unverified constraint becomes a global hard prohibition.
6. Same Principal has two valid canonical write epochs.
7. Root narrative suppresses the only independent evidence path.
8. Budget shrink silently deletes valid exposure.
9. Breach or insolvency automatically erases Principal identity.
10. Principal exceeds declared Worker/Grant/WorkOrder/delegation limits.
