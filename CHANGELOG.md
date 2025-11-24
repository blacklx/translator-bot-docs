# Changelog

All notable changes to Translator Bot will be documented in this file.
This project follows [Semantic Versioning](https://semver.org/).

---

## [2.1.1] - 2025-11-24
### Fixed
- Context-menu translation replies now truncate to Discord's 2 000-character limit instead of failing with “Something went wrong” on long messages.
- “Translate → Choose Language” now removes its dropdown after replying so the response stays clean and can’t be re-run accidentally.
- Attachment-only mirrors now send a placeholder line (“(attachments only)”) so Discord webhooks no longer reject empty messages.
- `/link bulk` now falls back to live guild fetches so channel names resolve even when they aren’t already cached.
- Worker now trims mirrored messages to Discord's 2 000-character webhook limit and appends a truncation notice, preventing DLQ churn when Nitro users exceed the bot's posting cap.
- DLQ entries and admin notifications now trigger only after the final retry fails, reducing noise from transient errors.
- `/q healwebhooks` now walks all linked channels, recreates missing hooks, and refreshes cached IDs instead of being a placeholder; webhook cache updates are granular per channel.
- All locale-to-language mapping now goes through a single helper so both translation commands interpret user locales consistently.

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
