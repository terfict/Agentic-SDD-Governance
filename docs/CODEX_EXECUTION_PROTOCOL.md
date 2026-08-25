# Codex / Implementation-Agent Execution Protocol

## Canonical Startup Command

English:

> Sync the latest branch. Read `docs/specs/ACTIVE_WORK.md`. Execute the referenced active Work Order exactly. Stop at its defined stop condition.

中文：

> 同步最新分支。讀取 `docs/specs/ACTIVE_WORK.md`。嚴格依照其中引用的目前有效 Work Order 執行工作，並在該 Work Order 所定義的停止條件達成後立即停止。

## Fixed Protocol

1. Sync the latest repository state.
2. Read `ACTIVE_WORK.md`.
3. Read the referenced active Work Order.
4. Read the latest Reviewer Decision.
5. Read referenced authoritative specifications.
6. Validate stage authorization and scope.
7. Execute only authorized scope.
8. Commit source changes.
9. Run required tests/browser verification.
10. Commit evidence/reports separately when practical.
11. Push.
12. Wait for required CI.
13. Stop at the Work Order stop condition.
14. Return the Reviewer package.

## Hard Rules

- Do not self-accept.
- Do not self-authorize the next stage.
- Do not rewrite acceptance requirements to accommodate implementation.
- Do not broaden scope merely because a broader change seems convenient.
- Do not treat CI Green as Product Ready.
- Do not fabricate evidence.
- Do not treat historical success as certification of current source.
- Do not perform unapproved external or paid actions.
- If scope or authority conflicts are found, STOP and report the conflict.
