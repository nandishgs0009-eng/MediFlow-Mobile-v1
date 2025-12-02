# MediFlow Mobile App Setup Guide

This guide explains how to build and deploy your web application as a native mobile app using **Capacitor**.

## ✅ What Was Installed

The following dependencies have been installed to convert your web app to mobile:

### Core Capacitor Packages
- `@capacitor/core` - Core Capacitor framework
- `@capacitor/cli` - Command-line tools
- `@capacitor/android` - Android native support
- `@capacitor/ios` - iOS native support
- `@capacitor/splash-screen` - Splash screen plugin

### Capacitor Plugins (Already Installed)
- `@capacitor/app` - App lifecycle and deep linking
- `@capacitor/camera` - Camera access
- `@capacitor/device` - Device information
- `@capacitor/filesystem` - File system access
- `@capacitor/geolocation` - Location services

## 🚀 Quick Start Commands

### 1. Sync Web App to Mobile Platforms
```bash
npm run mobile:sync              # Sync to both Android and iOS
npm run mobile:sync:android      # Sync to Android only
npm run mobile:sync:ios          # Sync to iOS only
```

### 2. Open Mobile IDEs
```bash
npm run mobile:open:android      # Open Android Studio
npm run mobile:open:ios          # Open Xcode
```

### 3. Build Native Apps
```bash
npm run mobile:build             # Build both platforms
```

## 📋 Prerequisites for Building

### For Android Development
- Install **Android Studio** from https://developer.android.com/studio
- Install Android SDK
- Java Development Kit (JDK) 11 or higher
- Set `ANDROID_HOME` environment variable

### For iOS Development (Mac Only)
- Install **Xcode** from App Store
- Install CocoaPods: `sudo gem install cocoapods`
- macOS 12+

## 🔧 Project Structure

```
MediFlow-Mobile-10/
├── src/                    # React source code
├── dist/                   # Built web files
├── android/                # Android native project
├── ios/                    # iOS native project
├── capacitor.config.ts    # Capacitor configuration
└── package.json            # Project dependencies
```

## 📱 Development Workflow

### For Web Development
```bash
npm run dev                 # Start Vite dev server
```

### For Mobile Testing
1. **Make code changes** in your React components
2. **Rebuild the web app**: `npm run build`
3. **Sync to mobile**: `npm run mobile:sync:android` or `npm run mobile:sync:ios`
4. **Test in emulator/device**: Open Android Studio or Xcode

## 🎨 Mobile Features Enabled

Your app now has:
- ✅ Back button handling (Android)
- ✅ App lifecycle management
- ✅ Splash screen on launch
- ✅ Deep linking support
- ✅ Camera access (via plugin)
- ✅ Geolocation (via plugin)
- ✅ File system access (via plugin)

## 📦 App Configuration

Edit `capacitor.config.ts` to customize:
- App name
- App ID (bundle identifier)
- Splash screen timing
- Server settings

## 🔐 Signing & Publishing

### Android APK/AAB
1. Open Android Studio: `npm run mobile:open:android`
2. Navigate to **Build → Generate Signed Bundle / APK**
3. Create a signing key
4. Follow the wizard to generate release build

### iOS IPA
1. Open Xcode: `npm run mobile:open:ios`
2. Select **Product → Archive**
3. Sign with Apple Developer certificate
4. Upload to App Store Connect

## 🐛 Troubleshooting

### Sync Issues
```bash
npx cap doctor                  # Check for issues
npx cap clean                   # Clean generated files
npm run mobile:sync             # Re-sync everything
```

### Android Build Issues
- Clear Android cache: `cd android && ./gradlew clean`
- Ensure Android SDK is installed
- Check Java version: `java -version`

### iOS Build Issues
- Update CocoaPods: `pod repo update`
- Clear iOS cache: `cd ios && rm -rf Pods && pod install`

## 📚 Useful Resources

- **Capacitor Documentation**: https://capacitorjs.com/docs
- **Android Development Guide**: https://developer.android.com/guide
- **iOS Development Guide**: https://developer.apple.com/ios/
- **Capacitor Plugins**: https://capacitorjs.com/docs/plugins

## 🎯 Next Steps

1. **Test on device**: Connect Android/iOS device via USB
2. **Install app**: Run from Android Studio / Xcode
3. **Debug**: Use DevTools in web view
4. **Submit to stores**: Follow app store submission guidelines

## 📝 Notes

- Your Supabase authentication will work on mobile (already configured)
- Service Worker will function on mobile browsers
- All your existing React code works without changes
- Install more Capacitor plugins as needed: `npm install @capacitor/plugin-name`

## 💡 Pro Tips

- Use `npx cap update` to update Capacitor versions
- Always test on real devices before submission
- Use Capacitor DevTools for debugging
- Keep your app size under 100MB for best performance

---

**Happy building! 🚀**
