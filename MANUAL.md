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
  Get-FileHash .\Pingr-v1.0.0.apk -Algorithm SHA256
  Get-Content .\Pingr-v1.0.0.apk.sha256
  ```
- **macOS / Linux**:
  ```bash
  sha256sum -c Pingr-v1.0.0.apk.sha256
  ```

### Install on Android
1. Open the downloaded `.apk` file on your phone.
2. If prompted, allow **Install unknown apps** for your browser or file manager.
3. Tap **Install**.

> **Updating later**: Future official releases are signed with the same release key, so you can install newer APKs directly over older versions without losing your settings or cached courses.

---

## 2. First-Time Setup

1. Launch **Pingr** and tap the **Settings** gear icon in the top-right corner.
2. Fill in **IUMS Credentials & Semester**:
   - **Student / User ID**: Your IUMS student ID.
   - **Password**: Your IUMS password (stored encrypted on your device only).
   - **Semester ID**: The numeric semester code for the term you want to monitor (e.g., `11022025` for Fall 2025).
3. Set **Polling Interval**:
   - Choose a preset (`20m`, `30m`, `45m`, `60m`) or type any number `>= 20` minutes.
4. Tap **Save Settings**. You will automatically return to the home screen.
5. Tap **Start Monitor** and grant the **Notifications** permission when prompted.
   - Starting the monitor immediately performs an initial check to fetch your semester name and current published courses.

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

> **Note on the silent background notification**: Android requires active background services to display an ongoing notification. Pingr uses a silent, minimal-priority channel (`Background Service`) so it stays out of your way and never rings or pops up.

---

## 4. Understanding Notifications & App Actions

- **New Result Alert**:
  - Title: `Pingr • New Result (<Semester Name>)` (e.g., `Pingr • New Result (Fall 2025)`)
  - Body: `<Course Code>: <Course Title>` (grades are intentionally omitted from the notification—tap it to open Pingr and view your full grades).
- **Check Now**:
  - Manually checks IUMS immediately and resets the next scheduled poll countdown.
- **Clear** (next to `Courses (N)`):
  - Clears only Pingr's locally cached course list on your phone (never affects your actual IUMS records). The next check will re-save a fresh baseline.
- **Pingr Monitor Paused**:
  - If your password changes or fails authentication (`401`), or if IUMS reports `>= 3` failed login attempts, Pingr automatically pauses monitoring and alerts you so your account does not get locked behind reCAPTCHA.
  - **Fix**: Sign into the IUMS portal once in a browser to reset the attempt counter, update your credentials in Pingr Settings, and tap **Start Monitor**.

---

## 5. Troubleshooting & FAQ

**Q: Why didn't I get a notification for courses that were already published before I installed Pingr?**  
A: The first successful check saves your existing courses as a baseline. Notifications trigger only when a **new** course appears or an existing course's grade changes afterward.

**Q: Will monitoring resume if I restart my phone?**  
A: Yes. If monitoring was active before rebooting, Pingr automatically restarts background monitoring after boot (provided Autostart/Unrestricted Battery is enabled on OEM devices).

**Q: Does Pingr store my password on any server?**  
A: No. Your credentials remain strictly inside your phone's encrypted local storage and are only sent over HTTPS to the AUST IUMS portal.

**Q: Found a bug or an issue on your device?**  
A: Open an issue on the [**Issues**](https://github.com/h3xord/Pingr/issues) tab with your phone model, Android version, and what happened.
