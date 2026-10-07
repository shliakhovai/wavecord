# AGENTS.md

## Project rules

- This is a Python `discord.py` music bot. Use `uv` for Python environment and dependency work.
- Keep `main.py` as the application entry point and composition root.
- Work test-first: add or change a failing `pytest` test before implementation, then make it pass. Tests and implementation belong in the same PR.
- Keep PRs as small vertical increments that deliver one coherent capability; do not bundle the whole roadmap into one PR.
- Keep business/domain logic separate from Discord, YouTube, FFmpeg, configuration, and other infrastructure. Put non-business implementation details under `_detail/`.
- Use the repository's existing pre-commit hook configuration as the source of truth for formatting, linting, and type checks. Do not introduce competing tooling unless explicitly requested.
- Secrets belong in `.env`; never commit credentials or tokens. Keep only safe example values in `.env.example`.
- Prefer slash commands for Discord user interactions.
- Do not put large policy or architecture explanations here. Update the relevant file under `docs/` instead.

## Contextual docs

- Architecture or file placement: `docs/architecture.md`
- Development conventions and configuration: `docs/development.md`
- Tests or TDD workflow: `docs/testing.md`
- PR scope and delivery workflow: `docs/pull-requests.md`
- Feature sequencing: `docs/roadmap.md`
