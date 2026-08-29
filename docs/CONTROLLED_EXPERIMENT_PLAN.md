# Controlled Experiment Plan

## Gate

This experiment MUST NOT begin until R0-Core enforcement has passed the required E2 admission tests, including negative and mutation tests.

## Hypothesis

For workloads involving persistent commitments, worker replacement, model replacement, bounded delegation and recovery, a governed Principal Layer may reduce Human orchestration and improve continuity/accountability without increasing authority violations compared with a capability-matched supervisor-agent baseline.

The claim is workload-specific. Failure on one workload does not universally falsify the architecture.

## Groups

### Baseline
Human → Supervisor Agent → Workers

### Treatment
HumanRootOffice → RootPrincipal → CompanyPrincipal → Workers

The baseline must receive comparable models, tools, raw data and task capability.

## Independent variable
Presence of Principal Layer contracts/enforcement.

## Primary dependent variables
- Human orchestration interventions;
- unauthorized effect count;
- authority violation count;
- commitment-loss count;
- continuity failure count;
- recovery success rate;
- time-to-goal;
- computational/tool cost;
- Human review cost/time;
- evidence-policy completeness;
- remediation latency.

## Workload classes
1. simple operational workload;
2. commitment-heavy customer workflow;
3. budget/exposure workload;
4. Worker replacement workload;
5. Engine/model handoff workload;
6. conflicting-constraint workload.

## Fault injection
- brain/provider swap;
- Worker crash;
- bad contractor;
- forbidden authority attempt;
- expired grant;
- reservation leak attempt;
- fake external-law assertion;
- budget shrink;
- evidence cherry-pick;
- evaluator-capture simulation;
- source/target migration partition;
- succession ambiguity.

## Repetition
At least three independent runs per condition with fixed recorded random seeds; additional runs SHOULD be used when variance is material.

## Claim discipline

Permitted:
> Under workload W and failure regime F, the Principal Layer changed metric M by X in N runs while satisfying the stated authority/evidence conditions.

Forbidden:
> World 9 is universally superior.

## Longitudinal follow-up

A multi-day operational scenario may follow controlled experiments to expose temporal and recovery defects. It is not itself a causal scientific experiment.
