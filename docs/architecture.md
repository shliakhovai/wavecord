# Architecture

## Goal

Build a maintainable Discord music bot that can join voice channels and play audio sourced from YouTube through slash commands. The design should make the domain behavior testable without requiring Discord, YouTube, or FFmpeg in ordinary unit tests.

## Intended structure

```text
.
├── main.py
├── pyproject.toml
├── uv.lock
├── .env
├── .env.example
├── AGENTS.md
├── docs/
├── tests/
└── musicbot/
    ├── __init__.py
    ├── music/
    │   ├── __init__.py
    │   ├── models.py
    │   ├── queue.py
    │   └── service.py
    └── _detail/
        ├── __init__.py
        ├── config.py
        ├── discord/
        │   ├── __init__.py
        │   ├── bot.py
        │   └── cogs/
        │       ├── __init__.py
        │       └── music.py
        ├── youtube/
        │   ├── __init__.py
        │   └── yt_dlp.py
        └── audio/
            ├── __init__.py
            └── ffmpeg.py
```

This is the intended direction, not permission to create every module before it is needed. Add files incrementally as a PR requires them.

## Boundaries

### Business/domain logic

Business logic describes music-bot behavior independently of external tools. Examples include:

- track and queue models;
- queue ordering and mutations;
- what `play`, `pause`, `resume`, `skip`, and volume changes mean;
- state transitions for the active track;
- behavior when the queue is empty;
- validation rules that are part of the bot's product behavior.

Keep this logic outside `_detail/` whenever it can be expressed without importing `discord.py`, `yt-dlp`, FFmpeg-specific code, environment loaders, or other infrastructure.

### `_detail/`

`_detail/` contains software and infrastructure details needed to realize the domain behavior. Examples include:

- Discord bot setup, cogs, slash-command bindings, interactions, and voice-client adapters;
- `yt-dlp` calls and mapping extractor output into domain objects;
- FFmpeg process/source construction;
- environment-variable loading and configuration adapters;
- persistence, caches, network clients, logging adapters, and other framework integrations if they are added later.

The domain may define interfaces or protocols needed by its use cases. `_detail/` implements those interfaces.

Do not hide business rules inside cogs, `yt-dlp` wrappers, FFmpeg adapters, or configuration code.

## Entry point

`main.py` is the composition root. Keep it thin. Its responsibilities should be limited to tasks such as:

- loading configuration;
- creating the bot and dependencies;
- wiring adapters to services/cogs;
- starting the bot.

Do not place playback rules, queue behavior, or command implementations directly in `main.py`.

## Discord layer

Use `discord.py` cogs/extensions to organize slash commands. Cogs should translate Discord interactions into calls to application/domain services and translate results or failures back into Discord responses.

Avoid making cogs the owner of queue and playback business rules.

## YouTube and audio

Use `yt-dlp` as the YouTube extraction/search adapter and FFmpeg as the playback backend.

Keep extractor metadata and FFmpeg-specific objects from leaking through the domain unless a concrete requirement makes that unavoidable. Convert external data into project-owned models at the adapter boundary.

Prefer test doubles around YouTube extraction and playback in unit tests. Tests that execute real network calls or require FFmpeg should be explicitly separated as integration tests.
