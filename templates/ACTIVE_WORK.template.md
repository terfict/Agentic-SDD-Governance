# ACTIVE WORK

workId: <PROJECT-WORK-ID>
status: ACTIVE
priority: <P0|P1|P2>
baseline: <BASELINE_COMMIT_SHA>
acceptance: docs/specs/acceptance/<PROJECT-WORK-ID>.json
currentStage: <M0>
authorizedStage: <M0>
activeWorkOrder: docs/work-orders/<WO-ID>.md
latestReviewerDecision: docs/reviews/<REVIEW-ID>.md
nextStage: <M1-or-null>
nextStageAuthorized: false

## Title

<Current active work title>

## Authoritative documents

Implementation agent MUST read and follow, in this order:

1. `docs/specs/product/PRODUCT_TRUTH.md`
2. `docs/specs/architecture/ARCHITECTURE.md`
3. `docs/specs/ui/UI_MASTER_SPEC.md` (when applicable)
4. `docs/specs/acceptance/<PROJECT-WORK-ID>.json`
5. `docs/work-orders/<WO-ID>.md`
6. `docs/reviews/<REVIEW-ID>.md`

If these sources conflict, STOP and report the conflict. Do not silently choose an interpretation.

## Current authorization

- Authorized stage: `<M0>`
- Next stage: `<M1>`
- Next stage authorized: `false`
- Paid/external side effects authorized: `false` unless active Work Order explicitly says otherwise.

## Project objective

<One concise paragraph describing the current project-level objective.>

## Hard invariants

- One canonical writable semantic state where applicable.
- Specification determines implementation.
- Agent may not self-accept.
- Agent may not self-authorize the next stage.
- Gate PASS must prove the exact authoritative requirement.
- Evidence must bind to committed source.
- Historical behavior does not override current authoritative specs.
- No unapproved paid/external side effects.

## Current stage checkpoint

### <M0> — <Stage title>

Status: `<ACTIVE|REVIEWER ACCEPTED|REPAIR_REQUIRED|BLOCKED>`

Reviewed source commit: `<SHA-or-N/A>`

Evidence/report commit: `<SHA-or-N/A>`

Reviewer decision: `docs/reviews/<REVIEW-ID>.md`

## Stop rule

The implementation agent MUST stop at the active Work Order stop condition.

It MUST NOT advance `currentStage`, set `nextStageAuthorized: true`, begin the next stage, or mark Reviewer acceptance unless a later Reviewer-authorized Work Order explicitly requires the transition.
