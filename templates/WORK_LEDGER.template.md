# WORK LEDGER

This file is a historical index of ASG-governed work.

It is not a substitute for Product Truth, Architecture, Acceptance Contracts, Work Orders, or Reviewer Decisions.

## Current State

- Active work: `<PROJECT-WORK-ID>`
- Current stage: `<M0>`
- Active Work Order: `docs/work-orders/<WO-ID>.md`
- Latest Reviewer Decision: `docs/reviews/<REVIEW-ID>.md`
- Next stage authorized: `false`

## Ledger

| Work Order | Stage | Product Source Commit | Evidence Commit | Reviewer Decision | Result | CI | Notes |
|---|---|---|---|---|---|---|---|
| `<WO-M0-001>` | `<M0>` | `<SHA>` | `<SHA>` | `<REVIEW-M0-001>` | `<ACCEPTED/REPAIR_REQUIRED/BLOCKED>` | `<URL/result>` | `<notes>` |

## Result Vocabulary

Use only:

- `ACTIVE`
- `ACCEPTED`
- `REPAIR_REQUIRED`
- `BLOCKED`
- `SUPERSEDED`
- `NOT_EVALUATED`

Do not erase meaningful historical failures. A repair should normally create a new row / Work Order.

## Traceability Rules

Each row SHOULD be traceable to:

1. Work Order file
2. Product/source commit
3. Evidence/report commit
4. Reviewer Decision file
5. CI run, when applicable

If one of these does not exist, use `N/A` and explain why in Notes.
