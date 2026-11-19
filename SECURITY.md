# Security & Privacy Policy

## Data Handling

- **Local-only credentials**: Pingr stores your IUMS User ID, password, and active session token exclusively on your Android device using `EncryptedSharedPreferences` (`AES256_SIV` key encryption, `AES256_GCM` value encryption, backed by the Android Keystore).
- **No external servers**: Pingr communicates solely over HTTPS (`usesCleartextTraffic="false"`) with the AUST IUMS portal. There are no developer-hosted servers, analytics, or crash-reporting SDKs.
- **No cloud backups**: `android:allowBackup="false"` disables Google Drive Auto Backup and `adb backup`.
- **Release integrity**: Every official APK on GitHub Releases is signed with the same release certificate (`CN=Pingr, OU=h3xord, O=Pingr`) and accompanied by a `.sha256` checksum.

## Reporting a Security Issue

If you discover a security or privacy issue in Pingr, please do **not** post sensitive details publicly in an open issue. Instead, use GitHub's **Security → Advisories → Report a vulnerability** feature on this repository (once enabled), or open a minimal issue asking to coordinate a private report.
