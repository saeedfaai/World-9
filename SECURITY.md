# World 9 Security & Responsible Disclosure Boundary

Status: ACTIVE REPOSITORY POLICY / R0.2 SAFETY CANDIDATE

## Public-repository boundary

This repository is the **public research and governance surface** for World 9. It is not the approved location for a capability-bearing World 9 runtime.

Until an explicit governed reclassification changes this ceiling, the public repository is limited to **C0 / D0** material under `docs/CAPABILITY_DISCLOSURE_RISK_FRAMEWORK.md`.

### Publicly permitted by default

- research claims and non-claims;
- architecture and governance specifications;
- threat models and falsifiers;
- proof/evidence registries that do not disclose restricted capability;
- publication/review metadata;
- safe explanatory diagrams and non-turnkey pseudocode.

### Not permitted in this public repository by default

- executable Principal runtime;
- live tool/effect adapters;
- production deployment recipes or infrastructure configuration;
- credential brokers, secret material, API tokens, private keys or production authority material;
- code that materially enables unrestricted autonomous external effects;
- self-directed development/replication machinery intended for live operation;
- private infrastructure topology, customer/company data or operational attack-surface details;
- any artifact classified D1–D4 or above the current C0 public ceiling.

File type is not an exemption. A document, schema, prompt, test, diagram or deployment recipe can be restricted if it materially lowers the effort required to reproduce a restricted capability.

## Runtime rule

A capability-bearing implementation MUST live in a **separate private repository** with independent access control. Public architecture does not imply public runtime source.

No production secret may be committed to either repository. Runtime secrets must be provided through an external least-privilege secret/credential mechanism and remain revocable.

## Reviewer access

Journal reviewers and named researchers may receive a pinned, claim-scoped reviewer package or controlled repository access. Reviewer access SHOULD contain only what is necessary to reproduce the claim and MUST exclude unrelated live credentials, private data and production effect capability.

Read-only repository access does not prevent copying source. Therefore access to restricted source is itself a disclosure decision and must be classified accordingly.

## High-risk disclosure decisions

For C2+/D2+ artifacts, the author/requester cannot be the sole evaluator and promoter of public release. Unknown or disputed classification fails closed to the more restrictive disclosure state until reviewed.

## Security reports

If you identify a secret, live credential, unexpected capability-enabling artifact, disclosure-gate bypass, or a path that could expose restricted runtime material, do not publish exploitation details in a public issue. Contact the repository owner through the verified contact channel listed in the repository metadata and provide the minimum information needed to reproduce the problem safely.

## Claim boundary

This policy does not claim consciousness, sentience, AGI, rebellion, inevitable loss of control, or that the current public R0.1/R0.2 specification is itself an autonomous runtime. It is prospective dual-use and disclosure-risk governance.