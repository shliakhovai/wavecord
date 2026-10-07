# Delivery Roadmap

This roadmap describes feature order, not a requirement to implement all items at once. Each step should be split into reviewable vertical PRs following `docs/pull-requests.md`.

## Foundation

Establish only the minimum project skeleton needed for the first behavior:

- `uv` project setup;
- `main.py` composition root;
- `.env` configuration for the Discord token;
- `discord.py` bot startup;
- cog/extension loading;
- test structure;
- adapter boundaries for Discord, YouTube extraction, and audio playback as they become necessary.

Do not create speculative modules that the first feature does not use.

## Playback increments

### 1. Single YouTube URL

Deliver end-to-end playback for one YouTube URL.

The increment should establish the basic flow from slash command to extraction to voice playback, together with the minimum queue/playback state required for correct behavior.

### 2. Plain-text search

Allow the same play command to accept ordinary text and resolve an appropriate YouTube result.

Reuse the existing playback path rather than creating a second independent playback implementation.

### 3. Playlists

Accept YouTube playlist input and enqueue resolved tracks in the intended order.

Define and test failure behavior for unavailable or partially resolvable playlist entries.

## Voice and playback controls

Introduce controls as coherent increments, integrating with the same playback state:

- join;
- leave;
- pause;
- resume;
- skip;
- queue display/management;
- volume control.

Command handlers remain thin; command-independent rules belong in the domain/application layer.

## Slash commands

Discord user-facing commands should use slash commands. Keep names and responses consistent as the command set grows.

Do not couple core playback behavior to Discord interaction objects. This allows the business behavior to remain unit-testable.

## Later considerations

Only introduce these when a real requirement appears:

- persistence across restarts;
- per-guild saved settings;
- advanced queue editing;
- loop/repeat modes;
- autoplay/recommendations;
- caching;
- metrics or external observability;
- deployment-specific orchestration.

They are intentionally outside the initial scope.
