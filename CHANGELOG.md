# Changelog

All notable changes to this project will be documented in this file.

---

## [2.1.0] - 2025-09-08
### Added
- Migrated all storage from JSON files to PostgreSQL:
  - Mirrors, stats, DLQ, settings, links, and webhook cache are now fully database-backed.
  - Migration script `npm run db:migrate` to move existing JSON data into Postgres.
- Backup-friendly design: all state is now persisted in the database, making snapshots and restores easier.
- New `/q replay` command to re-enqueue jobs from DLQ.
- Admin notifications reworked into a single `/q notify` command with sub-actions:
  - `show` – view current status
  - `enable` / `disable` – toggle notifications
  - `set` – choose a target channel
- TypeScript type-safety improvements across queues, events, and services.

### Changed
- Removed legacy JSON storage code (`data/*.json`, file-based loaders).
- Cleaned up `/q` command set:
  - Removed confusing `/q notifyon`, `/q notifyoff`, `/q notifystatus`.
  - `/q healwebhooks` simplified and better aligned with actual webhook cache handling.
- Updated interaction responses to use `flags: MessageFlags.Ephemeral` instead of deprecated `ephemeral: true`.
- Improved logging format for jobs, DLQ entries, and DB init.

### Fixed
- Duplicate key errors in `mirrors` table by correctly handling upserts and conflict resolution.
- TypeScript build errors in `linking.ts`, `notifier.ts`, and event handlers.
- Ensured `guildId` can be nullable without breaking translation events.
- Notifications no longer fail when channel is partial – uses proper `GuildTextBasedChannel` type narrowing.
- Cleared out stale global command definitions; only the new command set is registered.

---

## [2.0.0] - 2025-09-06
### Added
- Manual translation via context menus:
  - Translate → My Language: instantly translate a message into the user’s Discord app language.
  - Translate → Choose Language: dropdown to translate into one of 25 common languages.
- Bulk linking: `/link bulk` to set up multiple channel-language pairs in one go.
- Localization system (`i18n.ts`) for ephemeral responses. Supports English (default), Norwegian, and partial translations for several other locales.
- Ephemeral replies now use the correct Discord flags API instead of deprecated `ephemeral: true`.

### Changed
- Major file structure refactor:
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
- Removed deprecated ready event name (now `clientReady`).
- Prevented multiple PM2 processes from handling the same interactions.
- Fixed Unknown interaction errors by properly deferring/updating component interactions.

---

## [1.2.0] - 2025-09-02
### Added
- Dead Letter Queue (DLQ) system for failed jobs.
- Experimental `/q replay` command to re-enqueue DLQ jobs.
- Health checks now include latency (ms) and error codes for Discord, Redis, and Translate.

### Fixed
- `/q purge` no longer times out; uses deferred replies and completes reliably.
- `/q healwebhooks` now uses deferred replies and handles errors per channel, preventing command failure.
- Mentions (@user, @role, @everyone) preserved correctly in translated messages.
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
