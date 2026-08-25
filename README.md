# Agentic SDD Governance — ASG

**中文名稱：AI Agent 規格驅動開發治理框架**  
**Canonical version:** `1.0.0`

ASG is a project-agnostic governance framework for specification-driven software development performed with AI coding agents such as Codex.

Its purpose is to make serious AI-assisted software projects self-describing, stage-controlled, evidence-driven, extensible, and independently reviewable.

## Core Flow

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
    └─ ACCEPTED → Explicit next-stage authorization
```

## Package Contents

- `SKILL.md` — canonical ASG governance skill
- `templates/ACTIVE_WORK.template.md`
- `templates/WORK_ORDER.template.md`
- `templates/REVIEW_DECISION.template.md`
- `templates/ADR.template.md`
- `templates/WORK_LEDGER.template.md`
- `templates/ACCEPTANCE_CONTRACT.template.json`
- `docs/GOVERNANCE_MODEL.md`
- `docs/REVIEWER_METHOD.md`
- `docs/EVIDENCE_POLICY.md`
- `docs/STAGE_GATE_POLICY.md`
- `docs/CODEX_EXECUTION_PROTOCOL.md`
- `VERSION`
- `CHANGELOG.md`

## Governance Profiles

- **Lite** — small scripts and isolated low-risk fixes
- **Standard** — normal production features and persistent applications
- **Strict** — long-lived, extensible, multi-stage, AI/provider-integrated systems

## Canonical Agent Startup Command

English:

> Sync the latest branch. Read `docs/specs/ACTIVE_WORK.md`. Execute the referenced active Work Order exactly. Stop at its defined stop condition.

中文：

> 同步最新分支。讀取 `docs/specs/ACTIVE_WORK.md`。嚴格依照其中引用的目前有效 Work Order 執行工作，並在該 Work Order 所定義的停止條件達成後立即停止。

## Core Rule

The Skill supplies the governance method.  
The project repository supplies current truth and authority.  
The Work Order supplies bounded execution authority.  
The implementation agent supplies code.  
Evidence supplies proof.  
The Reviewer supplies acceptance.  
Only explicit authorization advances the stage.

## First Strict Adopter

Unified Media Studio (`terfict/Unified-Media-Studio`) is the first repository adopting ASG Strict governance.

## Versioning

ASG uses Semantic Versioning. The repository content identifying `1.0.0` is the canonical v1.0.0 source. A Git tag/release named `v1.0.0` should point to the corresponding canonical release commit.
