# Testing on a Physical Device

Follow these steps to run your React Native app on a real Android or iOS device instead of an emulator/simulator.

---

## 1. Android

1. Enable USB debugging on your phone:
   - Settings → About phone → Tap “Build number” 7 times  
   - Settings → Developer options → Enable “USB debugging”
2. Connect device via USB and trust the computer.
3. Verify connection:
   ```bash
   adb devices
   # lists your device ID
   ```
4. Run the app on your device:
   ```bash
   npx react-native run-android --deviceId <your_device_id>
   ```
   Or simply:
   ```bash
   npx react-native run-android
   ```
   if only one device/emulator is connected.

---

## 2. iOS (macOS only)

1. On the device, go to Settings → Developer → Enable UI Automation (if available).
2. Connect your iPhone/iPad via USB and tap “Trust” on the device.
3. Install pods (if not done):
   ```bash
   cd ios && pod install && cd ..
   ```
4. Open the Xcode workspace:
   ```bash
   open ios/MyApp.xcworkspace
   ```
5. In Xcode:
   - Select your physical device from the target dropdown.
   - Click the Run ▶︎ button.

---

## 3. Troubleshooting

- Android:
  - If `adb devices` shows “unauthorized”, re-plug and accept trust prompt.
  - Make sure `minSdkVersion` in `android/app/build.gradle` ≤ your device’s API level.
- iOS:
  - Ensure a valid development team is selected in Xcode → Signing & Capabilities.
  - If you hit code signing issues, run `npx pod-install` and restart Xcode.

---

## 4. Next Steps

- Profile your app on-device using `adb logcat` (Android) or Xcode’s Console (iOS).  
- Use Flipper or React DevTools for on-device debugging.  
- Explore live reloading & performance monitors directly on your device.
