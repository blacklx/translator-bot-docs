# Changelog

All notable changes to Translator Bot will be documented in this file.
This project follows [Semantic Versioning](https://semver.org/).

---

## [1.3.0] - 2025-09-03
### Added
- Support for upgrading plain-text mentions (e.g. `@navn`) in language channels to real Discord mentions (`<@id>`), so pings now propagate correctly to the main channel.
- Fuzzy mention resolution: matches display names and usernames, supports Unicode/diacritics, and resolves unique `startsWith` or substring matches.
- Debug logging for Discord client lifecycle, shard events, and unhandled errors.
- Token preflight check on startup to verify `DISCORD_TOKEN` validity.

### Fixed
- Removed duplicate helper function that caused TypeScript syntax errors.
- Corrected placement of `client.on(...)` event handlers to avoid “used before declaration” errors.
- Cleaned up intents array (removed stray commas) and ensured `GuildMembers` intent is included exactly once.

---

## [1.2.0] - 2025-09-02
### Added
- Dead Letter Queue (DLQ) system for failed jobs.
- Experimental `/q replay` command to re-enqueue DLQ jobs.
- Health checks now include latency (ms) and error codes for Discord, Redis, and Translate.

### Fixed
- `/q purge` no longer times out; uses deferred replies and completes reliably.
- `/q healwebhooks` now uses deferred replies and handles errors per channel, preventing command failure.
- Mentions (`@user`, `@role`, `@everyone`) preserved correctly in translated messages.
- Admin notifications throttled to avoid spam.
- Various TypeScript fixes and interaction handling.

---

## [1.1.0] - 2025-08-28
### Added
- `/q stats` command now shows translation failure counts.
- Improved `/q status` with service health checks.

### Changed
- Fallback system posts original message if translation fails completely.
- Admin notification channel can be configured via `/q notify`.

### Fixed
- Race conditions when editing/deleting mirrored messages.
- Better error handling when webhooks are missing.

---

## [1.0.0] - 2025-08-20
### Added
- Initial release of Translator Bot.
- Channel linking with `/link`.
- Queue overview with `/q status`.
- Error notifications with `/q notify`.
- Retry and fallback on Google Translate errors.
- Stats tracking (delivered, characters translated, failures).
