# 🚀 Debug APK Build Guide - ChatWave App

## ✅ Quick Start (3 आसान स्टेप्स)

### Step 1: Install Dependencies
```bash
npm install
```

### Step 2: Build Debug APK
```bash
npm run android:build
```

### Step 3: Install on Device
```bash
adb install -r android/app/build/outputs/apk/debug/app-debug.apk
```

---

## 📋 Prerequisites (जरूरी चीजें)

पहले ये सब install करना होगा:

### Linux/macOS:
```bash
# 1. Java Development Kit (JDK 17)
brew install openjdk@17

# 2. Android SDK
# Download Android Studio from: https://developer.android.com/studio
# Or using homebrew
brew install android-sdk

# 3. Set ANDROID_HOME
echo 'export ANDROID_HOME=$HOME/Library/Android/sdk' >> ~/.zshrc
echo 'export PATH=$PATH:$ANDROID_HOME/emulator' >> ~/.zshrc
echo 'export PATH=$PATH:$ANDROID_HOME/tools' >> ~/.zshrc
echo 'export PATH=$PATH:$ANDROID_HOME/tools/bin' >> ~/.zshrc
echo 'export PATH=$PATH:$ANDROID_HOME/platform-tools' >> ~/.zshrc
source ~/.zshrc
```

### Windows:
```cmd
# Install Chocolatey first (Run as Administrator)
powershell -Command "iex ((New-Object System.Net.ServicePointManager).SecurityProtocol = 3072; iex (New-Object Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))"

# Then install dependencies
choco install openjdk17
choco install android-sdk

# Set ANDROID_HOME
setx ANDROID_HOME "C:\Users\YourUsername\AppData\Local\Android\Sdk"
```

---

## 🔨 Detailed Build Commands

### Option 1: Using npm script (Easiest)
```bash
npm run android:build
```

### Option 2: Using Gradle directly
```bash
cd android
./gradlew assembleDebug    # macOS/Linux
# or
gradlew.bat assembleDebug  # Windows
cd ..
```

### Option 3: Using Android Studio
1. Open Android Studio
2. File → Open → Select `android` folder
3. Click Build → Build App Bundles/APK → Build APK(s)
4. APK location: `android/app/build/outputs/apk/debug/app-debug.apk`

---

## 📱 Install & Run on Device

### Prerequisites:
- Connect Android device via USB
- Enable USB Debugging on device
- Or start Android emulator

### Install:
```bash
# Check connected devices
adb devices

# Install APK
adb install -r android/app/build/outputs/apk/debug/app-debug.apk

# Launch app
adb shell am start -n com.chatwave.app/.MainActivity

# View logs
adb logcat | grep "ChatWave"
```

---

## 🐛 Troubleshooting

### Problem: `ANDROID_HOME not found`
```bash
echo $ANDROID_HOME
# If empty, set it:
export ANDROID_HOME=$HOME/Library/Android/sdk  # macOS
# or
export ANDROID_HOME=$HOME/Android/Sdk          # Linux
```

### Problem: Permission denied on gradlew
```bash
chmod +x android/gradlew
```

### Problem: Out of memory during build
Edit `android/gradle.properties`:
```properties
org.gradle.jvmargs=-Xmx4096m -XX:MaxPermSize=1024m
```

### Problem: Device not showing in `adb devices`
```bash
# Restart ADB
adb kill-server
adb start-server

# Reconnect device and enable USB Debugging
```

---

## 📁 Project Structure

```
chatwave-app/
├── android/               # Android native code
│   ├── app/
│   │   ├── build/
│   │   ├── src/
│   │   ├── build.gradle
│   │   └── proguard-rules.pro
│   ├── build.gradle
│   └── gradle.properties
├── App.js                 # Main React Native component
├── index.js              # Entry point
├── package.json          # NPM dependencies
├── app.json             # App configuration
└── README.md            # Main documentation
```

---

## 🚀 CI/CD (Automatic Builds)

GitHub Actions automatically builds debug APK on:
- Push to `main` / `develop`
- Pull requests
- Manual workflow dispatch

Check **Actions** tab for build artifacts.

---

## 💡 Development Tips

```bash
# Start Metro bundler (in separate terminal)
npm start

# Build and test
npm run android:build

# Clean and rebuild
cd android && ./gradlew clean && cd ..
npm run android:build

# Update dependencies
npm update

# Check React Native version
npm list react-native
```

---

## 📞 Support

- [React Native Docs](https://reactnative.dev/)
- [Android Developer Guide](https://developer.android.com/docs)
- [GitHub Issues](https://github.com/upscias1351-dev/chatwave-app/issues)

---

## ✨ Next Steps

1. ✅ Debug APK built successfully!
2. 📱 Install on device
3. 🧪 Test the app
4. 🔧 Make changes to `App.js`
5. 🔄 Rebuild when ready

Happy Coding! 🎉
