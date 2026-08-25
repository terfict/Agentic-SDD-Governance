# Evidence Policy

## Principle

A PASS is valid only when evidence proves the exact authoritative requirement against the committed source it claims to verify.

## Requirement Binding

Acceptance evidence SHOULD include:

```json
{
  "gateId": "GATE-01",
  "requirement": "<loaded from authoritative contract>",
  "requirementHash": "<sha256(normalized requirement)>",
  "status": "PASS",
  "assertions": [],
  "evidence": {}
}
```

Evidence tooling SHOULD reject unknown gate IDs, duplicate contradictory results, requirement-hash mismatch, PASS against a different requirement, source SHA mismatch, stale test hashes, and screenshot-only proof without functional assertions.

## Source Binding

Reports SHOULD distinguish:

- `productSourceCommitSha`
- `executedSourceCommitSha`
- `evidenceCommitSha`
- `ciCommitSha`

## Browser Evidence

For user-facing behavior, prefer real application journeys in a real browser. Capture DOM assertions, application/canonical state assertions, unexpected console errors, meaningful screenshots, and trace/log evidence where useful.

Screenshot existence alone is not PASS.

## Truthful Status

Use PASS only when fully proven. Otherwise use FAIL, SKIP, NOT_EVALUATED, or the project's declared equivalent. Do not attach an acceptance-gate ID to a merely related supporting assertion.
