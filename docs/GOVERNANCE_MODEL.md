# ASG Governance Model

ASG separates durable project truth, current execution authority, implementation, evidence, and independent acceptance.

## Layers

1. **Product Truth** — what the product is and is not.
2. **Architecture** — durable system boundaries and ownership.
3. **Acceptance Contract** — exact requirements that must be proven.
4. **ACTIVE_WORK** — the single currently authorized stage and pointers.
5. **Active Work Order** — bounded implementation instructions.
6. **Implementation** — source changes made by the implementation agent.
7. **Evidence** — tests, browser journeys, traces, hashes, and CI.
8. **Reviewer Decision** — independent ACCEPTED / REPAIR_REQUIRED / BLOCKED / SUPERSEDED / NOT_EVALUATED verdict.
9. **Stage Authorization** — explicit permission to move forward.

## Authority Precedence

Product Truth → Architecture → UI/UX Spec → Acceptance Contract → ACTIVE_WORK → Work Order → Reviewer Decision → Implementation → Reports → Historical behavior.

If higher-authority sources conflict, stop and resolve the conflict rather than silently choosing an implementation-friendly interpretation.

## Strict Profile Invariants

- Exactly one active Work Order.
- Exactly one authorized stage.
- Implementation agents cannot self-accept.
- Implementation agents cannot self-authorize the next stage.
- Acceptance PASS must bind to the exact authoritative requirement.
- Evidence must bind to committed source.
- User-facing behavior requires real browser evidence where practical.
- New functionality should be primarily additive and extension-driven.
- External/paid side effects require explicit authorization.
