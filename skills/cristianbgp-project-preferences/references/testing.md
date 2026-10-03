# Testing preferences

Choose tests that provide evidence about the changed behavior. TDD is useful when requested or when a small failing case helps drive the change; it is not a prerequisite for every documentation or visual edit.

## Observable behavior

- Test through the public boundary that owns the behavior: a function, rendered component, HTTP endpoint, or complete user flow.
- Write expectations from requirements, known examples, or independently worked results. Do not repeat the implementation's calculation to manufacture the expected answer.
- Avoid assertions about source-code strings, private methods, incidental component structure, or internal call counts unless that detail is itself part of the contract.
- When following TDD, use a small failing case, implement the behavior, and refactor with the relevant tests passing. Avoid speculative batches of tests for interfaces that have not been established.
- Infer ordinary test boundaries from the task and repository. Ask for clarification when expected behavior is ambiguous, rather than requiring approval for every test.

## Choose the test level

- Use Vitest for business rules, validation, transformations, and service behavior where it fits. Preserve an existing effective runner.
- Use Testing Library for meaningful React interactions and states. Prefer accessible queries by role and name or label; use test IDs when semantic queries cannot identify the intended target.
- Use integration tests for contracts across real components or services. Use E2E tests for important browser flows whose correctness depends on navigation, authentication, or the complete system.
- Select coverage according to risk and the likely failure. Neither E2E-only testing nor testing every component in isolation is a universal default.
- Add dependencies only when the required checks cannot reasonably use the project's existing tools.

## Mocks and external boundaries

- Keep React, the router, and the component behavior real where practical. Mock external boundaries rather than reproducing the internals being tested.
- Use a focused HTTP substitute such as MSW when it helps verify client behavior. Check the real API contract separately; a mocked response cannot prove server compatibility.
- Use controlled clocks for time-dependent behavior and restore test state afterwards.
- If a test needs elaborate mocks of internal collaborators, reconsider its boundary or use an integration test. The number of mocks alone does not decide the test level.

## SQL and persistence

- Use database-backed tests when correctness depends on constraints, joins, transactions, migrations, or concurrency. A mocked ORM result cannot establish those behaviors.
- Use PGlite when it represents the relevant PostgreSQL behavior. Use real PostgreSQL for features or concurrency semantics that require it.
- Prepare isolated data and deterministic cleanup. Run against a dedicated test database, not production or a developer's working data.
- Assert persisted state when persistence is part of the contract, including rollback or uniqueness behavior when relevant. Avoid tying assertions to incidental schema details.

## Verification

- Run the focused checks that establish the change, then any repository-required checks. Broaden testing when failures or remaining uncertainty justify it.
- Report what ran and any material limitation. Format validation of a skill does not prove its behavior in another agent.
