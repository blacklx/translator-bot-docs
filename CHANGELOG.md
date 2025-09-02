# Changelog

All notable changes to Translator Bot will be documented in this file.  
This project follows [Semantic Versioning](https://semver.org/).

---

## [1.2.0] - 2025-09-02
### Added
- Dead Letter Queue (DLQ) system for failed jobs.
- Experimental `/q replay` command to re-enqueue DLQ jobs.
- Health checks now include latency (ms) and error codes for Discord, Redis, and Translate.

### Fixed
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
