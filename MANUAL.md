# Pingr User Manual

Complete guide for installing, configuring, and troubleshooting **Pingr** on Android.

---

## 1. Installation & Checksum Verification

### Download
1. Go to [**Releases**](https://github.com/h3xord/Pingr/releases/latest).
2. Download `Pingr-vX.Y.Z.apk` (and optionally `Pingr-vX.Y.Z.apk.sha256`).

### Optional: Verify SHA-256 Checksum
Compare the downloaded APK against the `.sha256` file from the same release:

- **Windows (Command Prompt)**:
  ```cmd
  certutil -hashfile Pingr-v2.0.0.apk SHA256
  type Pingr-v2.0.0.apk.sha256
  ```
- **macOS / Linux**:
  ```bash
  sha256sum -c Pingr-v2.0.0.apk.sha256
  ```

### Install on Android (Standard)
1. Open the downloaded `.apk` file on your phone.
2. If prompted, allow **Install unknown apps** for your browser or file manager.
3. Tap **Install**.

> **Updating from v1.0.0**: Official releases are signed with the same release key, so you can install `Pingr-v2.0.0.apk` directly over `v1.0.0` without uninstalling or losing your saved credentials and cached courses.

### Install via ADB / Platform Tools (Android 17+ or Blocked Sideloading)

If your device blocks direct APK installation (such as on **Android 17+** or restricted sideloading devices), you can install or update Pingr cleanly from a PC/Mac using Google's official **Android SDK Platform Tools (`adb`)**:

#### Step 1 — Download Platform Tools on Your Computer
1. Download the official **SDK Platform-Tools** zip from Google:  
   https://developer.android.com/tools/releases/platform-tools
2. Extract the zip file to an easy-to-find folder (for example, `C:\platform-tools` on Windows or `~/platform-tools` on macOS/Linux).
3. Copy the downloaded `Pingr-v2.0.0.apk` into that same `platform-tools` folder (this keeps the command short).

#### Step 2 — Enable USB Debugging on Your Phone
1. Open **Settings → About phone** (on some phones: **About phone → Software information**).
2. Tap **Build number** (on Xiaomi/MIUI/HyperOS: tap **OS version / MIUI version**) **7 times** until it says *"You are now a developer!"*.
3. Go back to **Settings → System → Developer options** (or **Settings → Additional settings → Developer options** on Xiaomi/Oppo/Realme).
4. Enable **USB debugging**.
5. *(Xiaomi / Redmi / POCO only)* Also enable **Install via USB** (and **USB debugging (Security settings)** if present) inside Developer options.

#### Step 3 — Connect Your Phone and Verify ADB
1. Connect your phone to your computer with a **data-capable USB cable** (switch the USB notification on your phone to **File transfer** if needed).
2. Open a terminal inside your `platform-tools` folder:
   - **Windows**: Open the `platform-tools` folder in File Explorer, click the address bar, type `cmd`, and press **Enter**.
   - **macOS / Linux**: Open Terminal and run `cd ~/platform-tools`.
3. Check that your phone is detected:
   - **Windows (Command Prompt)**:
     ```cmd
     adb devices
     ```
   - **macOS / Linux**:
     ```bash
     ./adb devices
     ```
4. Look at your phone screen and tap **Allow** (optionally check *"Always allow from this computer"*) on the **Allow USB debugging?** prompt.
5. Run the `devices` command again — you should see your device ID followed by `device` (not `unauthorized`).

#### Step 4 — Install (or Update) Pingr
Run the install command from the same terminal:

- **Windows (Command Prompt)**:
  ```cmd
  adb install -r Pingr-v2.0.0.apk
  ```
- **macOS / Linux**:
  ```bash
  ./adb install -r Pingr-v2.0.0.apk
  ```

- The `-r` flag **replaces/updates** an existing Pingr installation while keeping all your saved credentials, settings, and cached data intact. It also works for a fresh install.
- When you see `Success`, Pingr is installed and ready on your phone (you can safely unplug the USB cable).

#### Common ADB Troubleshooting
- **`adb devices` shows nothing:** Try a different USB port or a different cable (many charging cables do not carry data), and make sure **USB debugging** is turned on. On Windows, you may need your phone manufacturer's USB driver (or Google USB Driver for Pixel).
- **`unauthorized` next to device ID:** Unlock your phone screen, unplug and reconnect the USB cable, and tap **Allow** on the USB debugging popup.
- **`INSTALL_FAILED_USER_RESTRICTED` (Xiaomi / MIUI / HyperOS):** Enable **Install via USB** in Developer options (requires being signed into a Mi Account on some MIUI/HyperOS builds).
- **`INSTALL_FAILED_UPDATE_INCOMPATIBLE`:** This happens if you previously installed an unofficial/debug APK signed with a different key. Uninstall the old debug build first, then run the `adb install` command again.

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
