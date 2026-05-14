# 🚀 Build ScienceWiz AAB on Codemagic (FREE — No Installation Needed)

Follow these steps exactly. Takes about 20 minutes total.

---

## PHASE 1 — Create Your Signing Keystore (5 minutes)
You need this ONCE. It's your app's permanent identity on Play Store.

### If you have Java installed on your PC:
```bash
keytool -genkey -v \
  -keystore sciencewiz-release.jks \
  -keyalg RSA -keysize 2048 \
  -validity 10000 \
  -alias sciencewiz
```
Answer the prompts:
- Enter keystore password: **choose something strong, WRITE IT DOWN**
- Re-enter password: same
- First and last name: Your name
- Organisational unit: (press Enter to skip)
- Organisation: Your name or company
- City: Your city
- State: Your state (e.g. Maharashtra)
- Country code: IN
- Confirm with: **yes**

This creates `sciencewiz-release.jks` in your current folder.

### If you DON'T have Java:
1. Go to https://keystore-generator.vercel.app  (free online tool)
2. Fill in the form, download the `.jks` file
3. Save the passwords you used

---

## PHASE 2 — Set Up Codemagic (10 minutes)

### Step 1 — Create free account
1. Go to **https://codemagic.io**
2. Click **"Sign up free"**
3. Sign up with GitHub or Google (easiest)

### Step 2 — Upload your project
**Option A — Via GitHub (recommended):**
1. Create a free account at https://github.com
2. Create a new repository called `sciencewiz` (set to Private)
3. Extract the ZIP file on your computer
4. Upload all files to GitHub (drag and drop in browser)
5. In Codemagic → click **"Add application"** → connect GitHub → select `sciencewiz`

**Option B — Direct ZIP upload:**
1. In Codemagic → click **"Add application"**
2. Select **"Other"** → upload zip directly

### Step 3 — Upload your Keystore
1. In Codemagic → go to **Teams → Personal Account → Keystores**
2. Click **"Add keystore"**
3. Upload your `sciencewiz-release.jks` file
4. Enter:
   - **Keystore name:** `sciencewiz_keystore`  ← must match codemagic.yaml exactly
   - **Keystore password:** (what you set in Phase 1)
   - **Key alias:** `sciencewiz`
   - **Key password:** (what you set in Phase 1)
5. Click **Save**

### Step 4 — Trigger the Build
1. In your app → click **"Start build"**
2. Select workflow: **"android-release"**
3. Click **"Start"**
4. Watch the live build log — takes about 5-10 minutes

### Step 5 — Download your AAB
1. When build shows ✅ green:
2. Click **"Artifacts"**
3. Download **`app-release.aab`** ← this is your Play Store file
4. Also download **`app-release.apk`** ← install this on your phone to test

---

## PHASE 3 — Test Before Uploading (2 minutes)

### Install APK on your Android phone:
1. On your phone: Settings → Security → **Enable "Unknown sources"** or **"Install unknown apps"**
2. Transfer the APK to your phone via USB or WhatsApp
3. Open the file and install
4. Test all 5 modules thoroughly

---

## PHASE 4 — Publish (FREE options)

### Option A — Amazon Appstore (100% FREE)
Reaches millions of Android users in India. No fee ever.
1. Go to https://developer.amazon.com/apps-and-games
2. Create free account
3. Click **"Add new app"** → Android
4. Upload your `app-release.aab`
5. Fill in title, description (copy from PLAYSTORE_LISTING.md)
6. Submit — approved in 1-3 days

### Option B — Google Play Store ($25 one-time)
1. Go to https://play.google.com/console
2. Pay $25 (one time only, forever)
3. Upload `app-release.aab`
4. Fill store listing from PLAYSTORE_LISTING.md
5. Submit for review (1-7 days)

---

## ❗ Common Problems & Fixes

| Problem | Fix |
|---------|-----|
| Build fails: "keystore not found" | Check keystore name in Codemagic matches `sciencewiz_keystore` in codemagic.yaml |
| Build fails: "flutter pub get failed" | Check pubspec.yaml is in root of project |
| Build fails: "compileSdk" error | Codemagic free tier uses latest Android SDK — already set to 34 |
| APK installs but crashes | Check build log for Dart errors before building |
| Codemagic says "no workflow found" | Make sure codemagic.yaml is in the ROOT folder of the project |

---

## 📧 Support
- Codemagic docs: https://docs.codemagic.io
- Codemagic free Discord: https://discord.gg/codemagic
- Amazon Appstore help: https://developer.amazon.com/docs

---
*You do not need Android Studio, Flutter, or any developer tools on your PC.*
*Everything compiles in the cloud for free.*
