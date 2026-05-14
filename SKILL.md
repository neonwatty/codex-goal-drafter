---
name: codex-goal-drafter
description: Draft, critique, and refine durable Codex /goal statements for long-running autonomous coding work. Use when the user asks to create, improve, review, or structure a /goal prompt; wants acceptance criteria, stop conditions, constraints, or verification plans for Codex goals; or is about to run a multi-step Codex task that should continue until a measurable outcome is reached.
---

# Codex Goal Drafter

## Purpose

Turn an intended task into an auditable `/goal` statement that Codex can pursue, verify, and stop. Treat `/goal` as a constraint workflow, not a generic task prompt.

## Workflow

1. Clarify the target only when required.
   Ask at most three questions if the task lacks a repository, scope boundary, verification method, or stop condition. Otherwise make conservative assumptions and state them in the drafted goal.

2. Warm up the context before the goal.
   Include a short preamble when useful: what the project is, important surfaces, user-visible failure modes, work already tried, and known anti-patterns. Do not make the `/goal` depend on vague project lore.

3. Draft the goal around evidence.
   Every goal must include scope, constraints, acceptance criteria, verification commands or checks, deliverables, and a stop rule.

4. Separate discovery from fixing.
   For QA or bug-hunting goals, prefer "hunt first" unless the user explicitly asks for fixes. If fixes are included, define whether Codex should commit, open PRs, or only produce patches.

5. Make completion measurable.
   Replace fuzzy endings like "until everything is fixed" with concrete stop conditions such as "until `npm test` passes", "until 20 discrete issues are logged", or "until the three listed screens match the attached screenshots at desktop and mobile sizes."

6. Include a drift guard.
   Add explicit non-goals, forbidden files or directories, maximum blast radius, and when Codex should pause for human input.

## Output Shape

Produce:

- A ready-to-paste `/goal` block.
- A short rationale naming the key constraints and stop condition.
- Optional warm-up context to send before `/goal` if the model needs project orientation.

Prefer this structure:

```text
/goal [role + objective]

Context:
- Project:
- Important surfaces:
- User-visible failure modes:
- Prior attempts / ruled-out approaches:

Scope:
- Include:
- Exclude:

Constraints:
- Do not:
- Preserve:
- Pause and ask if:

Acceptance criteria:
- [measurable condition]
- [measurable condition]

Verification:
- Run:
- Inspect:
- Evidence to report:

Deliverables:
- [branch/PR/report/patch/tests/log]

Stop rule:
- Stop when [specific measurable end state] or pause if [blocker].
```

## Quality Bar

A good `/goal` statement lets Codex answer "am I done?" without inventing success criteria. Reject or rewrite goals that rely on words like "better", "polished", "complete", "robust", or "production-ready" unless those words are backed by concrete checks.

Use references/goal-patterns.md for reusable templates, critique checklist, and examples.
