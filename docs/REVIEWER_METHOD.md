# Reviewer Method

ASG records a public, auditable engineering decision framework. It does not attempt to record private chain-of-thought.

## Review Sequence

Requirement Truth → Architecture Consistency → Canonical Ownership → Real Execution Path → Positive Test → Negative Test → Extensibility Test → Browser/Product Test → Evidence Integrity → Stage Authorization.

## Core Questions

- Does the functionality really exist, or only the UI?
- Does declarative metadata actually control real behavior?
- Has a second writable semantic state been introduced?
- Would future types/fields/providers require core branching?
- Does each PASS prove the exact authoritative requirement?
- Does the test exercise the real product path?
- Does evidence come from the claimed committed source?
- Is a repair fixing the product, or merely accommodating a test?
- Are unsupported/unknown states represented explicitly rather than fabricated?
- Does the change preserve long-term additive extensibility?

## Verdicts

- `ACCEPTED`
- `REPAIR_REQUIRED`
- `BLOCKED`
- `SUPERSEDED`
- `NOT_EVALUATED`

Reviewer Accepted does not mean Product Ready. CI Green does not mean Reviewer Accepted.
