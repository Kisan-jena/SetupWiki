# React Native Setup Guide with Expo (Windows)

This guide will walk you through setting up React Native development environment on Windows using Expo, including Android Emulator setup and Expo Go mobile app integration.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation Steps](#installation-steps)
- [Android Emulator Setup](#android-emulator-setup)
- [Creating Your First App](#creating-your-first-app)
- [Running Your App](#running-your-app)
- [Using Expo Go on Physical Device](#using-expo-go-on-physical-device)
- [Troubleshooting](#troubleshooting)

---

## Prerequisites

Before starting, ensure you have:
- Windows 10/11 (64-bit)
- At least 8GB RAM (16GB recommended)
- 20GB free disk space
- Administrator access to your computer

---

## Installation Steps

### 1. Install Node.js

1. Download Node.js LTS version from [nodejs.org](https://nodejs.org/)
2. Run the installer and follow the installation wizard
3. Verify installation:
   ```powershell
   node --version
   npm --version
   ```

### 2. Install Git (Optional but Recommended)

1. Download Git from [git-scm.com](https://git-scm.com/)
2. Install with default settings
3. Verify:
   ```powershell
   git --version
   ```

### 3. Install Expo CLI

Expo CLI is installed globally via npm:

```powershell
npm install -g expo-cli
```

Verify installation:
```powershell
npx expo --version
```

---

## Android Emulator Setup

### 1. Install Android Studio

1. Download Android Studio from [developer.android.com](https://developer.android.com/studio)
2. Run the installer and choose "Standard" installation
3. During installation, make sure the following are selected:
   - Android SDK
   - Android SDK Platform
   - Android Virtual Device (AVD)

### 2. Configure Android SDK

1. Open Android Studio
2. Go to **Settings/Preferences** → **Appearance & Behavior** → **System Settings** → **Android SDK**
3. Select the **SDK Platforms** tab
4. Check the box for the latest Android version (e.g., Android 14.0 "UpsideDownCake")
5. Select the **SDK Tools** tab and ensure the following are installed:
   - Android SDK Build-Tools
   - Android Emulator
   - Android SDK Platform-Tools
   - Google Play services
6. Click **Apply** to install

### 3. Set Environment Variables

Add Android SDK to your system environment variables:

1. Open **System Properties** → **Advanced** → **Environment Variables**
2. Under **User variables**, click **New** and add:
   - Variable name: `ANDROID_HOME`
   - Variable value: `C:\Users\YourUsername\AppData\Local\Android\Sdk`

3. Edit the **Path** variable and add:
   ```
   `C:\Users\YourUsername\AppData\Local\Android\Sdk\platform-tools`
   ```

4. Click **OK** to save

5. **Restart your terminal** or computer for changes to take effect

6. Verify installation:
   ```powershell
   adb --version
   ```

### 4. Create an Android Virtual Device (AVD)

1. Open Android Studio
2. Click on **More Actions** → **Virtual Device Manager**
3. Click **Create Virtual Device**
4. Select a device definition (e.g., Pixel 7 Pro)
5. Click **Next**
6. Download and select a system image (e.g., API Level 34 - Android 14.0)
7. Click **Next**, then **Finish**
8. Your emulator is now ready!

### 5. Test the Emulator

Launch the emulator from Android Studio or via command line:

```powershell
emulator -avd Your_AVD_Name
```

Or list available AVDs:
```powershell
emulator -list-avds
```

---

## Creating Your First App

### 1. Create a New Expo Project

```powershell
npx create-expo-app@latest MyFirstApp
```

Select a template when prompted:
- **Blank** - A minimal app with just the essentials
- **Blank (TypeScript)** - Same as blank but with TypeScript
- **Navigation (Expo Router)** - Pre-configured with expo-router

### 2. Navigate to Your Project

```powershell
cd MyFirstApp
```

### 3. Project Structure

```
MyFirstApp/
├── app/                  # App screens (if using Expo Router)
│   ├── (tabs)/          # Tab navigation screens
│   ├── _layout.tsx      # Root layout
│   └── index.tsx        # Home screen
├── assets/              # Images, fonts, and other assets
├── components/          # Reusable components
├── constants/           # App constants and theme
├── hooks/               # Custom React hooks
├── app.json            # Expo configuration
├── package.json        # Dependencies and scripts
└── tsconfig.json       # TypeScript configuration
```

---

## Running Your App

### Option 1: Using Android Emulator

1. **Start the emulator** (if not already running):
   - Open Android Studio → Virtual Device Manager → Launch your AVD
   - Or via command line: `emulator -avd Your_AVD_Name`

2. **Start the Expo development server**:
   ```powershell
   npm start
   ```

3. **Launch on Android**:
   - Press `a` in the terminal, or
   - Run: `npm run android`

The app will build and open in the Android emulator automatically.

### Option 2: Using Expo Go on Physical Device

See the next section for detailed instructions.

### Development Server Commands

When running `npm start`, you'll see several options:
- **a** - Open on Android emulator
- **w** - Open in web browser
- **r** - Reload app
- **m** - Toggle menu
- **?** - Show all commands

---

## Using Expo Go on Physical Device

Expo Go allows you to run your app on a real device without building a native binary.

### 1. Install Expo Go

- **Android**: Download from [Google Play Store](https://play.google.com/store/apps/details?id=host.exp.exponent)
- **iOS**: Download from [App Store](https://apps.apple.com/app/expo-go/id982107779)

### 2. Connect to the Same Network

Ensure your computer and mobile device are on the **same Wi-Fi network**.

### 3. Start Development Server

```powershell
npm start
```

### 4. Scan QR Code

A QR code will appear in the terminal.

**On Android:**
- Open the Expo Go app
- Tap **Scan QR Code**
- Point your camera at the QR code

**On iOS:**
- Open the Camera app
- Point at the QR code
- Tap the notification banner

Your app will load on your device!

### 5. Live Reload

Any changes you make to your code will automatically reload on your device.

---

## Troubleshooting

### Emulator Issues

**Problem**: Emulator won't start
- Solution: Check if Hyper-V is enabled (Settings → Apps → Optional Features → More Windows Features → Hyper-V)
- Alternative: Use HAXM (Intel Hardware Accelerated Execution Manager)

**Problem**: ADB not recognized
- Solution: Verify `ANDROID_HOME` environment variable is set correctly
- Restart your terminal/computer after setting environment variables

**Problem**: Emulator is very slow
- Solution: Allocate more RAM to the AVD (Edit AVD → Show Advanced Settings → RAM)
- Enable hardware acceleration in BIOS

### Expo Go Issues

**Problem**: Can't connect to development server
- Solution 1: Ensure both devices are on the same network
- Solution 2: Try using tunnel mode: `npm start -- --tunnel`
- Solution 3: Disable firewall temporarily to test connection

**Problem**: "Something went wrong" in Expo Go
- Solution: Clear Expo Go cache (Settings → Clear Cache)
- Restart the development server with: `npm start --clear`

### Build Issues

**Problem**: `npm start` fails with exit code 1
- Solution: Delete `node_modules` and reinstall:
  ```powershell
  Remove-Item -Recurse -Force node_modules
  npm install
  ```

**Problem**: Metro bundler errors
- Solution: Clear Metro cache:
  ```powershell
  npx expo start --clear
  ```

### General Tips

- Always restart the development server after installing new packages
- Use `npx expo doctor` to check for common issues
- Keep Expo CLI and dependencies updated:
  ```powershell
  npm install expo@latest
  npx expo install --fix
  ```

---

## Useful Commands

```powershell
# Start development server
npm start

# Start with cleared cache
npm start --clear

# Run on Android emulator
npm run android

# Run on iOS simulator (macOS only)
npm run ios

# Run in web browser
npm run web

# Check for issues
npx expo doctor

# Update dependencies
npx expo install --fix

# Build APK for testing
eas build --platform android --profile preview
```

---

## Additional Resources

- [Expo Documentation](https://docs.expo.dev/)
- [React Native Documentation](https://reactnative.dev/)
- [Android Developer Guides](https://developer.android.com/)
- [Expo Forums](https://forums.expo.dev/)

---

## Next Steps

1. Explore the default project structure
2. Modify `app/index.tsx` to customize your home screen
3. Add new screens in the `app/` directory
4. Install additional packages as needed:
   ```powershell
   npx expo install package-name
   ```
5. Learn about Expo Router for navigation
6. Build your first feature!

---

**Happy Coding! 🚀 , OPEN TO ACCEPT VALUEABLE CHANGE**

---

*Last Updated: November 25, 2025*
