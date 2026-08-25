# Stage Gate Policy

## Rule

A development stage may advance only when all of the following are true:

```text
authorized scope complete
AND required acceptance evidence valid
AND required regressions truthful
AND evidence/source binding valid
AND Reviewer verdict = ACCEPTED
AND Reviewer explicitly authorizes next stage
```

The implementation agent cannot satisfy the final two conditions by itself.

## ACTIVE_WORK

Strict projects SHOULD record:

```yaml
currentStage: <M2>
authorizedStage: <M2>
nextStage: <M3>
nextStageAuthorized: false
```

## Prohibited Stage Behavior

- Stage creep into unauthorized work.
- Implementation agent setting its own stage to ACCEPTED.
- Implementation agent setting `nextStageAuthorized: true` without Reviewer authorization.
- Rewriting acceptance requirements merely because implementation is incomplete.
- Marking deferred future-stage gates PASS using loosely related current-stage assertions.

## Repair

When a stage fails review, create a new repair Work Order. Preserve the historical Work Order and Reviewer Decision for traceability.
