# 📱 How to Install MediFlow Mobile App

This guide shows you how to install the MediFlow app on Android and iOS devices after cloning from GitHub.

## 📥 Step 1: Clone the Repository

```bash
git clone https://github.com/nandishgs0009-eng/MediFlow-Mobile-v1.git
cd MediFlow-Mobile-v1
```

## 📦 Step 2: Install Dependencies

```bash
npm install --legacy-peer-deps
```

This installs all required packages including:
- React & Vite
- Capacitor framework
- Android/iOS support
- All plugins (Camera, Geolocation, etc.)

## 🔨 Step 3: Build Web App

```bash
npm run build
```

This creates the `dist/` folder with production-ready web files.

## 🎯 Step 4: Sync to Mobile Platforms

```bash
npm run mobile:sync
```

This syncs the built web app to both Android and iOS native projects.

---

# 🤖 Install on Android

## Prerequisites

1. **Android Studio** - Download from https://developer.android.com/studio
2. **Android SDK** - Installed via Android Studio
3. **Java Development Kit (JDK) 11+** - Required for building
4. **Android Device or Emulator**

### Verify Android Setup
```bash
java -version                    # Check Java
echo %ANDROID_HOME%              # Check Android SDK path
```

If `ANDROID_HOME` is not set:
1. Find your Android SDK location (usually `C:\Users\YourName\AppData\Local\Android\Sdk`)
2. Add to Windows Environment Variables

## Installation Steps

### Option A: Using Android Studio (Easiest)

1. **Open Android Studio project:**
   ```bash
   npm run mobile:open:android
   ```

2. **Select your device or emulator:**
   - Click on device dropdown at top
   - Select connected phone or create emulator

3. **Run the app:**
   - Click the green **Play (▶)** button
   - Wait for build and installation to complete

### Option B: Using Command Line

1. **Build the APK:**
   ```bash
   cd android
   ./gradlew build
   ```

2. **Install on connected device:**
   ```bash
   ./gradlew installDebug
   ```

3. **Back to main directory:**
   ```bash
   cd ..
   ```

### Option C: Using ADB (Android Debug Bridge)

1. **Connect Android device via USB**

2. **Enable USB Debugging on phone:**
   - Settings → About Phone → Tap Build Number 7 times
   - Back to Settings → Developer Options → Enable USB Debugging

3. **Install from command line:**
   ```bash
   cd android
   adb install -r app/build/outputs/apk/debug/app-debug.apk
   cd ..
   ```

## Verify Installation

1. Look for **MediFlow** app on home screen
2. Tap to launch
3. You should see the login screen

---

# 🍎 Install on iOS

## Prerequisites

⚠️ **iOS development requires a Mac with Xcode**

1. **Xcode** - Download from App Store
2. **CocoaPods** - Install via:
   ```bash
   sudo gem install cocoapods
   ```
3. **iOS Device or Simulator**

## Installation Steps

### Option A: Using Xcode (Recommended)

1. **Open Xcode project:**
   ```bash
   npm run mobile:open:ios
   ```

2. **In Xcode, select your target:**
   - Click on project name in sidebar
   - Select "Signing & Capabilities"
   - Choose your team for signing

3. **Select device:**
   - At top, select your device or simulator

4. **Build & Run:**
   - Press **Cmd + R** or click Play button
   - Wait for build to complete

### Option B: Using Command Line

1. **Build for simulator:**
   ```bash
   cd ios
   xcodebuild -workspace App/App.xcworkspace -scheme App -configuration Debug -derivedDataPath build -arch x86_64 -sdk iphonesimulator
   cd ..
   ```

2. **Build for device:**
   ```bash
   cd ios
   xcodebuild -workspace App/App.xcworkspace -scheme App -configuration Debug
   cd ..
   ```

## Verify Installation

1. Look for **MediFlow** on home screen
2. Tap to launch
3. You should see the login screen

---

# 🔑 First Time Setup

Once the app is installed:

1. **Login with your credentials:**
   - Email: your@email.com
   - Password: your password

2. **Grant permissions when asked:**
   - ✅ Camera (for photos if needed)
   - ✅ Location (for medical records)
   - ✅ File access (for documents)

3. **App is ready to use!**

---

# 🐛 Troubleshooting

## Android Issues

### App won't install
```bash
# Clear cache
cd android
./gradlew clean
./gradlew build
cd ..

# Try again
npm run mobile:open:android
```

### Gradle build fails
- Ensure Java 11+ is installed: `java -version`
- Update Android SDK via Android Studio
- Check `ANDROID_HOME` environment variable

### APK install fails on device
```bash
# Uninstall old version first
adb uninstall com.nandishmediflow.app

# Then install new version
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

## iOS Issues

### CocoaPods error
```bash
pod repo update
cd ios
pod install
cd ..
```

### Xcode build fails
1. Clean build folder: **Cmd + Shift + K**
2. Delete derived data: `rm -rf ~/Library/Developer/Xcode/DerivedData/*`
3. Rebuild: **Cmd + B**

### Code signing error
1. Select project in Xcode
2. Go to Signing & Capabilities
3. Select your Apple Developer account
4. Choose provisioning profile

---

# 🚀 Development Workflow

## After Making Code Changes

1. **Save changes** in your editor
2. **Rebuild web app:**
   ```bash
   npm run build
   ```
3. **Sync to mobile:**
   ```bash
   npm run mobile:sync
   ```
4. **Reload app** in emulator/device:
   - Android: Cmd + M or Menu → Reload
   - iOS: Cmd + R or shake device

---

# 📊 Testing the App

### On Physical Device (Best)

1. Connect device via USB
2. Build and run from IDE
3. Test all features:
   - Login/Logout
   - Add treatments
   - Add medicines
   - View dashboard
   - Camera access
   - Geolocation

### On Emulator

1. Start Android Emulator from Android Studio
2. Or use iOS Simulator from Xcode
3. Run same tests as physical device

### Debug Mode

**Android:**
```bash
adb logcat | grep "MediFlow"
```

**iOS:**
- Open Console in Xcode to see logs

---

# 📝 Build for Release

## Android Release Build

1. Open Android Studio
2. **Build → Generate Signed Bundle / APK**
3. Create/select signing key
4. Choose "Release" build type
5. Generated APK ready for Play Store

## iOS Release Build

1. Open Xcode
2. **Product → Archive**
3. Sign with Apple Developer certificate
4. Generated IPA ready for App Store Connect

---

# 🆘 Quick Reference

| Task | Command |
|------|---------|
| Install dependencies | `npm install --legacy-peer-deps` |
| Build web app | `npm run build` |
| Sync to mobile | `npm run mobile:sync` |
| Open Android Studio | `npm run mobile:open:android` |
| Open Xcode | `npm run mobile:open:ios` |
| Check setup | `npx cap doctor` |
| Clean everything | `npx cap clean` |

---

# 📚 Learn More

- **Capacitor Docs**: https://capacitorjs.com/docs
- **Android Dev**: https://developer.android.com/docs
- **iOS Dev**: https://developer.apple.com/documentation/
- **GitHub Repo**: https://github.com/nandishgs0009-eng/MediFlow-Mobile-v1

---

## ✅ Installation Complete!

Your MediFlow app is now installed and ready to use! 🎉

**Need help?** Check the troubleshooting section or review the main MOBILE_SETUP.md file.
