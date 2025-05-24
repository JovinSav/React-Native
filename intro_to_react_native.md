# Introduction to React Native (without Expo)

React Native lets you build mobile apps using JavaScript and React. This guide walks you through setting up and running a new project without Expo.

---

## 1. Prerequisites

- **Node.js** (>=14.x): https://nodejs.org  
- **Yarn** (optional): `npm install -g yarn`  
- **Java JDK** (>=11) for Android: https://adoptopenjdk.net  
- **Android Studio** with SDK & AVD  
- **Xcode** (macOS only) for iOS Simulator

---

## 2. Install React Native CLI

```bash
npm install -g react-native-cli
```
if issues just uninstall react native cli
```bash
npm uninstall -g react-native-cli @react-native-community/cli
```
and use
```bash
npx @react-native-community/cli@latest init AwesomeProject
```

(or with Yarn)

```bash
yarn global add react-native-cli
```

---

## 3. Create a New Project

```bash
npx react-native init MyApp
cd MyApp
```

This generates the `android/` and `ios/` native folders and a basic JS entry point.

---

## 4. Project Structure

```bash
MyApp/
├── android/           # Android native project
│   ├── app/           # Your app module
│   └── build.gradle   # Gradle config
├── ios/               # iOS native project
│   ├── MyApp/         # Xcode project folder
│   └── Podfile        # CocoaPods config
├── __tests__/         # Jest tests
├── App.js             # Main React component
├── index.js           # Entry point
├── node_modules/      # Installed packages
├── package.json       # Project metadata & scripts
└── yarn.lock / package-lock.json  # Locked dependency versions
```

---

## 5. Running on Android

1. Start an Android emulator in Android Studio (AVD).  
2. In your project root:

   ```bash
   npx react-native run-android
   ```

---

## 6. Running on iOS (macOS)

1. Open the project in Xcode:  
   ```bash
   open ios/MyApp.xcworkspace
   ```  
2. Hit “Run” or from CLI:

   ```bash
   npx react-native run-ios
   ```

---

## 7. Your First Component

Edit `App.js`:

```jsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Hello, React Native!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: 'center', alignItems: 'center' },
  title: { fontSize: 24, fontWeight: 'bold' },
});
```

---

## 8. Installing Libraries

To add third-party packages, use npm or Yarn. For example, to install React Navigation:

```bash
# React Navigation core
npm install @react-navigation/native

# required dependencies
npm install react-native-screens react-native-safe-area-context

# native stack navigator
npm install @react-navigation/native-stack

# iOS Pods install
cd ios && pod install && cd ..

# Or with Yarn:
yarn add @react-navigation/native \
  react-native-screens react-native-safe-area-context \
  @react-navigation/native-stack
```

Feel free to install other libraries (e.g., `react-native-vector-icons`) in the same way.

---

## 9. Styling

- Use `StyleSheet.create({})`.  
- Flexbox layout by default.  
- No CSS file; all styles in JS.

---

## 10. Debugging & Live Reload

- Shake device/emulator to open the dev menu.  
- Enable “Live Reload” or “Fast Refresh”.  
- Use Chrome DevTools (`Debug in Chrome`).

---

## 11. Next Steps

- Explore core components: ScrollView, FlatList, TextInput, etc.  
- State management: Context API, Redux, Recoil.  
- Navigation: React Navigation.  
- Native modules if you need custom native code.

---

## Resources

- Official docs: https://reactnative.dev  
- React Native CLI Quickstart: https://reactnative.dev/docs/environment-setup  
- Community tutorials on YouTube and blogs
