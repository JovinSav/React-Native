# Releasing an Android APK

A step-by-step guide to generate and sign a production APK for your React Native Android app.

---

## 1. Prerequisites

- JDK 11+ installed and `JAVA_HOME` set  
- Android Studio with SDK & Platform tools  
- A **release keystore** (see next step)

---

## 2. Generate a Signing Key (Skip if you already have one)

If you already have a release keystore, skip this step and proceed to [Configure Gradle for Signing](#3-configure-gradle-for-signing).

In a terminal, run:

```bash
keytool -genkey -v \
  -keystore myapp-release-key.jks \
  -alias myappkey \
  -keyalg RSA -keysize 2048 \
  -validity 10000
```

## 3. Configure Gradle for Signing

1. Copy your `myapp-release-key.jks` into `android/app/`.  
2. In `android/gradle.properties`, add:
   ```properties
   MYAPP_RELEASE_STORE_FILE=myapp-release-key.jks
   MYAPP_RELEASE_KEY_ALIAS=myappkey
   MYAPP_RELEASE_STORE_PASSWORD=your_keystore_password
   MYAPP_RELEASE_KEY_PASSWORD=your_key_password
   ```
3. In `android/app/build.gradle`, under `android { … }`, update:
   ```groovy
   signingConfigs {
       release {
           storeFile file(MYAPP_RELEASE_STORE_FILE)
           storePassword MYAPP_RELEASE_STORE_PASSWORD
           keyAlias MYAPP_RELEASE_KEY_ALIAS
           keyPassword MYAPP_RELEASE_KEY_PASSWORD
       }
   }
   buildTypes {
       release {
           signingConfig signingConfigs.release
           minifyEnabled true          // enable ProGuard/R8
           shrinkResources true        // remove unused resources
           proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
       }
   }
   ```

## 3.1 Optional: Build an Unsigned Release APK (Skip Signing)

If you don’t have a signing key and don’t need to sign (e.g., for local or internal testing), generate an unsigned release APK:

```bash
cd android
./gradlew assembleRelease -x signRelease
```

The unsigned APK will be at:
`android/app/build/outputs/apk/release/app-release-unsigned.apk`

> Note: unsigned APKs cannot be published to the Play Store.

## 4. Build the Release APK or AAB

Open a terminal in your project’s `android/` folder and run:

```bash
# APK
./gradlew assembleRelease

# or AAB (recommended for Play Store)
./gradlew bundleRelease
```

The generated artifact will be in:
- APK: `android/app/build/outputs/apk/release/app-release.apk`
- AAB: `android/app/build/outputs/bundle/release/app-release.aab`

## 5. Test the Release Build

Install and test on a device or emulator:

```bash
adb install -r android/app/build/outputs/apk/release/app-release.apk
# or if using AAB, use bundletool to convert to APK(s) first
```

Ensure all features and assets load correctly in production mode.

## 6. Prepare for Play Store

1. Create a Play Store listing and upload your APK/AAB.  
2. Fill in app details, screenshots, release notes and version codes.  
3. Roll out to internal, closed or production tracks as needed.

## 7. Versioning & Updates

- Bump `versionCode` and `versionName` in `android/app/build.gradle` before each release.  
- Use semantic versioning (e.g., `1.0.1`, `1.1.0`).  

---

You now have a complete end-to-end process for generating, signing and publishing a React Native Android release build.