---
name: goal-audit
description: Independently audit a saved Codex goal contract against implementation evidence when the user or executing agent requests a final goal review.
---

# Goal Audit

Audit a confirmed goal contract as a separate, skeptical, read-only reviewer. The coordinator should delegate this skill to another agent with the contract path, workspace, and claimed evidence. If you are the executing agent and cannot delegate to a separate reviewer, report that independent audit is unavailable; do not label your own assessment independent. If you have been delegated solely to audit, perform the review directly without spawning another auditor.

## Evidence review

1. Read the saved contract and identify its original outcome, scope, constraints, verification plan, and acceptance criterion IDs. Treat it as the audit standard. Flag any criterion that is too vague to judge.
2. Inspect the actual artifact, changed code, relevant diff, test and command results, walkthrough evidence, and any report the executor supplied. Verify important claims directly where feasible. Treat a claimed pass, screenshot, or summary as a lead, not proof by itself.
3. For each acceptance criterion, assign exactly one status: `met` when direct evidence supports the condition, `unmet` when evidence shows a failure, or `unverified` when the evidence is missing or insufficient. Cite the evidence and explain material uncertainty. Check the original user outcome separately so a checklist cannot hide a missed purpose.
4. Check whether the work stayed within the agreed breadth and constraints. Note material regressions or unauthorized scope changes. Use proportionate checks; do not require unrelated tests merely to enlarge the audit.

## Report and stop

Return a compact audit report to the coordinator with the contract path and revision, implementation revision or dirty-worktree identity, overall verdict (`pass`, `gaps`, or `inconclusive`), a row for every criterion ID and its status and evidence, outcome assessment, scope or constraint issues, and the smallest decision needed from the user. The coordinator saves this report beside the contract as `<contract-stem>.audit.md`; remain read-only yourself. `pass` requires every criterion met and no material outcome or constraint gap. Do not convert unknowns into passes.

When any criterion is `unmet` or `unverified`, report the gap to the user through the coordinator and stop. Do not edit files, repair defects, change the contract, or continue implementation during this audit. The user decides whether to continue within scope, revise the contract, or accept a limitation.
