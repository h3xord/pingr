# Pingr User Manual

Complete guide for installing, configuring, and troubleshooting **Pingr** on Android.

---

## 1. Installation & Checksum Verification

### Download
1. Go to [**Releases**](https://github.com/h3xord/Pingr/releases/latest).
2. Download `Pingr-vX.Y.Z.apk` (and optionally `Pingr-vX.Y.Z.apk.sha256`).

### Optional: Verify SHA-256 Checksum
Compare the downloaded APK against the `.sha256` file from the same release:

- **Windows (PowerShell)**:
  ```powershell
  Get-FileHash .\Pingr-v2.0.0.apk -Algorithm SHA256
  Get-Content .\Pingr-v2.0.0.apk.sha256
  ```
- **macOS / Linux**:
  ```bash
  sha256sum -c Pingr-v2.0.0.apk.sha256
  ```

### Install on Android
1. Open the downloaded `.apk` file on your phone.
2. If prompted, allow **Install unknown apps** for your browser or file manager.
3. Tap **Install**.

> **Updating from v1.0.0**: Official releases are signed with the same release key, so you can install `Pingr-v2.0.0.apk` directly over `v1.0.0` without uninstalling or losing your saved credentials and cached courses.

---

## 2. First-Time Setup

1. Launch **Pingr** and tap the **Settings** gear icon in the top-right corner.
2. *(Optional if you only want AUST Notices)* Fill in **IUMS Credentials & Semester**:
   - **Student / User ID**: Your IUMS student ID.
   - **Password**: Your IUMS password (stored encrypted on your device only).
   - **Semester ID**: The numeric semester code for the term you want to monitor (e.g., `11022025` for Fall 2025). Tap the **`?`** button next to the field to open the **Semester ID Helper** (`11 + Term (01 Spring / 02 Fall) + Year`).
3. Set **Polling Intervals**:
   - Tap a shared preset (`15m`, `30m`, `45m`, `60m`) to autofill both **IUMS** and **Notices**, or type any custom interval `>= 15` minutes for each individually.
4. Tap **Save** in the top-right corner. You will automatically return to the home screen.
5. Switch between **IUMS** and **Notices** using the floating pill switcher at the top, and tap **Start Monitor** on whichever tab(s) you want monitored (grant the **Notifications** permission when prompted).
   - Starting a monitor immediately performs an initial check to save a baseline.

---

## 3. Keeping Background Monitoring Reliable

Android manufacturers aggressively restrict background apps to save battery. For consistent background checks:

1. In Pingr **Settings → Background Reliability**, tap **Allow Unrestricted Background** and confirm **Allow**.
2. Depending on your phone brand, also check these system settings:

- **Xiaomi / Redmi / POCO (MIUI / HyperOS)**:
  - `Settings → Apps → Manage apps → Pingr`:
    - Enable **Autostart**
    - **Battery saver** → **No restrictions**
- **Samsung (One UI)**:
  - `Settings → Apps → Pingr → Battery` → **Unrestricted**
  - `Settings → Battery → Background usage limits → Never auto sleeping apps` → Add **Pingr**
- **OnePlus / Oppo / Realme (OxygenOS / ColorOS / Realme UI)**:
  - `Settings → Apps → App management → Pingr → Battery usage` → Enable **Allow background activity** and **Allow auto-launch**
- **Google Pixel / Stock Android**:
  - `Settings → Apps → Pingr → App battery usage` → **Unrestricted**

> **Note on the silent background notification**: Android requires active background services to display an ongoing notification. Pingr uses a single silent, minimal-priority channel (`Background Service`) shared across both monitors so it stays out of your way and never rings or pops up.

---

## 4. Understanding Notifications & App Actions

- **New Result Alert (IUMS)**:
  - Title: `Pingr • New Result (<Semester Name>)` (e.g., `Pingr • New Result (Fall 2025)`)
  - Body: `<Course Code>: <Course Title>` (grades are intentionally omitted from the notification—tap it to open Pingr and view your full grades).
- **New AUST Notice Alert (Notices)**:
  - Title: `Pingr • New AUST Notice` (or `Pingr • N New AUST Notices`)
  - Body: Notice title(s) and date(s). Tapping a single-notice alert opens the full notice in your default browser; tapping a multi-notice alert opens Pingr directly on the **Notices** tab.
- **New-Item Highlighting**:
  - Newly published courses and notices are pinned to the top of the list with a highlighted card border and `NEW` badge. Highlights persist across background polls until you view that tab, then clear on the next check.
- **Check Now / Pull-to-Refresh**:
  - Manually checks immediately (either via **Check Now** or by pulling down on the list) and resets the next scheduled poll countdown.
- **Clear** (next to `Semester: <Name>` or `Notices`):
  - Clears only Pingr's locally cached list on your phone (never affects your actual IUMS records). The next check will re-save a fresh baseline.
- **Offline Handling**:
  - If a check fails due to no internet or server issues, Pingr keeps your **Last checked** time at the last successful fetch. When internet connectivity returns, active monitors automatically fetch immediately.
- **Pingr Monitor Paused**:
  - If your IUMS password changes or fails authentication (`401`), or if IUMS reports `>= 3` failed login attempts, Pingr automatically pauses **IUMS** monitoring (without stopping **Notices** monitoring) and alerts you so your account does not get locked behind reCAPTCHA.
  - **Fix**: Sign into the IUMS portal once in a browser to reset the attempt counter, update your credentials in Pingr Settings, and tap **Start Monitor**.

---

## 5. Troubleshooting & FAQ

**Q: Why didn't I get a notification for courses or notices that were already published before I started monitoring?**  
A: The first successful check saves existing items as a baseline. Notifications trigger only when a **new** course, updated grade, or new notice appears afterward.

**Q: Can I use the Notices tab without entering my IUMS password?**  
A: Yes. The Notices tab scrapes the public `aust.edu/notice` page and works completely independently of IUMS credentials.

**Q: Will monitoring resume if I restart my phone?**  
A: Yes. If either monitor was active before rebooting, Pingr automatically restarts background monitoring after boot (provided Autostart/Unrestricted Battery is enabled on OEM devices).

**Q: Does Pingr store my password on any server?**  
A: No. Your credentials remain strictly inside your phone's encrypted local storage and are only sent over HTTPS to the AUST IUMS portal.

**Q: Found a bug or an issue on your device?**  
A: Open an issue on the [**Issues**](https://github.com/h3xord/Pingr/issues) tab with your phone model, Android version, and what happened.
