# 🔬 ScienceWiz — Class 9 & 10 CBSE Science App

A complete Flutter app with 5 science modules for Indian CBSE students.
**100% offline. No database. No backend.**

---

## 📱 Modules Included
1. **Periodic Table Explorer** — 30 elements with properties, uses, fun facts
2. **Physics Formula Sheet** — NCERT Class 9 & 10, chapter-wise with examples
3. **Chemical Equation Balancer** — 15 NCERT equations with step-by-step working
4. **Human Body Systems** — 6 systems, detailed organ notes
5. **Science Experiment Guide** — 10 NCERT practicals with full procedure

---

## 🛠️ HOW TO BUILD THE APK / AAB

### Prerequisites (install these once)
| Tool | Download |
|------|---------|
| Flutter SDK | https://flutter.dev/docs/get-started/install |
| Android Studio | https://developer.android.com/studio |
| Java JDK 11+ | Included with Android Studio |

---

### STEP 1 — Install Flutter
```bash
# Download Flutter SDK from https://flutter.dev
# Add flutter/bin to your PATH

# Verify installation
flutter doctor
# All items should show ✓ (green checkmarks)
```

---

### STEP 2 — Open the Project
```bash
# Navigate to the project folder
cd sciencewiz

# Get all dependencies
flutter pub get

# Check for any issues
flutter analyze
```

---

### STEP 3 — Test on Emulator (optional but recommended)
```bash
# Start Android emulator from Android Studio, then:
flutter run

# The app should launch on the emulator
# Test all 5 modules before building release
```

---

### STEP 4 — Create a Signing Keystore (ONE TIME ONLY)
```bash
# This creates your unique signing certificate
# KEEP THIS FILE SAFE — you need it for every update forever!

keytool -genkey -v \
  -keystore sciencewiz-release.jks \
  -keyalg RSA \
  -keysize 2048 \
  -validity 10000 \
  -alias sciencewiz

# You will be asked:
# - Keystore password (remember this!)
# - Key password (can be same as keystore)
# - Your name, organisation, city, state, country
```

---

### STEP 5 — Configure Signing
```bash
# Copy the template
cp android/key.properties.template android/key.properties

# Edit android/key.properties with your passwords:
# storePassword=your_keystore_password
# keyPassword=your_key_password
# keyAlias=sciencewiz
# storeFile=../sciencewiz-release.jks

# IMPORTANT: Move sciencewiz-release.jks to the android/ folder
# or update storeFile path accordingly
```

---

### STEP 6 — Build Release AAB (for Play Store)
```bash
# Build App Bundle (AAB) — recommended for Play Store
flutter build appbundle --release

# Output file location:
# build/app/outputs/bundle/release/app-release.aab
```

```bash
# OR build APK (for direct installation / testing)
flutter build apk --release --split-per-abi

# Output files:
# build/app/outputs/flutter-apk/app-armeabi-v7a-release.apk  (older phones)
# build/app/outputs/flutter-apk/app-arm64-v8a-release.apk    (modern phones)
# build/app/outputs/flutter-apk/app-x86_64-release.apk       (emulators)
```

---

### STEP 7 — Upload to Google Play Store

#### First, create a developer account:
1. Go to https://play.google.com/console
2. Pay one-time fee of **$25 USD**
3. Complete identity verification

#### Create your app listing:
1. Click **"Create app"**
2. Fill in app name: **ScienceWiz — Class 9 & 10 Science**
3. Select **Free**, **Education** category
4. Select **India** as primary country (can add more)

#### Upload your build:
1. Go to **Production → Create new release**
2. Upload your `app-release.aab` file
3. Add release notes: "Initial release with 5 science modules"

#### Complete the store listing:
- Upload screenshots (min 2, max 8) — see PLAYSTORE_LISTING.md
- Upload feature graphic (1024×500 px)
- Upload app icon (512×512 px)
- Paste the description from PLAYSTORE_LISTING.md
- Add privacy policy URL (host privacy_policy.html on a free site like GitHub Pages)

#### Content rating:
1. Go to **Policy → App content → Content rating**
2. Fill in the questionnaire
3. ScienceWiz should receive **Everyone** rating

#### Review and publish:
1. Complete all required sections (green checkmarks)
2. Submit for review
3. Google reviews in 1–7 days
4. You'll receive email confirmation when live

---

## 🔒 Security Features Included
- `minifyEnabled true` — code obfuscation in release build
- `shrinkResources true` — removes unused resources
- `network_security_config.xml` — blocks cleartext (HTTP) traffic
- `allowBackup="false"` — prevents data backup exposure
- `screenOrientation="portrait"` — locked to portrait
- ProGuard rules configured

---

## 💰 Adding AdMob (when ready)

1. Create account at https://admob.google.com
2. Add `google_mobile_ads: ^4.0.0` to pubspec.yaml
3. Add your AdMob App ID to AndroidManifest.xml:
```xml
<meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="ca-app-pub-XXXXXXXXXXXXXXXX~XXXXXXXXXX"/>
```
4. Add banner ad widget to each screen's bottom

---

## 📁 Project Structure
```
sciencewiz/
├── lib/
│   ├── main.dart                    # App entry + navigation
│   ├── screens/
│   │   ├── home_screen.dart         # Home with 5 module cards
│   │   ├── periodic_table_screen.dart
│   │   ├── physics_formulas_screen.dart
│   │   ├── equation_balancer_screen.dart
│   │   ├── human_body_screen.dart
│   │   └── experiment_guide_screen.dart
│   └── data/
│       ├── elements_data.dart       # 30 elements
│       ├── physics_data.dart        # 8 chapters, 40+ formulas
│       ├── human_body_data.dart     # 6 systems, 18 organs
│       └── experiments_data.dart   # 10 NCERT practicals
├── android/
│   ├── app/
│   │   ├── build.gradle             # Target SDK 34, signing config
│   │   ├── proguard-rules.pro       # Security obfuscation
│   │   └── src/main/
│   │       ├── AndroidManifest.xml
│   │       ├── kotlin/.../MainActivity.kt
│   │       └── res/
│   │           ├── xml/network_security_config.xml
│   │           └── values/styles.xml
│   └── build.gradle
├── assets/
│   └── privacy_policy.html
├── pubspec.yaml
├── .gitignore                       # Protects signing keys
├── PLAYSTORE_LISTING.md             # Copy-paste store description
└── README.md                        # This file
```

---

## ⚡ Quick Build (TL;DR)
```bash
flutter pub get
# (create keystore + key.properties as above)
flutter build appbundle --release
# Upload build/app/outputs/bundle/release/app-release.aab to Play Store
```

---

## 🆘 Common Issues

| Problem | Solution |
|---------|---------|
| `flutter doctor` shows ✗ for Android | Open Android Studio → SDK Manager → install Android SDK 34 |
| `keytool not found` | Use full path: `C:\Program Files\Java\jdk\bin\keytool` on Windows |
| Build fails with "key.properties not found" | Copy template file and fill in your passwords |
| App crashes on launch | Run `flutter run` in debug mode and check console output |
| `AAPT error` for icons | Add actual PNG icons to mipmap folders (see below) |

### Adding App Icons
Replace placeholder icons in these folders with 🔬 or atom PNG images:
- `android/app/src/main/res/mipmap-mdpi/` → 48×48 px
- `android/app/src/main/res/mipmap-hdpi/` → 72×72 px  
- `android/app/src/main/res/mipmap-xhdpi/` → 96×96 px
- `android/app/src/main/res/mipmap-xxhdpi/` → 144×144 px
- `android/app/src/main/res/mipmap-xxxhdpi/` → 192×192 px

Or use the `flutter_launcher_icons` package to auto-generate all sizes from one image.

---

*Built with Flutter 3.x | Target: Android 5.0+ (API 21+) | CBSE Class 9 & 10*
