# Testing and TDD

## Required workflow

Development is test-driven.

For each behavior change:

1. Write or change a test that describes the desired behavior.
2. Run the relevant test and confirm it fails for the expected reason.
3. Implement the smallest coherent change that makes the test pass.
4. Refactor while keeping the tests green.
5. Run the relevant broader test set.
6. Run the quality checks defined by the repository's pre-commit hook configuration.

Do not write the implementation first and add tests afterward merely to document it.

Tests and their implementation must be delivered together in the same PR.

## Test command

Use `pytest` through the project's `uv` environment. Prefer focused test execution while iterating, then run the full suite before considering the change complete.

## Test boundaries

Favor fast unit tests for domain behavior.

Business/domain tests should normally not require:

- a real Discord connection;
- a live YouTube request;
- a running FFmpeg process;
- real credentials;
- a populated `.env`.

Use fakes, stubs, mocks, or small test adapters at infrastructure boundaries where appropriate.

Add integration tests when behavior specifically depends on the integration itself. Keep those tests identifiable and separate from ordinary domain unit tests.

## What to test

For each increment, cover externally meaningful behavior and important failure paths rather than implementation trivia.

Examples include:

- queue ordering and removal;
- playing when idle versus when a track is already active;
- skipping with and without a next track;
- pause/resume state behavior;
- volume validation and changes;
- conversion of a resolved YouTube item into a domain track;
- command behavior when the caller is not in a voice channel;
- handling failed extraction or playback.

Do not assert private implementation details when a public behavior can express the same requirement.

## Regression tests

When fixing a bug, first add a test that reproduces the bug. The fix is complete only when the regression test passes together with the relevant existing suite.
