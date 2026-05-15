# LYRIX — APK Build Guide

## Option A: GitHub Actions (easiest, no Android Studio needed)

1. Create a new GitHub repo and push this entire folder to it
2. Go to your repo → **Actions** tab
3. The workflow runs automatically — wait ~5 minutes
4. Go to the completed run → **Artifacts** → download `lyrix-debug-apk`
5. Unzip it — you have your `.apk` file

To install on your phone:
- Enable **Settings → Install unknown apps** for your browser/file manager
- Transfer the APK to your phone and tap to install

---

## Option B: Android Studio on Windows 11 (first-time local build)

### Prerequisites
Install these in order:
1. [Node.js LTS](https://nodejs.org) — tick "Add to PATH" during install
2. [Android Studio](https://developer.android.com/studio) — during setup wizard, install:
   - Android SDK
   - Android SDK Platform (API 34)
   - Android Virtual Device
3. Git (optional but recommended)

Set the `ANDROID_HOME` environment variable:
- Search Windows → "Edit the system environment variables"
- New variable: `ANDROID_HOME` = `C:\Users\<YOU>\AppData\Local\Android\Sdk`
- Add to `Path`: `%ANDROID_HOME%\platform-tools`

### Build steps (run in Command Prompt or PowerShell)

```bat
cd lyrix-apk
npm install
npx cap add android
npx cap sync android
npx cap open android
```

This opens the project in Android Studio. Then:
- Wait for Gradle sync to finish (first time takes a few minutes)
- Menu → **Build → Build Bundle(s) / APK(s) → Build APK(s)**
- Click "locate" in the notification that appears
- Your APK is in `android\app\build\outputs\apk\debug\app-debug.apk`

---

## Updating the app later

After editing `www/index.html`, just run:
```bat
npx cap sync android
```
Then rebuild the APK (or push to GitHub and let Actions do it).

---

## Going further: signed release APK

The debug APK works fine for personal use. For Google Play or sharing
without "untrusted app" warnings, you'd need a signed release APK.
Ask Claude to walk you through generating a keystore when you're ready.
