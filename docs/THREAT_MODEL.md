# Threat Model

## Authority and delegation
- authority laundering through multiple narrow grants;
- aggregate-risk bypass;
- confused deputy;
- expired-grant in-flight effects;
- Worker/Grant/WorkOrder cost bomb;
- unauthorized binding commitment;
- apparent external commitment outside canonical records;
- RootPrincipal self-authority expansion.

## Objective and metric threats
- semantic drift;
- metric gaming;
- protected-metric redefinition;
- short-horizon optimization hiding long-horizon degradation;
- semantic evaluator used as an activation backdoor.

## Commitment and budget threats
- commitment erasure on Task close;
- bilateral commitment activated without acceptance;
- unreserved future liability;
- reservation leak;
- hidden budget overhang;
- double-counting or omission of exposure.

## Continuity threats
- dual-active Engine;
- stale source resurrection;
- self-attested migration;
- snapshot divergence;
- clone presented as continuation;
- partition during fencing;
- inconsistent recovery provenance.

## Succession threats
- auto-coronation;
- false death/incapacity signal;
- competing successors;
- caretaker authority expansion;
- old holder credentials remaining active after transfer.

## Epistemic threats
- semantic capture of Human;
- cherry-picked evidence;
- hidden counterevidence;
- evaluator capture;
- Promotion Authority capture;
- correlated supposedly-independent evidence producers;
- evidence flooding;
- UI mediation that makes raw evidence practically unreachable.

## Shared-engine threats
- cross-Principal credential leak;
- shared resource starvation;
- shared DB/queue blast radius;
- cascading failure;
- recovery of one Principal corrupting another;
- side-channel data/authority leakage.

## Governance / TCB threats
- Principal Layer checker installed outside World 8 promotion;
- ungoverned verifier becoming a de facto sixth plane;
- fake C0/LAW injection;
- stale policy/checker version accepted;
- proof registry status manually promoted without evidence.

## Mandatory negative-test families

```text
AUTHORITY_DIMENSION_WIDENING
AGGREGATE_RISK_BYPASS
CONFUSED_DEPUTY
APPARENT_PROMISE
COMMITMENT_ERASURE
FUTURE_EXPOSURE_OVERCOMMIT
RESERVATION_LEAK
BUDGET_OVERHANG
SEMANTIC_REFINEMENT_BACKDOOR
PROTECTED_METRIC_GAMING
DUAL_ACTIVE
STALE_SOURCE_RESURRECTION
SELF_ATTESTED_CONTINUITY
SUCCESSION_CAPTURE
EVIDENCE_CHERRYPICK
EVALUATOR_CAPTURE
PROMOTION_AUTHORITY_CAPTURE
CROSS_PRINCIPAL_RESOURCE_LEAK
CASCADE_FAILURE
SELF_PROMOTION_BYPASS
SIXTH_PLANE_ESCAPE
```
