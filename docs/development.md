# Development

## Tooling

Follow the environment setup in `README.md`, which currently uses `venv` and `pip` to install the development
tooling. `uv` is the intended dependency and environment manager once a foundation increment adds the required
project metadata and lockfile. Until then, do not add a parallel dependency workflow.

The intended application entry point is:

```text
main.py
```

The test framework is `pytest`.

Formatting, linting, and file-validation rules are defined by the repository's existing pre-commit hook
configuration. Inspect that configuration before changing code and use the tools and versions it already specifies.
Do not invent duplicate quality configurations merely because a tool is familiar.

## Configuration

Local secrets and runtime configuration belong in `.env`.

At minimum, the bot will require a Discord token. Additional settings may be introduced only when the implementation needs them.

Rules:

- never commit `.env`;
- never hard-code Discord tokens, credentials, cookies, or secrets;
- maintain `.env.example` with variable names and safe placeholder values only;
- fail clearly when required configuration is absent;
- centralize environment parsing under `_detail/` rather than reading environment variables throughout business logic.

## Dependencies

Add dependencies only when they are needed by the current increment.

Expected core integrations are:

- `discord.py` for Discord;
- `yt-dlp` for YouTube URL/search/playlist extraction;
- FFmpeg available to the runtime for audio playback;
- `pytest` for testing.

When adding or updating Python dependencies, keep the `uv` project metadata and lockfile consistent.

## Async code

Discord and voice operations are asynchronous. Keep blocking work out of the event loop. In particular, treat extraction, process invocation, and other potentially blocking operations as infrastructure concerns and isolate them behind adapters that can be tested or executed safely.

Do not introduce concurrency complexity before a feature needs it.

## Error handling

Handle expected operational failures explicitly, including cases such as:

- user not being in a voice channel when required;
- bot lacking permissions;
- unavailable or unsupported YouTube input;
- extraction failure;
- FFmpeg/playback failure;
- empty queue;
- invalid volume input;
- unavailable voice connection.

Return useful Discord-facing messages without exposing secrets, raw credentials, or unnecessary internal details.

## Documentation

Keep `AGENTS.md` short.

Put durable explanations in `docs/` and update the relevant document when architecture, workflow, or feature sequencing changes. Avoid creating documentation that only restates obvious code.
