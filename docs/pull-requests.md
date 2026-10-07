# Pull Request Workflow

## Scope

A PR should deliver one coherent vertical increment: enough behavior to be useful and reviewable, but not an entire roadmap.

Avoid both extremes:

- PRs that change only a trivial implementation fragment with no complete behavior;
- PRs that combine several independently reviewable features.

A good sequence for this project is:

1. support playing a single YouTube URL end to end;
2. add plain-text YouTube search;
3. add playlist input.

The exact boundaries may change as the code evolves, but keep the same principle.

## TDD and PR contents

Tests are written before implementation during development, but tests and implementation are pushed in the same PR.

Every behavior PR should contain:

- tests that specify the increment;
- the implementation that satisfies them;
- necessary refactoring;
- documentation changes when a durable project rule or architecture decision changed.

Do not create a separate implementation PR whose required tests are deferred to a later PR.

## Scope control

While implementing a PR:

- make necessary refactors when they directly support the increment;
- avoid opportunistic unrelated rewrites;
- avoid implementing future roadmap items “while already here”;
- do not build generalized abstractions without a current use case;
- leave the repository in a working state.

If a required prerequisite grows large enough to be independently useful and reviewable, split it into its own preceding PR.

## Completion checks

Before considering a PR ready:

- the intended tests pass;
- the full relevant `pytest` suite passes;
- repository-defined pre-commit checks pass;
- dependencies and lockfiles are consistent;
- no secrets are committed;
- docs are updated if the change alters documented architecture or workflow.
