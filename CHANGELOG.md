# Changelog

## v1.0.0

Initial public release of **Pingr** (`github.h3xord.pingr`).

### Highlights
- Monochrome Material 3 UI
- Reliable silent background monitoring via Foreground Service + `AlarmManager` (`ELAPSED_REALTIME_WAKEUP`)
- Editable Semester ID and customizable polling interval (default 30 min, minimum 20 min)
- Instant high-priority notifications displaying semester name, course code, and course title
- Session token (`access_token`) reuse until expiry to minimize login requests
- Automatic lockout guard (pauses monitoring on `401` or `>= 3` failed login attempts)
- Local-only `EncryptedSharedPreferences` storage, `allowBackup="false"`, `usesCleartextTraffic="false"`, and `FLAG_SECURE` in Settings
- Automatic monitor resume after device reboot
