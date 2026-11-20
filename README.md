# Dayyan Game Booster

A native Android companion app for Call of Duty: Mobile players. This first build focuses on truthful device information and safe pre-game guidance; it does not claim to unlock performance that Android or the phone does not expose to ordinary apps.

## Included in this project

- Native Android app built with Kotlin and Jetpack Compose.
- Dark dashboard with Home, Network, Game Preparation, and About sections.
- Battery percentage and charging state from Android.
- Battery temperature when the phone exposes that sensor value. This is **not** CPU or GPU temperature.
- Android thermal status when supported by the device and Android version.
- Active network type and Android's internet-validation state. This is **not** ping, latency, or a speed test.
- Available system RAM and total reported RAM.
- Current screen refresh rate. This is **not** the FPS rendered by CODM.
- CODM install detection and a launch shortcut for the package `com.activision.callofduty.shooter`.
- Unit test for Android thermal-status labels.
- GitHub Actions workflow that runs the unit tests, builds a debug APK, and stores the APK as a downloadable workflow artifact.
- Gradle 8.13 launcher scripts. The scripts download the pinned Gradle distribution on first use and verify its official SHA-256 checksum before running it.

## Project requirements

- Android Studio with Android SDK Platform 35 installed for local IDE builds.
- JDK 17 or newer for the build. The GitHub Actions workflow uses JDK 17.
- Android 8.0 (API 26) or newer to install the app. The target device in the project setup is Android 14, which meets this requirement.

## Build locally

Open the extracted `DayyanGameBooster` folder in Android Studio and allow Gradle sync to finish.

On Windows PowerShell, from the project folder:

```powershell
.\gradlew.bat :app:testDebugUnitTest :app:assembleDebug
```

On macOS/Linux, from the project folder:

```bash
./gradlew :app:testDebugUnitTest :app:assembleDebug
```

The debug APK is created at:

```text
app/build/outputs/apk/debug/app-debug.apk
```

The first command-line build downloads Gradle 8.13 if it is not already cached. The launcher checks the downloaded archive against the SHA-256 published by Gradle before extracting it.

## Build with GitHub Actions

1. Extract this ZIP on your computer.
2. Open your repository: <https://github.com/abduldayyanibrahim315-creator/Dayyan-game-booster->.
3. Use **Add file → Upload files** and upload the contents inside the extracted `DayyanGameBooster` folder. Keep the folder structure intact, including `.github/workflows/android.yml`.
4. Commit the upload to the `main` branch.
5. Open the repository's **Actions** tab and select the **Android APK** workflow.
6. When the run completes successfully, open that run and download the `dayyan-game-booster-debug` artifact.
7. Extract the artifact ZIP to get `app-debug.apk`, then transfer the APK to your Android phone and install it.

The workflow runs on pushes to `main`, pull requests targeting `main`, and manual workflow dispatches.

## Current limitations — important

This is the first usable app foundation, not a finished system-level game booster.

- It does not measure live CODM FPS or draw a floating FPS overlay.
- It does not force CPU/GPU clock speeds, change thermal policy, modify game files, or bypass Android/game protections.
- It does not guarantee higher FPS, lower ping, or smoother gameplay.
- Battery temperature must not be interpreted as CPU/GPU temperature.
- Display refresh rate must not be interpreted as the game's rendered frame rate.
- Network validation is not a ping or throughput measurement.
- Cloud sign-in/accounts, cross-device sync, and automatic background notifications are not implemented in this first version. They require additional design and, for accounts/sync, a backend service.
- If Android or the phone does not expose a metric, the app should show it as unavailable rather than inventing a number.

## Package details

- Application ID: `com.dayyan.gamebooster`
- Version: `0.1.0` (version code `1`)
- Minimum Android version: Android 8.0 / API 26
- Compile SDK: 35
- Main source: `app/src/main/java/com/dayyan/gamebooster/MainActivity.kt`

## Privacy

The app requests only `ACCESS_NETWORK_STATE` in this starter version. It does not request contacts, location, microphone, storage, or account credentials. No analytics or remote API service is configured.
