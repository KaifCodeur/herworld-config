# 🌸 Persona's World (HerWorld)

![React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Expo](https://img.shields.io/badge/Expo-000020?style=for-the-badge&logo=expo&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Android](https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)

**Personalise • Journal • Remember**

A personalised wellness and memories app for Android. It greets you by name, counts down to your birthday, keeps a private journal that works offline and backs up to the cloud, plays calming music and stores your photo memories.

> 🚧 **Status:** Under active development. New features ship over-the-air.

---

## 📲 Download

**Android APK (v1.1.0):** [Download the app] --> Coming soon

1. Open the link on your Android phone and download the APK.
2. If asked, allow installs from your browser.
3. Open the app and finish the short onboarding.

Works on Android 7 or newer, on 32-bit and 64-bit phones.

---

## ✨ Features

- 👋 Onboarding with name and date of birth
- 🎂 Birthday countdown and the age you are turning
- 📔 Journal that works fully offline
- ☁️ Optional cloud backup with email sign-in
- 🔄 Multi-device sync, deleted entries stay deleted
- 🎵 Music player with background playback
- 📸 Photo memories from camera or gallery
- 🔔 One gentle notification per day with a custom icon
- ⚡ Over-the-air updates without a new APK
- 🚦 Remote version gate to retire old versions
- 📱 Optimised for Android

---

## 🛠️ Tech Stack

### App
- React Native
- Expo (managed workflow)
- React Navigation
- JavaScript

### Storage
- AsyncStorage (local-first)

### Backend
- Firebase Authentication
- Cloud Firestore (accessed through the REST API)
- Firestore security rules

### Device Features
- expo-notifications
- expo-audio
- expo-camera
- expo-image-picker

### APIs
- YouTube Data API v3

### Builds and Updates
- EAS Build (Android APK)
- EAS Update (`expo-updates`)

### Remote Config
- JSON file hosted on GitHub

### Version Control and Tools
- Git
- GitHub
- VS Code
- Expo Go
- Node.js

---

## 🏗️ System Architecture

```
                 +------------------------+
                 |   React Native App     |
                 |  (Expo, Android APK)   |
                 +-----------+------------+
                             |
        +--------------------+--------------------+
        |                    |                    |
        ▼                    ▼                    ▼
  AsyncStorage         Firebase Auth        GitHub JSON file
  (local-first)        + Firestore          (version gate)
        |                    |
        +---- merge by id ---+
         + remembered deletes
                             |
                             ▼
                  Same journal on every phone

        EAS Update  ───►  New JavaScript reaches installed apps
```

---

## 🧠 How It Works

- **Local-first journal.** Entries are saved on the phone first. If the user is signed in, the app syncs when the journal opens and shortly after each change.
- **Safe sync.** Entries have unique ids and are merged by id. Deleted ids are remembered, so a deleted entry never returns from another device.
- **Firebase over REST.** Sign-in, token refresh and Firestore access use plain HTTPS requests, which avoids known Expo bundler problems with the Firebase SDK.
- **Over-the-air updates.** JavaScript and content changes reach installed apps through EAS Update. A new APK is only needed for native changes.
- **Version gate.** On launch the app reads a JSON file from GitHub. If the installed version is too old, it shows an update screen. If the user is offline, the app opens normally.

---

## 🚀 Deployment

| Service | Platform |
|---------|----------|
| App Builds | EAS Build |
| Updates | EAS Update |
| Backend | Firebase |
| Remote Config | GitHub |

---

## 🎯 Future Improvements

- 🔐 App lock (PIN / fingerprint)
- 🔒 End-to-end encrypted journal
- 🧾 Sync name and birthday across devices
- 🌙 Dark mode
- 📥 Export journal as PDF
- 🌍 Multi-language support

---

## 👨‍💻 Author

**Shaik Mohammed Kaif**
Computer Science Engineer (AI & ML)

GitHub: https://github.com/KaifCodeur
LinkedIn: https://www.linkedin.com/in/kaifshaikmd/

---

## ⭐ Support

If you found this project interesting, please consider giving it a ⭐ on GitHub.
