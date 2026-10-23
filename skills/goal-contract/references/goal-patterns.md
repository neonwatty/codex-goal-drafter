# Goal Interview Patterns

Use the section matching the user's work. Combine sections for hybrid goals. These are prompts for discovering a contract, not a questionnaire to recite. Skip answered questions and follow up where an answer changes the finish line.

## Questions shared by every goal

- **Outcome:** Who benefits, and what can they do or decide when this succeeds?
- **Breadth:** What is the smallest complete outcome? Which adjacent surfaces must work for it to be real? Which are outside this run?
- **Acceptance:** What would convince the user that the outcome happened? What could look complete while actually missing the point?
- **Evidence:** What will be inspected, run, measured, demonstrated, or compared? What is the baseline, if relevant?
- **Authority:** Is this discovery, implementation, or both? Are code changes, dependencies, migrations, external services, publishing, or PRs within scope?
- **Deliverables:** What should exist at the end, and where should findings or artifacts live?
- **Stop:** When is the goal complete? Which blocker or decision should bring it back to the user?

If the user says “make it better,” ask which experience or outcome they mean, then offer a few concrete interpretations. If they say “QA it,” ask what journey or failure class matters and whether to report findings, fix confirmed issues, or both. If they say “done when tests pass,” ask which user-visible claim those tests establish and what else must be checked. Keep going until the user can recognize a successful and an unsuccessful result.

Do not demand precision that the work cannot supply. A discovery goal may finish with an evidence-backed decision and explicit unknowns. A feature goal may need a working user journey. Label uncertainties rather than disguising them as acceptance criteria.

## Feature development

Ask about the primary user journey, the first and last observable steps, and the states that could prevent completion. Determine whether existing data, permissions, integrations, or migration paths are part of the goal. Distinguish essential behavior from follow-on improvements.

Useful acceptance evidence: demonstrate the full journey, exercise meaningful edge and error states, run relevant tests, and inspect the result in its real UI or API surface. Ask which environments and user roles matter. Do not require every possible edge case or broad suite without a reason.

## UX or visual work

Ask what users currently struggle with, which screens or states are included, and what “better” means here: task completion, clarity, accessibility, visual match, responsiveness, or another criterion. Identify references or design constraints when available. Ask whether behavior may change or only presentation.

Useful acceptance evidence: walk through the task at relevant viewport sizes, inspect loading and error states, compare against references when supplied, and run applicable accessibility or UI checks. A screenshot alone does not establish that the interaction works.

## QA and bug discovery

Ask which workflows and failure modes to probe, which environments and accounts are available, and whether the run should investigate only or also fix confirmed defects. Agree on coverage boundaries and the standard for reporting a finding: reproduction, expected and actual behavior, severity, and evidence.

Finish when the agreed surfaces and realistic failure modes have been checked and confirmed findings plus coverage gaps are documented. Do not invent an issue quota or keep searching solely to meet a count. If fixing is included, agree on the fix scope and regression proof separately.

## Test repair or reliability

Ask for the failing command, observed symptom, baseline, and whether the goal is to repair the product behavior, a flaky test, the test environment, or all relevant causes. Identify behavior that must remain intact and any known intermittent conditions.

Useful acceptance evidence: reproduce the failure when possible, show the targeted check passing repeatedly when flakiness is at issue, run proportionate regression checks, and explain the cause. A green run without a credible cause may not resolve a flaky failure.

## Experiment or research

Ask the user to choose the intended finish: an evidence-backed decision, measured comparison, prototype, reproducible result, report, or another artifact. Ask which hypothesis or options matter, what baseline and evaluation method are credible, and what result would change the decision. Decide how to report negative results, inconclusive evidence, and unavailable inputs.

Useful acceptance evidence: source-backed findings, reproducible measurements, a working prototype evaluated against named criteria, or an explicit decision with uncertainty. Do not treat building a prototype as success when the user wanted a decision, or vice versa.

## Creation of an artifact

Ask who will use the artifact, in what setting, and what it must contain or enable. Establish format, destination, reference examples, quality criteria, and any review or export requirements. For creative work, ask which aspects are fixed and where exploration is welcome.

Useful acceptance evidence: inspect the finished artifact in its intended viewer, check required content and format, and exercise any interactive behavior. For visuals, compare against references or agreed visual criteria rather than asserting that the output is “polished.”

## Contract check

Before presenting the contract, test it against three questions:

1. Could the agent satisfy every listed task yet fail the user's original outcome? If yes, strengthen the outcome or acceptance criteria.
2. Could the agent reasonably stop too early or continue indefinitely? If yes, sharpen the finish or blocked condition.
3. Does each acceptance criterion have a credible evidence source? If no, ask, narrow it, or mark it as a judgment for the user.

Keep the contract short enough to review in one pass. Wait for explicit confirmation. If the user corrects it, update the contract and ask for confirmation again when the correction materially changes the finish line. Save the confirmed version in the project and transform it into `/goal` without quietly adding scope.

A saved contract needs a stable outcome, included and excluded scope, acceptance criteria with IDs and evidence, verification including any walkthrough, deliverables, constraints, and completion and blocked conditions. The IDs make a separate read-only reviewer able to report `met`, `unmet`, or `unverified` for each criterion without losing the original finish line. The coordinator saves that report as an adjacent `.audit.md` receipt. An audit with gaps returns to the user for review before the executor does more work. A claimed blocker needs a verified cause and a check for a safe authorized correction, within the contract's limits.

Use a compact shape such as:

```markdown
# Goal contract: <outcome>

## Outcome and breadth
<Who can do or decide what; included and excluded surfaces.>

## Acceptance criteria
| ID | Observable condition | Evidence |
| --- | --- | --- |
| AC1 | <condition> | <walkthrough, test, artifact, measurement, or source> |

## Verification and deliverables
<Relevant walkthrough and tests; artifacts and evidence to leave behind.>

## Constraints and stop conditions
<Authority boundaries, preserved behavior, completion rule, and blockers.>

## Audit rule
A separate read-only reviewer checks each AC against evidence. The coordinator saves the review beside this contract as `<contract-stem>.audit.md`. Report unmet or unverified criteria to the user and wait before doing more work.
```

The final `/goal` may point to this file instead of repeating it in full. Adapt this starter to the confirmed contract:

```text
/goal Fulfill the confirmed contract at docs/goal-contracts/<slug>.md. Work within its scope and collect evidence for each acceptance criterion. Verify a suspected blocker and a safe authorized correction before stopping, without exceeding the contract's limits. Before claiming completion, delegate a read-only audit to a separate agent using $goal-audit and save its report beside the contract as <slug>.audit.md. If the auditor reports unmet or unverified criteria, report the gaps to me and wait for my direction before further work. Complete only when the saved independent audit supports every criterion and the original outcome.
```

If the installed plugin or a separate reviewer is unavailable, disclose the missing independent audit and ask the user how to proceed; do not silently replace it with self-review.
