# Goal Patterns

## Critique Checklist

Before finalizing a `/goal`, check that it has:

- Objective: one durable outcome, not a pile of unrelated requests.
- Context: enough project and user context to avoid cold-start guessing.
- Scope: included and excluded areas.
- Constraints: files, APIs, UX boundaries, permissions, and rollback expectations.
- Acceptance criteria: observable outcomes, not vibes.
- Verification: commands, tests, screenshots, manual flows, or reports.
- Deliverables: exact artifacts to leave behind.
- Stop rule: precise completion or pause condition.
- Drift guard: what to avoid and when to ask for help.

## QA / Bug Hunt Template

```text
/goal act as a QA engineer hunting real bugs in [project].

Context:
- Project: [what it is]
- Critical surfaces: [install, upgrade, onboarding, payment, auth, routing, etc.]
- User-visible failure modes: [what bad looks like]

Scope:
- Include realistic user paths through [areas].
- Exclude [areas that should not be touched].

Constraints:
- Hunt first; do not fix unless explicitly instructed.
- Use [testboxes/simulator/browser/local commands] to validate findings.
- Do not report duplicates or speculative issues.

Acceptance criteria:
- Find [N] discrete, reproducible new issues.
- For each issue include repro steps, expected behavior, actual behavior, severity, suspected cause, and proposed fix.

Verification:
- Run [commands/checks] where relevant.
- Capture logs, screenshots, or command output for each confirmed issue.

Deliverables:
- Write findings to [path].
- Summarize the highest-severity issues at the end.

Stop rule:
- Stop once [N] confirmed issues are logged, or pause if the environment prevents validation.
```

## Fix Existing Failing Checks Template

```text
/goal fix [specific failing checks] in [project].

Context:
- Current failure: [test/build/lint command and observed failure]
- Important boundaries: [modules/files involved]

Scope:
- Include changes needed to make [commands] pass.
- Exclude unrelated refactors, dependency upgrades, and behavior changes outside [area].

Constraints:
- Preserve public APIs unless required by the failure.
- Do not modify [files/directories] without pausing first.
- Add or update focused tests only where they prove the fix.

Acceptance criteria:
- [command] exits 0.
- Relevant targeted tests cover the fixed behavior.
- No unrelated files are changed.

Verification:
- Run [targeted command].
- Run [broader regression command if affordable].

Deliverables:
- Leave a concise summary of root cause, changed files, and verification output.

Stop rule:
- Stop when all listed verification commands pass, or pause with the smallest failing reproduction if blocked.
```

## Greenfield Feature Template

```text
/goal build [feature/tool/app] for [user/persona/use case].

Context:
- Project: [existing app or new app]
- Reference projects or files to study: [links/paths]
- Expected user workflow: [how someone will use it]
- Design or implementation patterns to adopt: [patterns]
- Anti-patterns to avoid: [previous failures, unwanted style, forbidden architecture]

Scope:
- Include [screens, APIs, storage, tests, docs].
- Exclude [nice-to-haves].

Constraints:
- Follow existing project conventions.
- Keep changes within [directories].
- Pause before adding new dependencies or external services.

Acceptance criteria:
- User can [primary workflow].
- Edge cases [list] are handled.
- [tests/build/lint/visual checks] pass.

Verification:
- Run [commands].
- Exercise [manual/browser/simulator flows].
- Capture [screenshots/logs] if UI is involved.

Deliverables:
- Implement code, tests, and any required migration/config.
- Summarize changed files, usage, and verification.

Stop rule:
- Stop when the acceptance criteria are met and verification evidence is reported.
```

## Refactor Template

```text
/goal refactor [area] to [target architecture] without changing user-visible behavior.

Context:
- Current problem: [why the refactor is needed]
- Target shape: [desired pattern]
- Risk areas: [behavior that must not regress]

Scope:
- Include [modules].
- Exclude [modules].

Constraints:
- Preserve existing APIs and data contracts unless listed.
- Keep commits or changes logically grouped if committing.
- Do not mix formatting-only churn with behavior changes.

Acceptance criteria:
- Existing behavior is preserved for [flows].
- Code now follows [target pattern].
- Tests prove the preserved behavior or newly isolated units.

Verification:
- Run [existing tests].
- Run [manual flows] if behavior is hard to cover automatically.

Deliverables:
- Code changes, tests, and a short migration note if needed.

Stop rule:
- Stop once verification passes and no unrelated diffs remain.
```

## Bad To Good Examples

Bad:

```text
/goal make onboarding better
```

Good:

```text
/goal improve onboarding completion in the web app by fixing confirmed UX and runtime failures in the signup-to-first-project flow.

Scope:
- Include signup, email verification, first project creation, and first successful dashboard load.
- Exclude billing, team invitations, and post-onboarding settings.

Acceptance criteria:
- A new user can complete the flow on desktop and mobile without console errors.
- The flow has no dead ends, disabled buttons without explanation, or missing loading/error states.
- Existing onboarding tests pass and at least one regression test covers the fixed failure.

Verification:
- Run npm test -- onboarding.
- Run npm run lint.
- Use Playwright to exercise the full flow at desktop and mobile widths and capture screenshots.

Stop rule:
- Stop when the flow passes on both viewport sizes and verification evidence is reported, or pause if test credentials are unavailable.
```
