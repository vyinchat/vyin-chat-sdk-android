# Changelog

## [1.10.0] - 2026-04-29

### Breaking Changes

- `MessageAutoResendPolicy` default value changed from `true` to `false`. Auto-resend must now be explicitly enabled if required.

### Bug Fixes

- Fixed `GIMDatabase` singleton not being reset after `close()`, which could cause a crash on re-initialization.
- Fixed `sendCustomEvent()` sending swapped `data` and `reqId` parameters.
- Fixed Retrofit DELETE requests and `customTypes` query parameter encoding in channel APIs.

---

## [1.9.2] - 2026-03-24

### Bug Fixes

- Fixed an issue where `cachedMetaData` was not updated after calling `deleteMetaData()` or `deleteAllMetaData()`.

---

## [1.9.1] - 2026-03-23

### Bug Fixes

- `GroupChannel.getChannel()` / `OpenChannel.getChannel()` now use cache-first strategy instead of always hitting the server.
- `GroupChannel.getChannel()` callback now correctly delivers `GIMException` on failure (e.g. `ERR_UNAUTHORIZED`).

---

## [1.9.0] - 2026-03-20

- Initial public release.
