---
reviewId: <REVIEW-M0-001>
workId: <PROJECT-WORK-ID>
stage: <M0>
reviewedSourceCommit: <SHA>
reviewedEvidenceCommit: <SHA-or-null>
verdict: <ACCEPTED|REPAIR_REQUIRED|BLOCKED|SUPERSEDED|NOT_EVALUATED>
nextStageAuthorized: false
reviewedAt: <YYYY-MM-DD>
---

# Reviewer Decision — <Title>

## 1. Scope Reviewed

Reviewed:

- source commit: `<SHA>`
- evidence/report commit: `<SHA-or-null>`
- CI run: `<URL-or-N/A>`
- active Work Order: `docs/work-orders/<WO-ID>.md`
- acceptance contract: `docs/specs/acceptance/<PROJECT-WORK-ID>.json`

## 2. Verdict

**<ACCEPTED|REPAIR_REQUIRED|BLOCKED|SUPERSEDED|NOT_EVALUATED>**

This verdict applies only to stage `<M0>` and the reviewed commits above.

Reviewer Accepted does not mean Product Ready.

## 3. Accepted Portions

- <accepted item 1>
- <accepted item 2>
- <accepted item 3>

## 4. Findings

### BLOCKER-01 — <Title>

**Requirement:**  
<Exact authoritative requirement or reference>

**Evidence:**
- `<file/path>`
- `<symbol/test/trace>`
- `<commit>`

**Finding:**  
<What is wrong>

**Impact:**  
<Why it matters>

**Required correction:**  
<What must change>

**Forbidden workaround:**  
<What must not be done to fake compliance>

## 5. Acceptance-Gate Review

| Gate | Requirement Hash | Status | Evidence | Reviewer Notes |
|---|---|---|---|---|
| `<ID>` | `<hash>` | `<PASS/FAIL/SKIP>` | `<path>` | `<notes>` |

PASS means the exact gate requirement was proven.

## 6. Architecture Review

- Canonical ownership: `<PASS/FAIL/NOT_EVALUATED>`
- Extensibility/additive behavior: `<PASS/FAIL/NOT_EVALUATED>`
- No shadow writable state: `<PASS/FAIL/NOT_EVALUATED>`
- Real product path exercised: `<PASS/FAIL/NOT_EVALUATED>`
- Evidence/source binding: `<PASS/FAIL/NOT_EVALUATED>`

## 7. Safety Review

- paid/external submissions: `<0 or count>`
- production writes: `<0 or count>`
- destructive migrations: `<0 or count>`

## 8. Stage Authorization

Current stage: `<M0>`

Next stage: `<M1>`

Next stage authorized: `false`

If verdict is `ACCEPTED`, authorization still requires an explicit Reviewer control-plane decision.

## 9. Required Next Work

If repair is required, create a NEW Work Order. Do not silently rewrite historical Work Orders.

## 10. Reviewer Summary

<Concise decision rationale based on requirements, source, tests, and evidence. Do not include private chain-of-thought.>
