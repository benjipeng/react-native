# Expo vs React Native CLI: Complete Comparison Guide

## Overview

When starting a React Native project, you have two main paths: **Expo** (a framework built on React Native) or **React Native CLI** (plain React Native). This guide explains the differences, trade-offs, and helps you choose the right approach for your project.

## Prerequisites

- Understanding of React fundamentals
- Basic command-line knowledge
- Node.js installed (v18 or later recommended)

## What is React Native?

React Native is a framework for building native mobile apps using React. It compiles to actual native iOS and Android components, not web views or hybrid apps.

## What is Expo?

Expo is a **framework and platform built on top of React Native** that provides:
- Pre-configured native modules
- Development tools and services
- Cloud build infrastructure (EAS)
- Over-the-air (OTA) update system
- Simplified configuration

**Think of it as:** React Native is the engine, Expo is the complete car with all features included.

## What is React Native CLI?

React Native CLI is the **bare-bones React Native** without additional frameworks:
- Direct access to native iOS and Android projects
- Full control over native code
- Manual configuration required
- No pre-built services

**Think of it as:** Building the car yourself from engine parts - maximum control, maximum effort.

---

## Quick Decision Guide

**Choose Expo if:**
- ✅ Building a new app from scratch
- ✅ You're a solo developer or small team
- ✅ You want fast development and iteration
- ✅ You don't need custom native modules (yet)
- ✅ You want cloud builds and OTA updates
- ✅ You don't have a Mac (but need iOS builds)

**Choose React Native CLI if:**
- ✅ You need custom native modules immediately
- ✅ You're integrating into an existing native app
- ✅ You require the smallest possible app size
- ✅ You have dedicated iOS/Android developers
- ✅ You need full control over build process

---

## Installation & Setup

### Expo Setup

**Requirements:**
- Node.js (v18+)
- npm or yarn
- Phone with Expo Go app (optional, for testing)

**Installation:**
```bash
# No additional setup needed!
# Create and run in one command:
npx create-expo-app MyApp
cd MyApp
npm start
```

**Time to first run:** ~1 minute

**What you DON'T need:**
- ❌ Xcode (for development)
- ❌ Android Studio (for development)
- ❌ CocoaPods setup
- ❌ Java JDK configuration

### React Native CLI Setup

**Requirements:**
- Node.js (v18+)
- Watchman (macOS)
- Xcode (macOS, for iOS)
- Android Studio
- Java JDK 17
- CocoaPods
- Android SDK
- Environment variables configured

**Installation (macOS example):**
```bash
# Install Homebrew dependencies
brew install node
brew install watchman

# Install CocoaPods
sudo gem install cocoapods

# Install Android Studio (manual download)
# Install Xcode from Mac App Store
# Configure ANDROID_HOME environment variable
# Configure Java paths

# Create project
npx react-native@latest init MyApp

# Install iOS dependencies
cd MyApp/ios
pod install
cd ..

# Run (requires simulator/emulator running)
npm run ios
npm run android
```

**Time to first run:** 30 minutes to 2 hours (depending on experience)

---

## Project Structure Comparison

### Expo Project Structure

```
MyApp/
├── .expo/                    # Expo cache (gitignored)
├── assets/                   # Images, fonts, etc.
│   ├── icon.png             # App icon
│   ├── splash.png           # Splash screen
│   └── adaptive-icon.png    # Android adaptive icon
├── node_modules/
├── .gitignore
├── app.json                 # App configuration (main config file)
├── App.js                   # Entry point
├── babel.config.js
├── package.json
└── README.md

# Clean and simple - NO native folders
```

**app.json (Expo configuration):**
```json
{
  "expo": {
    "name": "MyApp",
    "slug": "my-app",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "userInterfaceStyle": "light",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "ios": {
      "supportsTablet": true,
      "bundleIdentifier": "com.mycompany.myapp",
      "buildNumber": "1.0.0"
    },
    "android": {
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#ffffff"
      },
      "package": "com.mycompany.myapp",
      "versionCode": 1
    },
    "web": {
      "favicon": "./assets/favicon.png"
    },
    "plugins": []
  }
}
```

### React Native CLI Project Structure

```
MyApp/
├── ios/                           # Complete iOS project
│   ├── MyApp/
│   │   ├── AppDelegate.h         # iOS app lifecycle (Objective-C header)
│   │   ├── AppDelegate.mm        # iOS app lifecycle (Objective-C++)
│   │   ├── Info.plist            # iOS app configuration
│   │   ├── Images.xcassets/      # iOS image assets
│   │   ├── LaunchScreen.storyboard
│   │   └── main.m                # iOS entry point
│   ├── MyApp.xcodeproj/          # Xcode project files
│   ├── MyApp.xcworkspace/        # Xcode workspace
│   ├── Podfile                   # iOS dependency manager config
│   ├── Podfile.lock
│   └── Pods/                     # Installed iOS dependencies
│
├── android/                       # Complete Android project
│   ├── app/
│   │   ├── src/
│   │   │   ├── main/
│   │   │   │   ├── java/com/myapp/
│   │   │   │   │   ├── MainActivity.java        # Android main activity
│   │   │   │   │   └── MainApplication.java     # Android app lifecycle
│   │   │   │   ├── AndroidManifest.xml         # Android app configuration
│   │   │   │   └── res/                        # Android resources
│   │   │   │       ├── drawable/               # Images
│   │   │   │       ├── mipmap-*/              # App icons
│   │   │   │       └── values/                 # Strings, colors, styles
│   │   ├── build.gradle                        # App-level build config
│   │   └── proguard-rules.pro                  # Code obfuscation rules
│   ├── gradle/                                  # Gradle wrapper
│   ├── build.gradle                             # Project-level build config
│   ├── gradle.properties                        # Gradle properties
│   ├── settings.gradle                          # Gradle settings
│   └── local.properties                         # Local SDK paths
│
├── node_modules/
├── .gitignore
├── App.tsx                        # Main app component
├── index.js                       # JS entry point
├── app.json                       # Basic app metadata
├── babel.config.js
├── metro.config.js                # Metro bundler config
├── package.json
├── tsconfig.json                  # TypeScript config
└── README.md

# Full native projects - complete control, more complexity
```

**Key difference:** React Native CLI gives you the complete `ios/` and `android/` folders with all native code. Expo manages these behind the scenes.

---

## Configuration Comparison

### Expo: Declarative Configuration

**All configuration in one file (`app.json` or `app.config.js`):**

```json
{
  "expo": {
    "name": "MyApp",
    "slug": "my-app",
    "version": "1.0.0",
    "orientation": "default",
    "icon": "./assets/icon.png",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "assetBundlePatterns": [
      "**/*"
    ],
    "ios": {
      "supportsTablet": true,
      "bundleIdentifier": "com.mycompany.myapp",
      "infoPlist": {
        "NSCameraUsageDescription": "This app uses the camera to take photos.",
        "NSPhotoLibraryUsageDescription": "This app accesses your photos."
      }
    },
    "android": {
      "package": "com.mycompany.myapp",
      "versionCode": 1,
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#ffffff"
      },
      "permissions": [
        "CAMERA",
        "READ_EXTERNAL_STORAGE",
        "WRITE_EXTERNAL_STORAGE"
      ]
    },
    "plugins": [
      "expo-camera",
      "expo-location"
    ]
  }
}
```

**Benefits:**
- Single source of truth
- JSON or JavaScript (dynamic config)
- No native knowledge required
- Config plugins handle native setup

### React Native CLI: Native Configuration

**Configuration spread across multiple native files:**

**iOS Permissions (`ios/MyApp/Info.plist`):**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>CFBundleDevelopmentRegion</key>
    <string>en</string>
    <key>CFBundleDisplayName</key>
    <string>MyApp</string>
    <key>CFBundleExecutable</key>
    <string>$(EXECUTABLE_NAME)</string>
    <key>CFBundleIdentifier</key>
    <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
    <key>CFBundleInfoDictionaryVersion</key>
    <string>6.0</string>
    <key>CFBundleName</key>
    <string>$(PRODUCT_NAME)</string>
    <key>CFBundlePackageType</key>
    <string>APPL</string>
    <key>CFBundleShortVersionString</key>
    <string>1.0</string>
    <key>CFBundleVersion</key>
    <string>1</string>
    <key>NSCameraUsageDescription</key>
    <string>This app uses the camera to take photos.</string>
    <key>NSPhotoLibraryUsageDescription</key>
    <string>This app accesses your photos.</string>
    <key>UILaunchStoryboardName</key>
    <string>LaunchScreen</string>
    <key>UIRequiredDeviceCapabilities</key>
    <array>
        <string>armv7</string>
    </array>
    <!-- Many more keys... -->
</dict>
</plist>
```

**Android Permissions (`android/app/src/main/AndroidManifest.xml`):**
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

    <application
      android:name=".MainApplication"
      android:label="@string/app_name"
      android:icon="@mipmap/ic_launcher"
      android:roundIcon="@mipmap/ic_launcher_round"
      android:allowBackup="false"
      android:theme="@style/AppTheme">

      <activity
          android:name=".MainActivity"
          android:label="@string/app_name"
          android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|screenSize|smallestScreenSize|uiMode"
          android:launchMode="singleTask"
          android:windowSoftInputMode="adjustResize"
          android:exported="true">
          <intent-filter>
              <action android:name="android.intent.action.MAIN" />
              <category android:name="android.intent.category.LAUNCHER" />
          </intent-filter>
      </activity>
    </application>
</manifest>
```

**Plus:**
- `android/app/build.gradle` - Build configuration, dependencies
- `ios/MyApp.xcodeproj/` - Xcode project settings
- `ios/Podfile` - iOS native dependencies
- Multiple other config files

**Challenges:**
- Must know iOS and Android conventions
- Different formats (XML, Plist, Gradle)
- Easy to make mistakes
- Changes require rebuilding

---

## Adding Native Functionality

### Example: Adding Camera Support

**Expo Approach:**

```bash
# 1. Install the package
npx expo install expo-camera

# 2. Add to app.json plugins (optional, auto-detected)
{
  "expo": {
    "plugins": ["expo-camera"]
  }
}

# 3. Use in code immediately (development)
import { Camera } from 'expo-camera';

function MyCameraComponent() {
  const [permission, requestPermission] = Camera.useCameraPermissions();

  if (!permission) return <Text>Loading...</Text>;
  if (!permission.granted) {
    return <Button title="Grant Permission" onPress={requestPermission} />;
  }

  return <Camera style={{ flex: 1 }} />;
}
```

**That's it!** Permissions are auto-configured when you build with `eas build`.

---

**React Native CLI Approach:**

```bash
# 1. Install package
npm install react-native-vision-camera

# 2. Install iOS dependencies
cd ios
pod install
cd ..

# 3. Configure iOS permissions (ios/MyApp/Info.plist)
# Add manually:
<key>NSCameraUsageDescription</key>
<string>$(PRODUCT_NAME) needs access to your camera.</string>
<key>NSMicrophoneUsageDescription</key>
<string>$(PRODUCT_NAME) needs access to your microphone.</string>

# 4. Configure Android permissions (android/app/src/main/AndroidManifest.xml)
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />

# 5. Configure Android build.gradle (android/app/build.gradle)
# Add to dependencies:
implementation "androidx.camera:camera-camera2:1.1.0"
implementation "androidx.camera:camera-lifecycle:1.1.0"
implementation "androidx.camera:camera-view:1.1.0"

# 6. Rebuild native apps
npm run ios
npm run android

# 7. Use in code
import { Camera } from 'react-native-vision-camera';
```

**Much more manual configuration required.**

---

## Development Workflow

### Expo Development

**Starting development:**
```bash
npm start
```

**Interactive CLI appears:**
```
┌─────────────────────────────────────────────────┐
│                                                 │
│  Metro waiting on exp://192.168.1.100:8081      │
│                                                 │
│  › Press a │ open Android                       │
│  › Press i │ open iOS simulator                 │
│  › Press w │ open web                           │
│                                                 │
│  › Press j │ open debugger                      │
│  › Press r │ reload app                         │
│  › Press m │ toggle menu                        │
│                                                 │
│  › Press ? │ show all commands                  │
│                                                 │
└─────────────────────────────────────────────────┘
```

**Running on physical device:**
1. Install Expo Go app from App Store/Play Store
2. Scan QR code from terminal
3. App loads instantly on your phone

**No USB cable needed!** Works over WiFi.

**Making changes:**
- Edit code
- Save file
- Hot reload updates instantly
- No rebuilding (for JS changes)

### React Native CLI Development

**Starting development:**
```bash
# Terminal 1: Start Metro bundler
npm start

# Terminal 2: Launch iOS (Mac only)
npm run ios

# Or Terminal 2: Launch Android
npm run android
```

**Running on physical device:**
1. Enable Developer Mode on device
2. Connect via USB
3. Configure device in Xcode/Android Studio
4. Run build command
5. Trust certificates/authorize device

**Making changes:**
- Edit code
- Save file
- Hot reload updates instantly (for JS changes)
- Native changes require full rebuild

**First launch time:**
- iOS: 2-5 minutes
- Android: 2-3 minutes

---

## Testing on Devices

### Expo

**Physical Device Testing:**
```bash
# Development build on device
npm start
# Scan QR code with Expo Go app

# Or create development build
eas build --profile development --platform ios
# Install on device via link
```

**Simulator/Emulator:**
```bash
npm start
# Press 'i' for iOS simulator
# Press 'a' for Android emulator
```

**Sharing with testers:**
- Publish to Expo
- Share QR code or link
- Testers use Expo Go app
- No developer account needed

### React Native CLI

**Physical Device Testing:**

**iOS:**
1. Open Xcode
2. Select your device
3. Configure signing certificate (Apple Developer account required - $99/year)
4. Build and run (Product → Run)
5. Trust developer certificate on device

**Android:**
1. Enable USB debugging on device
2. Connect via USB
3. `npm run android`
4. Authorize USB debugging on device

**Simulator/Emulator:**
```bash
npm run ios      # iOS Simulator (Mac only)
npm run android  # Android Emulator
```

**Sharing with testers:**
- TestFlight (iOS) - requires Apple Developer account
- Internal testing (Android) - upload to Play Console
- Ad-hoc distribution (complex)

---

## Building for Production

### Expo: EAS Build (Cloud)

**Setup:**
```bash
# Install EAS CLI
npm install -g eas-cli

# Login to Expo account
eas login

# Configure project
eas build:configure
```

**Build for both platforms (from any OS):**
```bash
# Build iOS and Android
eas build --platform all

# Or build individually
eas build --platform ios
eas build --platform android
```

**What happens:**
1. Code uploaded to Expo's cloud
2. Built on Expo's servers
3. Notifications when complete (~10-20 min)
4. Download `.ipa` (iOS) and `.aab` (Android)

**No Mac required for iOS builds!** You can build iOS apps from Windows/Linux.

**Automatic submission:**
```bash
# Submit to App Store
eas submit --platform ios

# Submit to Google Play
eas submit --platform android
```

**Cost:**
- Free tier: 30 builds/month (15 iOS, 15 Android)
- Paid plans for more builds

### React Native CLI: Local Build

**iOS Build (requires Mac + Xcode):**

```bash
# 1. Open Xcode
cd ios
open MyApp.xcworkspace

# 2. In Xcode:
# - Select "Any iOS Device" as target
# - Product → Archive
# - Wait 10-30 minutes for build
# - Validate archive
# - Distribute to App Store
# - Upload

# Or command line with fastlane (advanced):
fastlane ios release
```

**Requirements:**
- Mac with Xcode
- Apple Developer account ($99/year)
- Certificates and provisioning profiles configured
- Time: 10-30 minutes per build

**Android Build:**

```bash
cd android

# 1. Generate signing key (first time only)
keytool -genkeypair -v -storetype PKCS12 -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000

# 2. Configure signing in android/app/build.gradle
# Add keystore credentials

# 3. Build release
./gradlew bundleRelease

# Output: android/app/build/outputs/bundle/release/app-release.aab
```

**Requirements:**
- Android SDK
- Keystore configured
- Time: 5-15 minutes per build

**Submission:**
- Manual upload to App Store Connect (iOS)
- Manual upload to Google Play Console (Android)
- Or use fastlane for automation

---

## Over-the-Air (OTA) Updates

### Expo: Built-in EAS Update

```bash
# Push update to live apps
eas update --branch production --message "Fix critical bug"

# Users receive update in seconds/minutes
# No app store approval needed
# Works for JavaScript changes only
```

**How it works:**
- Users open app
- App checks for updates
- Downloads new JS bundle in background
- Applies on next restart

**Limitations:**
- JavaScript/assets only
- Native code changes require new build

**Cost:** Free for up to 1,000 active users/month

### React Native CLI: Manual Setup Required

**Options:**

**1. Microsoft CodePush (deprecated in 2024):**
- Was the go-to solution
- Now deprecated, not recommended for new projects

**2. expo-updates (can be used in bare React Native):**
```bash
npm install expo-updates
# Configure native setup manually
```

**3. Custom solution:**
- Build your own update server
- Implement download and apply logic
- Complex and error-prone

**4. No OTA updates:**
- Release new version to app stores
- Wait 1-7 days for review
- Users must manually update

**Reality:** Most React Native CLI apps don't have OTA updates and rely on app store releases.

---

## App Size Comparison

### Expo App Size

**Managed Expo:**
- iOS: ~40-60 MB (includes Expo Go runtime)
- Android: ~30-50 MB (includes Expo Go runtime)

**Expo with Custom Development Build:**
- iOS: ~15-30 MB (only includes what you use)
- Android: ~10-25 MB (only includes what you use)

**Note:** Modern Expo apps can be similar in size to React Native CLI apps when using custom development builds.

### React Native CLI App Size

**Bare React Native:**
- iOS: ~10-20 MB (minimal app)
- Android: ~8-15 MB (minimal app)

**With dependencies:**
- Grows based on what you add
- Can be larger or smaller than Expo depending on libraries

**Size difference is no longer a major factor in 2025** - Expo has closed the gap significantly.

---

## Native Modules & Third-Party Libraries

### Expo Approach

**Expo SDK modules (50+ pre-built):**
```bash
npx expo install expo-camera
npx expo install expo-location
npx expo install expo-notifications
npx expo install expo-file-system
# All have simple APIs and auto-configuration
```

**Third-party libraries:**

**If it supports Expo config plugins:**
```bash
npm install react-native-third-party
# Add to app.json plugins
{
  "plugins": ["react-native-third-party"]
}
```

**If it doesn't support Expo:**
```bash
# Use prebuild (creates ios/ and android/ folders)
npx expo prebuild
# Now you have access to native code
```

**Expo can use almost any React Native library** - the "can't use native modules" myth is outdated.

### React Native CLI Approach

**All libraries require manual native setup:**
```bash
npm install react-native-library
cd ios && pod install && cd ..
# Edit native files
# Rebuild apps
```

**More flexibility, more manual work.**

---

## Debugging

### Expo Debugging

**Built-in tools:**
```bash
npm start
# Press 'j' to open debugger
```

**React DevTools:**
```bash
npx react-devtools
```

**Network debugging:**
- Built into Expo Dev Tools
- See all network requests

**Native logs:**
```bash
npx expo run:ios    # See native iOS logs
npx expo run:android # See native Android logs
```

**Flipper (optional):**
- Can use Flipper with Expo development builds

### React Native CLI Debugging

**Chrome DevTools (legacy):**
```bash
# Shake device → "Debug" → Opens Chrome
```

**Flipper (recommended):**
```bash
# Install and configure Flipper
# Provides network inspector, layout inspector, logs
```

**Native debugging:**
- Xcode debugger (iOS)
- Android Studio debugger (Android)
- Direct access to native logs

**More powerful native debugging, steeper learning curve.**

---

## Common Tasks Comparison

| Task | Expo | React Native CLI |
|------|------|------------------|
| **Create project** | `npx create-expo-app` | `npx react-native init` + native setup |
| **Run on iOS** | `npm start` → press `i` | `npm run ios` (Mac only) |
| **Run on Android** | `npm start` → press `a` | `npm run android` |
| **Add camera** | `npx expo install expo-camera` | Install + manual native config |
| **Change app icon** | Replace `assets/icon.png` | Replace images in `ios/` and `android/` |
| **Configure permissions** | Edit `app.json` | Edit Info.plist + AndroidManifest.xml |
| **Build for iOS** | `eas build -p ios` (any OS) | Xcode Archive (Mac only) |
| **Build for Android** | `eas build -p android` | `./gradlew bundleRelease` |
| **Update live app** | `eas update` | Rebuild and resubmit to stores |
| **Share with testers** | Share QR code/link | TestFlight or APK distribution |

---

## Cost Comparison

### Expo Costs

**Free tier includes:**
- Unlimited development
- 30 builds/month (cloud)
- EAS Update for 1,000 users
- Basic support

**Paid plans (as of 2025):**
- **Production Plan**: ~$99/month (more builds, priority queue)
- **Enterprise**: Custom pricing

**You can avoid costs by:**
- Using local builds (`eas build --local`)
- Staying within free tier limits
- Using Expo without EAS services

### React Native CLI Costs

**Direct costs:**
- Apple Developer Program: $99/year (required for iOS)
- Google Play Developer: $25 one-time (required for Android)

**Infrastructure costs (optional):**
- CI/CD services (GitHub Actions, CircleCI, etc.)
- Fastlane automation
- CodePush alternatives
- Crash reporting services
- Analytics services

**Time is money:**
- More developer time for setup and maintenance
- Native expertise may require hiring specialists

---

## Migration Paths

### From Expo to React Native CLI (Prebuild)

```bash
# Generate native folders
npx expo prebuild

# Now you have ios/ and android/ folders
# Still can use Expo modules and services
# Full access to native code
```

**This is called "Bare Workflow" or "Prebuild" and is the recommended approach if you need native access.**

### From React Native CLI to Expo

```bash
# Install Expo modules
npx install-expo-modules

# Add Expo configuration
# Gradually adopt Expo modules
```

**Possible but less common - usually done piece by piece.**

---

## Platform-Specific Features

### Expo Platform Support

**Supported platforms:**
- ✅ iOS
- ✅ Android
- ✅ Web (with Expo for Web)

**Some Expo packages work on web too!**

```bash
# Create universal app
npx create-expo-app --template
npm run web  # Runs in browser!
```

### React Native CLI Platform Support

**Supported platforms:**
- ✅ iOS
- ✅ Android
- ⚠️ Web (requires react-native-web setup - manual)
- ⚠️ Windows (community-driven)
- ⚠️ macOS (community-driven)

**Focus is primarily on iOS and Android.**

---

## Learning Curve

### Expo Learning Path

1. **Week 1:** Learn React Native basics with Expo
2. **Week 2-3:** Build simple apps, use Expo modules
3. **Month 2:** Understand app.json configuration
4. **Month 3:** Learn EAS Build and deployment
5. **Advanced:** Understand when to use prebuild

**Progression:** JavaScript → React Native → Expo ecosystem

**Prerequisite knowledge:**
- React
- JavaScript/TypeScript
- Basic mobile concepts

### React Native CLI Learning Path

1. **Week 1:** Setup native development environment
2. **Week 2:** Learn React Native basics
3. **Week 3-4:** Understand native project structure
4. **Month 2:** Learn iOS and Android configuration
5. **Month 3:** Understand build systems (Xcode, Gradle)
6. **Month 4:** Learn native module linking
7. **Advanced:** Write native modules in Swift/Kotlin

**Progression:** Native development → React Native → Integration

**Prerequisite knowledge:**
- React
- JavaScript/TypeScript
- iOS development basics (Xcode, CocoaPods)
- Android development basics (Android Studio, Gradle)
- Mobile app concepts

**Steeper learning curve, requires native platform knowledge.**

---

## Team Considerations

### Expo for Teams

**Advantages:**
- Consistent development environment
- Less platform-specific knowledge required
- Faster onboarding for JavaScript developers
- Shared configuration in version control
- Cloud builds reduce "works on my machine" issues

**Best for:**
- Small teams (1-5 developers)
- Full-stack JavaScript teams
- Startups moving fast
- Teams without native developers

### React Native CLI for Teams

**Advantages:**
- Native developers can work in familiar tools
- Full control over build process
- Easier to integrate with existing CI/CD
- Can optimize for specific use cases

**Best for:**
- Teams with native iOS/Android developers
- Large organizations with native expertise
- Apps requiring heavy native customization
- Teams building platform-specific features

---

## Common Misconceptions

### About Expo

❌ **"Expo apps are slower"**
- Modern Expo apps perform identically to React Native CLI apps
- Both use the same React Native core

❌ **"You can't use native modules with Expo"**
- You can use prebuild or development builds
- Most libraries work with Expo via config plugins

❌ **"Expo apps are huge"**
- Custom development builds are similar size to bare RN
- Only Expo Go app is large (it's a development tool)

❌ **"Expo is for beginners only"**
- Many production apps use Expo (including large companies)
- Expo is professional-grade

### About React Native CLI

❌ **"React Native CLI is always faster"**
- Build times can be longer due to native compilation
- Hot reload is similar between both

❌ **"You have more control"**
- True for native code
- But Expo config plugins provide declarative control

❌ **"React Native CLI is harder to learn"**
- True, but necessary if you need native expertise

---

## Real-World Examples

### Apps Built with Expo

- **Pillar Valley** - Popular mobile game
- **Brex** - Fintech startup
- **Plentix** - Healthcare app
- **Many startups and indie apps**

### Apps Built with React Native (may use either)

- **Discord** - Chat app
- **Shopify** - E-commerce
- **Microsoft Office** - Productivity suite
- **Facebook/Instagram** (parts) - Social media

**Note:** Many large apps use a hybrid approach or custom build systems.

---

## Recommendations by Use Case

### Use Expo for:

✅ **MVP/Prototypes**
- Fast iteration needed
- Testing ideas quickly

✅ **Standard Apps**
- Social apps
- E-commerce
- Content apps
- Most CRUD apps

✅ **Solo Developers**
- Don't want to manage native code
- Focus on JavaScript

✅ **Cross-Platform Web + Mobile**
- Want to share code with web
- Universal apps

### Use React Native CLI for:

✅ **Heavy Native Integration**
- Bluetooth Low Energy
- Complex camera features
- Custom video processing
- Hardware integrations

✅ **Existing Native Apps**
- Adding React Native to existing iOS/Android app
- Brownfield projects

✅ **Minimal Size Requirements**
- Every MB matters
- Highly optimized builds

✅ **Native Development Teams**
- Team comfortable with Xcode/Android Studio
- Want full native control

### Use Expo + Prebuild for:

✅ **Starting Simple, Growing Complex**
- Begin with Expo simplicity
- Add native code as needed
- Best of both worlds

---

## The Verdict (2025)

**For most developers starting a new React Native project in 2025: Use Expo.**

**Why:**
- Faster development
- Better developer experience
- Easier maintenance
- Can always add native code later via prebuild
- The ecosystem has matured significantly
- Most limitations have been resolved

**React Native CLI still makes sense for:**
- Apps with immediate custom native requirements
- Teams with strong native expertise
- Integration into existing native apps
- Specific edge cases requiring full native control

---

## Next Steps

### If choosing Expo:
1. Follow the [official Expo tutorial](https://docs.expo.dev/tutorial/introduction/)
2. Learn about [EAS Build](https://docs.expo.dev/build/introduction/)
3. Explore [Expo SDK](https://docs.expo.dev/versions/latest/)
4. Join [Expo Discord community](https://chat.expo.dev/)

### If choosing React Native CLI:
1. Follow the [React Native setup guide](https://reactnative.dev/docs/environment-setup)
2. Learn native development basics (iOS and Android)
3. Understand [native modules](https://reactnative.dev/docs/native-modules-intro)
4. Set up build automation with [Fastlane](https://fastlane.tools/)

### Further Reading

- [Expo Documentation](https://docs.expo.dev/)
- [React Native Documentation](https://reactnative.dev/)
- [Expo vs React Native CLI (Official Comparison)](https://docs.expo.dev/faq/)
- [React Native Directory](https://reactnative.directory/) - Find compatible libraries

---

**Remember:** You can always switch approaches later. Start with what makes sense for your current needs and team expertise.
