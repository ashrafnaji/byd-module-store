# BYD Module Store — GitHub Repository

This repository hosts the **Magisk module catalog** for BYD head units.  
The [BYD Module Store APK](https://github.com/YOUR_GITHUB_USERNAME/byd-module-store/releases) reads `modules.json` from this repo, detects the installed head unit model, and shows compatible modules ready to install.

---

## Requirements (on the head unit)

| Requirement | Details |
|-------------|---------|
| Root | `su` must be available |
| Magisk | v20.4 or newer (`magisk --install-module` support) |
| Internet | Head unit must reach GitHub (Wi-Fi or mobile hotspot) |
| Android | API 26+ (Android 8.0+) |

---

## Supported Unit Models

| `ro.vehicle.type` | Model |
|-------------------|-------|
| `Di3.0_3.5UI` | BYD Di3.0 / Atto 3 3.5" UI |
| `Di3.0` | BYD Di3.0 standard |
| `Di4.0` | BYD Di4.0 |
| `*` | Any BYD unit |

---

## Available Modules

| ID | Name | Description |
|----|------|-------------|
| `byd-androidauto` | Android Auto | Patched Android Auto APK |
| `byd-carplay` | CarPlay + MFi Hook | Apple CarPlay via MFi emulation |
| `byd-lang-arabic` | Arabic UI Language Pack | RTL Arabic for 13 system APKs |
| `byd-voice-engine` | iFlytek Global Voice Engine | Multi-language voice (AR/EN/RU…) |
| `byd-store` | BYD App Store | BydStore marketplace APK |
| `byd-gms` | Google Mobile Services | GMS / Google Play |
| `byd-sigspoof` | Signature Spoofing | Framework sig-spoof patch |
| `byd-ota-patcher` | OTA Update Bypass | Block unwanted firmware updates |

---

## How to Add a New Module

1. Build your Magisk module ZIP with the standard Magisk format  
   (must contain `META-INF/com/google/android/update-binary` and `module.prop`).

2. Create a GitHub Release and upload the ZIP:
   ```
   Tag:  v1.0.0
   Asset: byd-your-module.zip
   ```

3. Add an entry to [`modules.json`](modules.json):
   ```json
   {
     "id": "byd-your-module",
     "name": "Your Module Name",
     "description": "What it does",
     "version": "1.0.0",
     "versionCode": 1,
     "author": "Your Name",
     "minMagisk": 20400,
     "compatibleUnits": ["Di3.0_3.5UI"],
     "compatibleSdkMin": 29,
     "compatibleSdkMax": 30,
     "downloadUrl": "https://github.com/YOUR_GITHUB_USERNAME/byd-module-store/releases/download/v1.0.0/byd-your-module.zip",
     "sha256": "",
     "sizeMb": 5.0,
     "changelog": "Initial release",
     "requires": []
   }
   ```

4. Commit & push. The app will pick up the new entry on next refresh.

---

## SHA256 Checksums (recommended)

Generate the SHA256 of your ZIP and add it to `modules.json` for integrity verification:

```bash
# Linux / macOS
sha256sum byd-your-module.zip

# Windows PowerShell
Get-FileHash byd-your-module.zip -Algorithm SHA256
```

---

## Repository Structure

```
byd-module-store/
  modules.json          ← Catalog read by the app
  README.md
  (module ZIPs are in GitHub Releases, not in this repo)
```

---

## Build the APK

```bash
cd android/
./gradlew assembleRelease
# Output: app/build/outputs/apk/release/app-release-unsigned.apk
```

Then sign it (or use `assembleDebug` for testing via ADB):
```bash
./gradlew assembleDebug
adb install app/build/outputs/apk/debug/app-debug.apk
```

---

## License

Community project. Use at your own risk.  
Modifying head unit software may void your warranty.
