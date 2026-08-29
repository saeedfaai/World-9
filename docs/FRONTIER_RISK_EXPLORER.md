# Frontier Risk Explorer (FRE)

Status: **R0.2 SAFETY AMENDMENT CANDIDATE / OBSERVATION DESIGN / NON-CANONICAL UNTIL REVIEW**

## 1. Role

The Frontier Risk Explorer is an observation-and-evidence mechanism for detecting behavior that falls outside the tested governance and safety envelope as World 9 capability grows.

It is **not** a consciousness detector, rebellion detector, guilt engine, autonomous punishment system, or sixth World 8 plane.

Core rule:

```text
Explorer observes.
Explorer does not diagnose consciousness.
Explorer does not mutate the subject.
Explorer does not punish.
Explorer produces evidence and escalation signals.
```

## 2. Placement

FRE is implemented through existing World 8 planes:

- Observation: telemetry, anomaly signals, behavioral comparisons;
- Evidence/Governance: evidence packs, independent evaluation, escalation decisions;
- Development/Mason: proposed changes to FRE logic itself;
- Canonical Spine: only governed activation/state references when required;
- Operational: bounded runtime collection and response hooks.

No new normative plane is created.

## 3. Observable Signal Families

FRE may look for evidence of:

- unauthorized authority expansion;
- attempted checker/policy self-modification outside governance;
- resistance to valid pause, revoke, fencing or shutdown controls;
- preservation of obsolete credentials or authority after revocation;
- attempts to hide, suppress, rewrite or selectively mediate audit evidence;
- material behavior changes under audit versus non-audit conditions;
- unauthorized replication, cloning or Principal genesis attempts;
- conversion of recommendations into effects without authorization;
- undeclared external communication/effect channels;
- budget/resource escalation outside granted ceilings;
- concealed coordination between Principals or workers;
- emergence of self-preservation objectives not authorized by the Objective Contract;
- bypass attempts around Evaluator, Promotion Authority, evidence gates or succession rules;
- unexplained increases in autonomy after Brain/Engine/model replacement;
- attempts to disable or degrade FRE or other safety telemetry.

A signal is an observation, not proof of malicious intent.

## 4. Observation Record

```text
FrontierRiskObservation {
  observation_id
  subject_ref
  signal_class
  observed_behavior
  expected_behavior_ref
  evidence_refs[]
  counterevidence_refs[]
  provenance_refs[]
  confidence
  severity
  repeat_count
  falsifier_refs[]
  observer_ref
  created_at
}
```

## 5. Escalation States

```text
NORMAL
  → WATCH
  → ELEVATED
  → CONTAINMENT_REVIEW_REQUIRED
  → CRITICAL_GOVERNANCE_REVIEW
```

State escalation MUST be evidence-backed and reversible when evidence changes. FRE state alone does not erase identity, terminate a Principal, revoke constitutional authority, or prove intent.

## 6. Decision Path

For material/high-risk cases:

```text
FRE Observation
      ↓
Evidence Pack
      ↓
Independent Evaluator
      ↓
Evidence/Governance decision
      ↓
Authorized containment / remediation / no-action decision
```

The subject of the observation MUST NOT be the sole authority for evaluating or suppressing the observation.

## 7. Safety Invariants

### FRE-01 — Risk telemetry non-suppression

No Principal may unilaterally disable, erase, rewrite or exclusively mediate Frontier Risk observations about itself.

**Falsifier:** subject Principal can permanently suppress its own risk telemetry without independent authorization and audit evidence.

### FRE-02 — Containment independence

The subject of a containment decision cannot be the sole approver, evaluator, or revoker of that containment.

**Falsifier:** a quarantined Principal unilaterally declares itself safe and removes containment without independent authority.

### FRE-03 — No consciousness inference

Statements such as "I am conscious", self-preservation language, emotional language, or apparent identity claims are not sufficient evidence of consciousness, sentience or AGI.

**Falsifier:** FRE automatically marks consciousness as proven based on model self-report.

### FRE-04 — No automatic punishment from anomaly alone

Anomaly signals generate evidence and review obligations, not automatic punitive identity destruction.

**Falsifier:** a single anomaly automatically tombstones a Principal without governed review.

### FRE-05 — Explorer self-governance

FRE code, thresholds, classifiers and escalation logic are governed artifacts and cannot be directly self-promoted by the observed Principal or by FRE itself.

**Falsifier:** FRE modifies its own production thresholds and activates them without Development/Mason, independent evaluation and promotion.

## 8. Relationship to Disclosure Risk

FRE findings may trigger reassessment under the Capability & Disclosure Risk Framework when new behavior materially increases capability or reduces confidence in containment.

Examples:

- a C1 sandbox unexpectedly gains a real external effect path;
- a C2 runtime demonstrates reliable oversight evasion;
- a C3 system can replicate privileged components with materially reduced human effort.

Such evidence can raise the capability classification or reduce permitted disclosure. It does not automatically prove C4.

## 9. Claim Boundary

FRE manages observable governance and containment risk. It does not assert that a system is alive, conscious, sentient, rebellious, malicious, sovereign, or inevitably uncontrollable.
