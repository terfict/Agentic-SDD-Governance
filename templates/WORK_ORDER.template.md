---
workOrderId: <WO-M0-001>
workId: <PROJECT-WORK-ID>
stage: <M0>
status: ACTIVE
createdFromReviewerDecision: <REVIEW-ID-or-BOOTSTRAP>
supersedes: null
authorizedNextStage: false
paidProviderAllowed: false
productionWriteAllowed: false
destructiveMigrationAllowed: false
---

# <Work Order Title>

## 1. Objective

<Exactly what this Work Order must accomplish.>

## 2. Why This Work Exists

<Problem / reviewer finding / architectural need that caused this Work Order.>

## 3. Authoritative Inputs

Read in this order:

1. `docs/specs/ACTIVE_WORK.md`
2. `docs/specs/product/PRODUCT_TRUTH.md`
3. `docs/specs/architecture/ARCHITECTURE.md`
4. `docs/specs/ui/UI_MASTER_SPEC.md` (if applicable)
5. `docs/specs/acceptance/<PROJECT-WORK-ID>.json`
6. `docs/reviews/<REVIEW-ID>.md`

If this Work Order conflicts with a higher-authority source, STOP and report the conflict.

## 4. Authorized Scope

The agent MAY:

- <allowed item 1>
- <allowed item 2>
- <allowed item 3>

## 5. Forbidden Scope

The agent MUST NOT:

- start `<NEXT_STAGE>`;
- change Product Truth merely to make tests pass;
- weaken Acceptance requirements;
- create a second writable semantic state;
- perform unapproved paid/external actions;
- broaden scope without Reviewer authorization.

## 6. Architecture Invariants

- <invariant 1>
- <invariant 2>
- <invariant 3>
- New functionality should be primarily additive.
- Declarative metadata must control real behavior, not exist as inert configuration.

## 7. Required Changes

### 7.1 <Area>

- <required change>
- <required change>

### 7.2 <Area>

- <required change>

## 8. Acceptance Criteria

Every PASS must bind to the exact authoritative Acceptance Contract requirement.

Required stage-local checks:

- `<M0-CHECK-01>` — <description>
- `<M0-CHECK-02>` — <description>

Acceptance gates intended to be evaluated in this Work Order:

- `<GATE-ID>` — <exact requirement or reference>
- `<GATE-ID>` — <exact requirement or reference>

Do not mark unrelated/deferred gates PASS.

## 9. Negative Tests

At minimum prove:

- <invalid condition> → rejected/filtered/blocked
- <unsupported condition> → explicit unsupported state
- <scope boundary> → no unauthorized behavior

## 10. Browser Journeys

Required only for user-facing behavior.

### JOURNEY-01 — <name>

1. Launch real application.
2. <interaction>
3. <interaction>
4. Assert DOM state.
5. Assert canonical/application state.
6. Capture meaningful screenshot.
7. Fail on unexpected application console errors.

Screenshot existence alone is not PASS.

## 11. Regression Requirements

Run all Work Order-required free regressions and truthfully record PASS / FAIL / SKIP. Do not convert a known blocker into fake PASS.

## 12. Evidence Requirements

Record at minimum:

- product/source commit SHA;
- executed source commit SHA;
- evidence/report commit SHA;
- test source hashes;
- relevant implementation source hashes;
- browser test hash;
- screenshots/traces when applicable;
- console errors;
- CI run URL and conclusion;
- external/paid side-effect count.

Acceptance evidence SHOULD include `gateId`, authoritative `requirement`, deterministic `requirementHash`, `status`, assertions, and evidence.

## 13. External Side-effect Policy

Default:

```text
paidProviderAllowed=false
productionWriteAllowed=false
destructiveMigrationAllowed=false
```

Do not infer authorization from credentials.

## 14. Commit Strategy

Recommended:

1. Source/product commit
2. Test/evidence/report commit

Keep source and evidence traceable.

## 15. Stop Condition

When all Work Order tasks are complete:

1. commit source;
2. run required tests/browser journeys;
3. commit evidence/reports;
4. push;
5. wait for required CI;
6. STOP.

Do NOT start the next stage, update Reviewer verdict to ACCEPTED, or self-authorize anything beyond this Work Order.

## 16. Reviewer Return Contract

Return source commit SHA, evidence/report commit SHA, exact changed files, tests run, browser journeys/assertion count, screenshots/traces, console errors, known blockers, deferred next-stage items, CI URL/conclusion, external/paid side-effect count, and spec synchronization performed.
