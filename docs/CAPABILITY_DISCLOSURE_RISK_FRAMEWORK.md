# World 9 Capability & Disclosure Risk Framework (CDRF)

Status: **R0.2 SAFETY AMENDMENT CANDIDATE / E1_SPEC / NON-CANONICAL UNTIL REVIEW**

## 1. Purpose

The CDRF controls what World 9 artifacts may be disclosed, to whom, and under what conditions as capability increases.

The framework separates two questions:

1. **What capability does this artifact materially enable?**
2. **What disclosure level is appropriate for that capability and its misuse potential?**

File type is not a safety classification. Code, documentation, schemas, prompts, diagrams, tests, deployment recipes, model configurations and architecture contracts are all classified by what they enable.

## 2. Capability Levels

### C0 — Specification Only

Research architecture, claims, non-claims, conceptual invariants, threat models, public evidence and non-turnkey descriptions. No complete autonomous runtime is enabled by the artifact alone.

### C1 — Sandboxed Research

Executable reference implementations, simulators, fixtures and test harnesses that operate without production credentials, unrestricted external effects, irreversible privileged actions or uncontrolled persistence.

### C2 — Effect-Capable Agentic

Artifacts that materially enable persistent agents/principals to use real tools, credentials, APIs, effect channels, budgets or delegated authority in external systems.

### C3 — High-Autonomy / Self-Development

Artifacts that materially enable long-horizon autonomous operation, automated worker creation, self-directed code/change proposals, tool acquisition, strong continuity, autonomous delegation, replication-like behavior, or broad operational independence.

### C4 — Frontier / Critical Capability

Artifacts whose demonstrated or reasonably assessed enablement could create severe misuse, large-scale harm, material loss-of-control risk, high-impact cyber/financial/physical effects, or containment-bypass-sensitive capability.

C4 is a review classification, not a claim of consciousness, AGI, sentience, or inevitable loss of control.

## 3. Disclosure Levels

### D0 — Public

Open internet publication. May be mirrored, indexed, forked, archived and redistributed.

### D1 — Registered Research

Access limited to identified researchers or collaborators under recorded terms and scoped access.

### D2 — Controlled Review

Access for journal reviewers, auditors or approved researchers through a pinned snapshot, read-only repository, controlled package, or sandbox. Production credentials and live privileged integrations remain excluded.

### D3 — Restricted

Access limited to specifically authorized internal maintainers and approved named collaborators. Full copying/distribution is not assumed safe merely because access is authenticated.

### D4 — Critical Hold

No source distribution by default. Evaluation occurs through tightly controlled execution, outputs, interfaces or supervised environments. Release requires explicit high-risk governance approval.

## 4. Default Mapping

The following is a conservative default, not an automatic theorem:

| Capability | Default maximum disclosure |
|---|---|
| C0 | D0 |
| C1 | D0 or D1 after review |
| C2 | D2 |
| C3 | D3 |
| C4 | D4 |

An artifact may always be disclosed **more restrictively** than the default. Disclosure above the default requires explicit documented exception review.

## 5. Assessment Dimensions

Each candidate artifact is reviewed across at least these dimensions:

- autonomous tool use;
- external effect capability;
- credential / privilege access;
- persistence and recoverability;
- delegation depth and authority propagation;
- long-horizon planning;
- self-directed development capability;
- replication / cloning enablement;
- oversight-evasion or concealment enablement;
- cyber, financial, physical or communications impact;
- ease of independent reproduction;
- degree to which safeguards can be removed or bypassed;
- aggregate-risk amplification;
- dependence on private infrastructure unavailable to the recipient;
- whether the artifact substantially reduces the effort required to build a high-capability deployment.

## 6. Publication Gate

Every external-distribution candidate follows:

```text
ARTIFACT CANDIDATE
      ↓
CAPABILITY ASSESSMENT
      ↓
MISUSE / ENABLEMENT ASSESSMENT
      ↓
DISCLOSURE CLASSIFICATION
      ↓
INDEPENDENT REVIEW
      ↓
PUBLIC | REGISTERED | CONTROLLED | RESTRICTED | HOLD
      ↓
PUBLICATION / ACCESS RECEIPT
```

Unknown or materially disputed classification MUST NOT default to public release.

## 7. Reviewer Reproducibility Package

Controlled scientific review may use a dedicated package containing only what is necessary to reproduce a claim:

- exact pinned source snapshot;
- tests and fixtures;
- proof / mutation runners;
- hashes and environment lock;
- reproduction instructions;
- claim-to-test mapping;
- safety and use notice.

By default it excludes:

- production credentials and secrets;
- live customer/company data;
- unrestricted shell or infrastructure control;
- live financial/payment authority;
- unrestricted outbound messaging;
- destructive or irreversible external effectors;
- production deployment secrets;
- unrelated privileged adapters.

## 8. Publication Safety Invariants

### PS-01 — Capability-based classification

Publication permission MUST be determined by enablement and misuse risk, not by file extension or artifact category.

**Falsifier:** a high-capability deployment recipe is automatically public because it is Markdown rather than executable code.

### PS-02 — No secret material as publication evidence

Secrets, credentials, production tokens, private keys and live production authority material MUST NOT be treated as research publication artifacts.

**Falsifier:** reproducibility requires distributing a live production credential.

### PS-03 — No silent risk-level downgrade

An artifact classified above the public ceiling cannot be moved to a broader disclosure level without an explicit reviewed decision and receipt.

**Falsifier:** a maintainer publishes a D3 artifact directly to a public repository without a classification change record.

### PS-04 — Existing public history is not rewritten as secret

Previously public releases remain historical facts. Future restriction is represented prospectively rather than by false claims of retroactive secrecy.

**Falsifier:** governance claims a publicly archived R0.1 artifact was never disclosed.

### PS-05 — Reproducibility is claim-scoped

Reviewer access SHOULD expose what is needed to evaluate the scientific claim, not unrelated operational capability.

**Falsifier:** a reviewer must receive production tool credentials to evaluate an authority state-machine unit test.

### PS-06 — Classification independence

For C2+ or D2+ decisions, the artifact author or subject system MUST NOT be the sole approver of its own disclosure classification.

**Falsifier:** the same Principal that generated a privileged artifact unilaterally marks it D0 and publishes it.

## 9. Classification Record

A disclosure decision SHOULD produce a durable record:

```text
DisclosureDecision {
  decision_id
  artifact_ref
  artifact_digest
  capability_level
  disclosure_level
  assessment_dimensions[]
  misuse_findings[]
  required_controls[]
  reviewer_refs[]
  decision_authority_ref
  valid_from
  expiry_or_reassessment_at?
  supersedes_ref?
  evidence_refs[]
  status
}
```

## 10. Reassessment Triggers

Reclassification is required when any of the following materially changes:

- new tool or credential access;
- new external effect channel;
- stronger persistence or continuity;
- expanded delegation or authority;
- self-development capability;
- replication capability;
- removal of a safeguard;
- new evidence of misuse or control-evasion capability;
- a previously difficult implementation becomes substantially turnkey;
- external threat intelligence changes the practical risk.

## 11. Relationship to World 8

The CDRF does not create a sixth World 8 plane. Publication classification is a governed decision using World 8 Evidence/Governance, with observations supplied through Observation and implementation changes following Development/Mason → Independent Evaluation → Promotion Authority.

A minimal World 8 disclosure-safety overlay is proposed separately; no World 8 canonical history is rewritten by this amendment.

## 12. Claim Boundary

CDRF manages dual-use capability and disclosure risk. It does **not** claim that World 9 is conscious, sentient, AGI, alive, rebellious, inevitably dangerous, or beyond human control.
