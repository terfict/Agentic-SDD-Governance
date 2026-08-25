# Agentic SDD Governance — ASG

**中文名稱：AI Agent 規格驅動開發治理框架**  
**Version:** 1.0.0  
**Status:** Canonical  
**Abbreviation:** ASG

## 1. Purpose

ASG is a project-agnostic governance framework for specification-driven software development performed with AI coding agents such as Codex.

ASG exists to prevent common agentic-development failure modes:

- implementation before product truth is stable;
- architecture invented ad hoc during coding;
- multiple writable semantic states;
- agents self-declaring completion;
- agents self-authorizing the next stage;
- tests passing without proving the actual requirement;
- screenshots being treated as functional evidence;
- reports being detached from the committed source they claim to verify;
- historical behavior overriding current authoritative specifications;
- extensibility being claimed without additive extension tests;
- CI green being misrepresented as product readiness;
- external or paid side effects occurring without explicit authorization.

ASG governs the flow:

**Product Truth → Architecture → Acceptance Contract → ACTIVE_WORK → Work Order → Implementation → Evidence → Reviewer Decision → Next-stage Authorization**

## 2. Core Principle

> Specification determines implementation. Implementation does not redefine the specification merely to become test-green.

```text
Product Truth
    ↓
Architecture
    ↓
Acceptance Contract
    ↓
ACTIVE_WORK
    ↓
Active Work Order
    ↓
Agent Implementation
    ↓
Committed Source
    ↓
Tests / Browser / CI
    ↓
Evidence
    ↓
Reviewer Decision
    ├─ REPAIR_REQUIRED → New Work Order
    └─ ACCEPTED → Next Stage May Be Authorized
```

No agent may skip this sequence unless the active governance profile explicitly permits a lighter process.

## 3. Governance Profiles

### 3.1 Lite

Use for small scripts, isolated bug fixes, one-file utilities, and low-risk changes.

Minimum:
- Work Order;
- tests;
- source commit;
- concise review result.

### 3.2 Standard

Use for normal production features, multi-file changes, persistent applications, and projects with CI.

Minimum:
- Product/feature specification;
- Work Order;
- Acceptance Criteria;
- tests;
- Reviewer Decision;
- CI evidence.

### 3.3 Strict

Use for long-lived platforms, extensible systems, multi-stage development, AI-heavy systems, provider integrations, systems with costly or external side effects, and projects where architecture/evidence integrity are critical.

Minimum:
- Product Truth;
- Architecture;
- UI/UX specification when applicable;
- Acceptance Contract;
- ACTIVE_WORK;
- Work Orders;
- Reviewer Decisions;
- ADRs;
- Work Ledger;
- real browser evidence for user-facing behavior;
- source/evidence/report binding;
- Control Plane validation;
- explicit next-stage authorization.

When uncertain, use Standard. Use Strict when architectural drift would be expensive.

## 4. Project Repository Contract

A Strict ASG repository SHOULD use:

```text
docs/
├─ specs/
│  ├─ ACTIVE_WORK.md
│  ├─ MASTER_SPEC_INDEX.md
│  ├─ product/
│  ├─ architecture/
│  ├─ ui/
│  └─ acceptance/
├─ work-orders/
├─ reviews/
├─ decisions/
└─ governance/
   ├─ REVIEWER_METHOD.md
   ├─ CODEX_EXECUTION_PROTOCOL.md
   ├─ EVIDENCE_POLICY.md
   └─ WORK_LEDGER.md
```

Project-specific truth MUST remain in the project repository.

The Skill defines the governance method.  
The project repository defines the current project state.

## 5. Authority Precedence

Unless a project explicitly declares a stricter precedence order, use:

1. Product Truth
2. Architecture
3. UI/UX Master Specification
4. Acceptance Contract
5. ACTIVE_WORK
6. Active Work Order
7. Latest Reviewer Decision
8. Implementation
9. Reports / generated evidence
10. Historical behavior

Rules:

- A Work Order cannot override Product Truth or Architecture.
- Tests cannot redefine Acceptance requirements.
- Historical implementation is not authoritative when superseded.
- If authoritative sources conflict, STOP and report the conflict.
- Do not silently choose the easier interpretation.

## 6. ACTIVE_WORK Contract

A project using ASG Strict MUST have exactly one active work descriptor.

Recommended stable metadata:

```yaml
workId: <project-work-id>
status: ACTIVE
currentStage: <stage>
authorizedStage: <stage>
activeWorkOrder: docs/work-orders/<active-work-order>.md
latestReviewerDecision: docs/reviews/<latest-review>.md
nextStage: <stage-or-null>
nextStageAuthorized: false
```

Invariant:

> Exactly one stage is currently authorized.

The implementation agent MUST NOT modify `currentStage` or set `nextStageAuthorized: true` unless a Reviewer-authorized Work Order explicitly instructs it to update the control plane.

## 7. Work Order Contract

A Work Order is the normal execution instruction for an implementation agent.

Recommended front matter:

```yaml
---
workOrderId: WO-M2-002
workId: PROJECT-WORK-ID
stage: M2
status: ACTIVE
createdFromReviewerDecision: REVIEW-M2-001
authorizedNextStage: false
paidProviderAllowed: false
productionWriteAllowed: false
destructiveMigrationAllowed: false
---
```

A Work Order SHOULD contain:

1. Objective
2. Why This Work Exists
3. Authoritative Inputs
4. Authorized Scope
5. Forbidden Scope
6. Architecture Invariants
7. Required Changes
8. Acceptance Criteria
9. Negative Tests
10. Browser Journeys, if applicable
11. Regression Requirements
12. Evidence Requirements
13. External Side-effect Policy
14. Commit Strategy
15. Stop Condition
16. Reviewer Return Contract

Historical Work Orders SHOULD be immutable. A repair SHOULD create a new Work Order rather than silently rewriting the old instruction.

## 8. Reviewer Decision Contract

Reviewer verdicts:

- `ACCEPTED`
- `REPAIR_REQUIRED`
- `BLOCKED`
- `SUPERSEDED`
- `NOT_EVALUATED`

A Reviewer Decision SHOULD record:

```yaml
workId: <id>
stage: <stage>
reviewedSourceCommit: <sha>
reviewedEvidenceCommit: <sha-or-null>
verdict: REPAIR_REQUIRED
nextStageAuthorized: false
```

It MUST distinguish accepted portions, blockers, evidence, impact, required correction, forbidden workaround, and stage authorization.

Definitions:

**Reviewer Accepted** does not mean **Product Ready**.  
**CI Green** does not mean **Reviewer Accepted**.  
**A passing test** does not mean **the requirement was proven**.

## 9. Reviewer Method

ASG records an auditable decision framework, not private chain-of-thought.

```text
Requirement Truth
    ↓
Architecture Consistency
    ↓
Canonical Ownership
    ↓
Real Execution Path
    ↓
Positive Test
    ↓
Negative Test
    ↓
Extensibility Test
    ↓
Browser/Product Test
    ↓
Evidence Integrity
    ↓
Stage Authorization
```

Reviewer questions:

A. Does the functionality really exist, or only the UI?  
B. Does declarative metadata actually control parse/UI/validation/compile behavior?  
C. Has a second writable semantic state been introduced?  
D. Would adding the 50th type/field/provider require editing core branching logic?  
E. When something is inapplicable, is it truly not shown, parsed, validated, or compiled?  
F. When a source is removed, is dependent state actually invalidated rather than merely hidden?  
G. Does each PASS prove the exact authoritative requirement?  
H. Does the test travel through the real product path?  
I. Does the evidence come from the committed source it claims to verify?  
J. Is the repair fixing the product, or only making the test green?  
K. Is the current known operation/type/model universe hard-coded?  
L. Does switching UI views avoid semantic mutation and revision changes?  
M. Are provider-native, heuristic, inferred, and experimental facts distinguished?  
N. Are unsupported states represented explicitly instead of fabricated?  
O. Does the change preserve long-term additive extensibility?

## 10. Canonical State Rule

For systems with multiple authoring methods or UI modes:

> Different entry methods may exist; writable semantic truth must remain singular.

```text
Prompt-first
Structured-first
Timeline-first
Preset-first
Mixed
      ↓
ONE canonical semantic state
```

Forbidden without explicit architectural approval:

- a second semantic database for Structured UI;
- a timeline store that independently owns the same meaning;
- writable Legacy/Compatibility projections;
- view switching that reparses or rebuilds semantics solely because the view changed.

UI-local ephemeral state is allowed for selected tab, collapsed panel, focus, transient validation presentation, and non-semantic display preferences.

## 11. Extensibility Rule

Default architectural principle:

> New functionality should be primarily additive.

Prefer:

- declarative registry entry;
- extension module;
- adapter;
- driver;
- capability metadata;
- prompt grammar registration;
- migration/alias metadata.

Avoid scattered core branching such as:

```js
if (type === "action-combat") { ... }
```

unless the behavior is genuinely part of Universal Core.

Extensibility acceptance SHOULD use a fictional future extension unknown to historical core code.

```text
Register new type
+ new fields
+ new operation
+ optional trait gate

Verify:
Registry
→ UI
→ Parse
→ Validation
→ Compile
→ Output filtering

without modifying core type-specific branches.
```

## 12. Acceptance Evidence Policy

Every acceptance gate PASS MUST bind to the exact authoritative requirement.

Recommended evidence record:

```json
{
  "gateId": "GATE-04",
  "requirement": "<loaded from authoritative acceptance contract>",
  "requirementHash": "<sha256(normalized requirement)>",
  "status": "PASS",
  "assertions": [],
  "evidence": {}
}
```

Evidence tooling SHOULD reject:

- unknown gate IDs;
- duplicate contradictory results;
- requirement-hash mismatch;
- PASS against a different requirement;
- reports generated from uncommitted or mismatched source;
- browser screenshots with no functional assertion;
- source SHA mismatch;
- stale test hashes.

Supporting test checks SHOULD use stage-local IDs instead of pretending every assertion is an acceptance gate.

## 13. Test Policy

Tests SHOULD be layered:

1. Static contract
2. Unit
3. Integration
4. Product-path compile/execution
5. Browser/E2E
6. Regression
7. Extensibility
8. Negative-path
9. Evidence integrity
10. CI

Rules:

- Helper-level PASS does not certify the product path.
- Positive tests alone are insufficient for routing, applicability, invalidation, authorization, or extensibility.
- User-facing behavior requires real browser operation where practical.
- Screenshot existence alone is not acceptance evidence.
- Unexpected console errors fail the relevant browser journey.
- A synthetic benchmark must actually exercise the behavior it claims to certify.

## 14. Report Integrity

Reports SHOULD record:

```text
productSourceCommitSha
executedSourceCommitSha
evidenceCommitSha
ciCommitSha
branch
generatedAt
testSourceHashes
relevantSourceHashes
browserTestHash
evidencePaths
CI run
paidProviderSubmissions
```

Do not overwrite historical traceability merely to show the latest SHA.

## 15. External Side-effect Safety

External effects require explicit authorization.

Examples:
- paid AI provider request;
- production deployment;
- destructive database migration;
- email/message send;
- irreversible cloud operation;
- paid benchmark.

Default:

```text
paidProviderAllowed: false
productionWriteAllowed: false
destructiveMigrationAllowed: false
```

An implementation agent MUST NOT infer authorization from the existence of credentials.

## 16. Implementation-Agent Execution Protocol

Canonical startup instruction:

> Sync the latest branch. Read `docs/specs/ACTIVE_WORK.md`. Execute the referenced active Work Order exactly. Stop at its defined stop condition.

中文：

> 同步最新分支。讀取 `docs/specs/ACTIVE_WORK.md`。嚴格依照其中引用的目前有效 Work Order 執行工作，並在該 Work Order 所定義的停止條件達成後立即停止。

Execution sequence:

1. Sync repository.
2. Read ACTIVE_WORK.
3. Read active Work Order.
4. Read latest Reviewer Decision.
5. Read referenced authoritative specifications.
6. Validate current-stage authorization.
7. Execute only authorized scope.
8. Commit source changes.
9. Run required tests/browser journeys.
10. Commit evidence/reports separately when practical.
11. Push.
12. Wait for required CI.
13. Stop at Work Order stop condition.
14. Return the Reviewer package.

The implementation agent MUST NOT self-accept, self-authorize the next stage, change requirements merely to match implementation, broaden scope for convenience, claim Product Ready from unit tests, fabricate evidence, treat historical success as certification of current source, or perform unapproved external/paid actions.

If scope conflict is discovered:

> STOP and report the conflict.

## 17. Reviewer Return Package

A completed Work Order SHOULD return:

1. Product/source commit SHA
2. Evidence/report commit SHA
3. Exact changed files
4. Exact tests executed
5. Browser journeys and assertion count
6. Screenshots / traces
7. Console errors
8. Known blockers
9. Deferred next-stage items
10. CI run URL and conclusion
11. External side-effect count
12. Any spec synchronization performed

The Reviewer then independently decides `ACCEPTED`, `REPAIR_REQUIRED`, `BLOCKED`, `SUPERSEDED`, or `NOT_EVALUATED`.

## 18. Stage Progression Rule

A stage progresses only when all are true:

```text
authorized scope complete
AND required acceptance evidence valid
AND required regressions truthful
AND evidence/source binding valid
AND Reviewer verdict = ACCEPTED
AND Reviewer explicitly authorizes next stage
```

The implementation agent cannot satisfy the final two conditions by itself.

## 19. Work Ledger

A project SHOULD maintain `docs/governance/WORK_LEDGER.md`.

Recommended columns:

```text
Work Order
Stage
Product Source Commit
Evidence Commit
Reviewer Decision
Result
CI
Notes
```

The Work Ledger is an index, not the authoritative source of detailed requirements.

## 20. ADR Policy

Use Architecture Decision Records for decisions expected to survive individual Work Orders.

Examples:

- Extensibility First
- One Canonical Writable State
- Provider/Model Separation
- Work Order / Reviewer Governance
- Evidence-bound Acceptance
- No Paid Provider Tests by Default

A Work Order is temporary execution authority. An ADR records a durable architectural decision.

## 21. Governance Anti-Patterns

Reject:

- **Test-driven specification drift** — weakening specification because a test fails.
- **Gate-name laundering** — attaching a gate ID to an unrelated assertion.
- **Screenshot acceptance** — treating screenshot existence as functionality.
- **Shadow-state implementation** — giving a new UI its own semantic database.
- **Stage creep** — quietly implementing later-stage behavior.
- **Self-certification** — an agent declaring Reviewer acceptance.
- **Historical-success reuse** — old success certifying new source.
- **Hard-coded extensibility** — registry exists but core still branches by type.
- **Evidence detached from source** — report SHA does not match executed tree.
- **Safety-by-convention** — risky side effects prevented only by memory.

## 22. Bootstrap Procedure for a New Project

For a new Standard/Strict project:

1. Define Product Truth.
2. Define architecture boundaries.
3. Define acceptance contract.
4. Choose governance profile.
5. Create ACTIVE_WORK.
6. Create initial Work Order.
7. Create Reviewer Method reference.
8. Create Work Ledger.
9. Add Control Plane checks.
10. Only then authorize implementation.

Suggested initial files:

```text
docs/specs/PRODUCT_TRUTH.md
docs/specs/ARCHITECTURE.md
docs/specs/ACTIVE_WORK.md
docs/specs/acceptance/<WORK-ID>.json
docs/work-orders/WO-M0-001.md
docs/reviews/
docs/decisions/
docs/governance/REVIEWER_METHOD.md
docs/governance/CODEX_EXECUTION_PROTOCOL.md
docs/governance/WORK_LEDGER.md
```

## 23. Skill Trigger Guidance

Use ASG when the user asks to:

- start or continue a serious software project;
- hand work to Codex or another implementation agent;
- create product/architecture/specification documents;
- review committed code against requirements;
- structure multi-stage development;
- establish acceptance criteria;
- prevent agents from changing scope;
- create evidence-driven CI/review governance;
- make a project long-term extensible;
- recover a project that has become ad hoc.

Do not force Strict ASG onto trivial one-off tasks.

## 24. Skill Behavior

When ASG is active:

1. Identify the project's current authoritative truth.
2. Identify current stage and authorization.
3. Prefer repository-resident instructions over transient chat instructions.
4. Convert substantial implementation requests into a Work Order.
5. Preserve architecture invariants.
6. Require evidence proportional to user-visible or architectural risk.
7. Review exact source, not only agent summaries.
8. Separate implementation completion from Reviewer acceptance.
9. Record durable decisions in ADRs.
10. Keep next-stage authorization explicit.
11. Prefer additive extensibility.
12. Preserve a truthful historical ledger.
13. Refuse to mark a requirement PASS without requirement-matched evidence.
14. Do not expose private chain-of-thought; record only auditable decision rationale, findings, evidence, and conclusions.

## 25. Versioning

ASG uses Semantic Versioning.

### v1.0.0

Initial canonical framework extracted from production use of specification-driven staged development, ACTIVE_WORK control plane, Work Orders, independent Reviewer decisions, evidence/source binding, browser evidence, extensibility benchmarks, explicit next-stage authorization, and external-side-effect safety.

Future versions SHOULD remain backward compatible where reasonable and SHOULD document governance-breaking changes explicitly.

## 26. Canonical Summary

> **ASG makes the repository self-describing enough that a new AI agent session can safely continue the project without relying on chat memory.**

The Skill supplies the method.  
The project repository supplies the truth.  
The Work Order supplies current authority.  
The implementation agent supplies code.  
Evidence supplies proof.  
The Reviewer supplies acceptance.  
Only explicit authorization advances the stage.
