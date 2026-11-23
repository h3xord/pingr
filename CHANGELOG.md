# Changelog

## v2.0.0

Major feature and polish update for **Pingr** (`github.h3xord.pingr`).

### New Features
- **AUST Notices Tab**: Added a floating top tab switcher (**IUMS** | **Notices**) to monitor official notices from `https://aust.edu/notice` independently — no IUMS login required.
- **Independent Notice Monitoring & Alerts**: Start/stop notice polling separately with its own **Pingr Notice Alerts** notification channel. Tapping a notice card (or its right-end arrow) opens the full notice in your default browser.
- **Separate Polling Intervals**: Configure **IUMS** and **Notices** polling intervals independently in Settings (minimum `15` minutes), with one-tap presets (`15m`, `30m`, `45m`, `60m`) that apply to both.
- **Semester ID Helper**: Interactive helper (accessible via the `?` button beside Semester ID or directly from the Semester Not Found popup) that builds AUST semester codes (`11 + Term + Year`) with `Spring (01)` / `Fall (02)` and `currentYear - 1` as default.
- **Pull-to-Refresh**: Swipe down on either the **IUMS** or **Notices** tab to refresh immediately, with source-aware loading indicators.
- **Pin & Highlight Newly Published Items**: Newly detected courses and notices are pinned to the top of the list with a highlighted card border and `NEW` badge, persisted across background polls until you view the tab.

### Reliability & UI Improvements
- **Accurate Last-Checked Timestamps**: Failed fetches no longer overwrite the last successful check time.
- **Auto-Fetch on Reconnect**: If a scheduled background check fails while offline, Pingr automatically fetches as soon as internet connectivity returns.
- **Polished Monochrome UI**: Compact, symmetrical monitor cards on both tabs, cleaner section headers (`Semester: <Name>` and `Notices`), adaptive top-bar **Save** action in Settings, and stark monochrome error popups replacing snackbars.

---

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
