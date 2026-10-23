---
name: goal-contract
description: Interview the user and prepare an evidence-based Codex /goal contract when they explicitly ask to draft, refine, or prepare a goal.
---

# Goal Contract

## Invocation boundary

Use for an explicit request to draft, critique, or prepare a goal. An ordinary request to implement, fix, investigate, or audit something should proceed directly; having multiple steps does not turn it into goal preparation.

## Purpose

Turn the user's intended outcome into a goal they understand and can judge before Codex starts. Preparation is an interview and a reviewable contract, not an implementation turn. Do not activate `/goal` or perform the requested product work while preparing it.

## Interview

1. Identify the kind of work: feature development, UX, QA or bug discovery, test repair, experiment or research, creation, or a combination. Use [goal-patterns.md](references/goal-patterns.md) for the relevant mode only.
2. Start from the concrete user outcome. Ask what success would look like to the person using or reviewing the result. Expand scope only where needed to make that outcome real. Make included areas, excluded areas, and the intended breadth explicit.
3. Ask targeted follow-ups until the user can judge what "done" means. Do not impose a fixed question count. Prefer one material decision at a time; offer plausible choices and tradeoffs when they help the user discover a preference. Reflect each answer and probe its unresolved consequence. Do not repeatedly ask for facts the user already supplied.
4. Establish observable acceptance criteria, the evidence that will prove each one, expected deliverables, constraints, and a stop or blocked condition. Ask whether the work includes investigation, implementation, or both when that affects scope. For experiments and research, have the user choose the intended finish: decision, measured result, prototype, report, or another outcome.
5. For feature, UX, and creation goals, include a relevant browser or manual walkthrough and relevant tests by default. Choose checks proportional to the work; if a check is unavailable or unsuitable, record the gap and a credible alternative. Do not invent command names or treat passing tests alone as proof of a user-visible outcome.

Read project files or run read-only discovery when a named repository or artifact would help make questions concrete. Separate observed facts from proposed criteria. Do not turn guesses into requirements. If the user cannot yet choose a material outcome, help them define a bounded discovery goal rather than fabricate a finish line.

## Contract and goal

Before producing the final `/goal`, show a concise contract covering outcome, breadth and exclusions, acceptance criteria, verification and QA, deliverables, constraints, and stop conditions. Flag decisions that remain open. Ask the user to confirm or correct this contract, and wait for an explicit confirmation. A request to prepare a goal is not confirmation of a contract the user has not seen.

After confirmation, save the contract as a small Markdown file in the project repository. Follow an existing project convention; otherwise use `docs/goal-contracts/<slug>.md`. Give each acceptance criterion a stable ID and name the evidence that would establish it. Include an audit rule: a separate read-only skeptical reviewer checks each criterion against evidence; unmet or unverified criteria are reported to the user for review before further work. Keep the file human-readable and limited to the contract, not a task board. If no project repository is available, ask for its location before claiming the contract is saved. Do not write the contract into a GoalBuddy board directory unless that board's schema permits it.

Produce a ready-to-paste `/goal` that points to the saved contract and preserves its decisions. Require the executor to leave an evidence map and delegate a final read-only review to a separate agent using the packaged `goal-audit` skill before claiming completion. The coordinator, not the read-only auditor, saves the auditor's report beside the contract as `<contract-stem>.audit.md`, preserving its criterion statuses, evidence, verdict, contract revision, and implementation revision or dirty-worktree identity. Do not claim completion until that receipt exists. If a separate reviewer is unavailable, disclose the missing audit rather than presenting a self-review as independent. If the audit finds unmet or unverified criteria, save the report, tell the user about the gaps, and wait for direction before more work. Before declaring a blocker, verify the precise failure and try a safe authorized correction when one is available; a first failed setup command is not by itself proof of an external blocker. Do not bypass scope or retry limits. Include only context Codex needs to act and audit completion. Give Codex room to choose an implementation path; do not turn the goal into a brittle step-by-step plan unless the user asked for one. Do not silently start the goal.

## Quality bar

A strong goal lets Codex answer "am I done?" against evidence without inventing success criteria. Terms such as "better", "polished", "complete", and "production-ready" need an observable meaning for this task. Acceptance criteria should cover the original outcome, not merely a checklist of internal work. Avoid arbitrary issue quotas, test counts, or file limits unless the user chose them for a reason.
