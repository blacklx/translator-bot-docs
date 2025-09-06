# Changelog

All notable changes to Translator Bot will be documented in this file.
This project follows [Semantic Versioning](https://semver.org/).

---

## [2.0.0] - 2025-09-06
### Added
- **Manual translation via context menus**:
  - `Translate → My Language`: instantly translate a message into the user’s Discord app language.
  - `Translate → Choose Language`: dropdown to translate into one of 25 common languages.
- **Bulk linking**: `/link bulk` to set up multiple channel-language pairs in one go.
- **Localization system (`i18n.ts`)** for ephemeral responses. Supports English (default), Norwegian, and partial translations for several other locales.
- Ephemeral replies now use the correct Discord **flags** API instead of deprecated `ephemeral: true`.

### Changed
- Major **file structure refactor**:
  - Split large `index.ts` into `bot.ts`, `register-commands.ts`, `queues/`, `commands/`, `services/`, and `interactions/`.
  - Removed obsolete `store.ts` and `data/stats.ts`.
- `/q` commands cleaned up and stabilized:
  - `/q stats`, `/q status`, `/q dlq`, `/q notify`, `/q healwebhooks` now work consistently.
  - Notifications can be configured per guild, and notify handler simplified.
- Improved webhook handling, translation error fallback, and message masking/restoration.
- Language dropdown reduced to 25 most common languages (single clean menu).

### Fixed
- `/q stats` hanging issue resolved.
- Errors like “Cannot read properties of undefined (reading 'delivered')” eliminated by updating queue/stat handling.
- Compatibility fixes for BullMQ and ioredis APIs.
- Corrected TypeScript configuration (`moduleResolution: NodeNext`) for builds.
- Removed deprecated `ready` event name (now `clientReady`).
- Prevented multiple PM2 processes from handling the same interactions.
- Fixed `Unknown interaction` errors by properly deferring/updating component interactions.

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
