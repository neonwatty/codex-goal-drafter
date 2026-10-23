# Codex Goal Contracts

A small plugin for defining what a Codex `/goal` must accomplish and checking the final result against evidence. Native `/goal` remains the execution engine.

## Workflow

1. Invoke `$goal-contract` with the outcome you want. It interviews you about breadth, acceptance criteria, QA, verification, deliverables, and stop conditions. It supports feature, UX, QA, test repair, experiment, research, and artifact goals.
2. Review the concise contract. The skill waits for explicit confirmation, then saves it in the project repository (normally `docs/goal-contracts/<slug>.md`) and gives you a ready-to-paste `/goal` command.
3. Run that command. The executor maps evidence to each criterion. Before declaring a blocker, it checks the exact failure and a safe authorized correction within the contract's limits.
4. The executor delegates a final read-only check to a separate agent using `$goal-audit`. The coordinator saves the auditor's report beside the contract as `<contract-stem>.audit.md`, including each criterion's `met`, `unmet`, or `unverified` status. Gaps come back to you before more implementation work; completion requires the saved passing receipt.

The plugin has two skills and no MCP server or lifecycle hook. It requires a local executor because it works with project files and verification commands. The audit is an explicit step in the generated goal instruction. The plugin cannot itself prove a product outcome or intercept every native `/goal` status change.

In the Seatify live-model trial, the interview fixed the local synthetic scope and a 10-attempt limit. An initial credential pull failed because of a CLI overwrite option; a corrected authorized pull cleared that apparent blocker. The independent audit passed, but its verdict lived only in the session. Those observations motivated the blocker check and saved audit receipt above.

## Local installation

From a local clone, register its marketplace and install the plugin:

```sh
codex plugin marketplace add /absolute/path/to/codex-goal-drafter
codex plugin add codex-goal-drafter@codex-goal-drafter-local
```

Restart Codex to load the new skills. The original personal `$codex-goal-drafter` skill remains as a compatibility entry point to `$goal-contract` in the repository.

## Files

- `skills/goal-contract/`: interview, confirmed contract, and native `/goal` handoff.
- `skills/goal-audit/`: independent, skeptical, read-only final review.
- `plugin.json`: portable plugin manifest.
- `.agents/plugins/marketplace.json`: local marketplace entry for installation and testing.
