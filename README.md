# 🌸 Persona's World (HerWorld)
 
![React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Expo](https://img.shields.io/badge/Expo-000020?style=for-the-badge&logo=expo&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Android](https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)
 
**Personalise • Journal • Remember**
 
A private, personalised wellness and memories app for Android, in **English and Hinglish**. It greets you by name, sends you a letter every day, helps you check in with your mood, keeps a journal that works offline and backs up to the cloud **encrypted with your own passcode**, lets you **write by speaking** in your own language, plays calming music, and keeps your photo memories together with the **place and time** they were taken. A **home screen widget** gives you the day's letter, one-tap writing and camera, and your music controls.
 
> 🚧 **Status:** Under active development. New features ship over-the-air.
 
<!-- Screenshots: add images to a "screenshots" folder and show them here, for example:
<p align="center">
  <img src="screenshots/home.png" width="200" />
  <img src="screenshots/journal.png" width="200" />
  <img src="screenshots/memories.png" width="200" />
  <img src="screenshots/widget.png" width="200" />
</p>
Use screenshots without real journal entries or personal photos.
-->
 
---
 
## 📲 Download
 
**Android APK (v1.3.0):** [Download the app](PASTE_NEW_APK_LINK_HERE)
 
1. Open the link on your Android phone and download the APK.
2. If asked, allow installs from your browser.
3. Open the app, pick your language and finish the short onboarding.
Works on Android 7 or newer, on 32-bit and 64-bit phones.
 
**Updates:** small updates arrive on their own. Close the app fully and open it twice to get them. When a new APK is out, an **Update** tag appears in Settings with a link to the newest version.
 
---
 
## ✨ Features
 
### Your personal space
- 👋 Onboarding with name, date of birth and language (**English** or **Hinglish**, changeable any time in Settings)
- 🏠 Home that greets you by name, with a gentle line for the day
- 🎂 Birthday countdown, the age you are turning, a small birthday ritual and wishes
### Every day
- 💌 **Daily letter**: 45 short letters, one a day, with a streak
- 💜 **How are you?**: pick one of 8 moods (Happy, Calm, Grateful, Energetic, Restless, Tired, Sad, Lonely) and get a kind note, small things to try and a song for the mood
- 📈 **Mood history**: your week, a 30-day chart and a gentle note if the last days were heavy (stays on your phone)
- ✨ Soul messages, Nature, Magic and more to explore
### Journal
- 📔 Works fully offline. Add up to 6 photos and finger doodles
- 🎙️ **Voice dictation**: tap the mic and speak, and your words appear in the entry. Choose **Hinglish** (written in English letters), English, Hindi, Telugu, Tamil, Kannada, Malayalam, Marathi, Bengali, Gujarati or Punjabi
- ✍️ **Drafts are saved automatically**, so an unfinished entry comes back even if the app was closed
- ☁️ Optional cloud backup with email sign-in and multi-device sync (deleted entries stay deleted)
- 🔐 Backup is **encrypted on your phone with your own passcode**. The server only sees scrambled text
### Memories
- 📸 Photo memories from camera or gallery: flash, timer, grid, zoom, colour filters, favourites and captions
- 📍 **Place and time on every photo**: camera photos are tagged with where they were taken (for example "Bengaluru, Karnataka") and the exact date and time. Gallery photos use the date and place stored inside the photo when it has them
- 🗂️ Photos are grouped **by month and place**, newest first, so a trip or a city becomes its own group
- 🧹 Remove the place from any single photo with one tap
### Music
- 🎵 Full songs and YouTube search, with a mini player that keeps playing on other screens
### Home screen widget (Android)
- 🌙 **Quick write** widget with a see-through background and two sizes
- 💌 Shows **today's letter** in your language, with your name
- ✍️ **Write** opens the journal with the writing box ready, and **Camera** opens the Memories camera
- 🎶 Shows the **cover and name of the last song**, with round **play/pause and next** buttons that work while the app is running in the background
### Care and control
- 🔒 **App lock** with your phone's fingerprint, face or PIN (Settings)
- 🔔 Three gentle reminders a day at times you choose, in your language
- 💌 Send feedback to the creator from Settings
- ⚡ Over-the-air updates, and a remote version gate to retire very old versions
---
 
## 🛠️ Tech Stack
 
### App
- React Native
- Expo (managed workflow, development builds)
- React Navigation, with deep links (`herworld://`) for the widget
- JavaScript
### Storage and security
- AsyncStorage (local-first) and expo-file-system for photos
- tweetnacl (secretbox) and @noble/hashes (PBKDF2) for the journal backup
- expo-local-authentication for the app lock
### Backend
- Firebase Authentication
- Cloud Firestore (accessed through the REST API)
- Firestore security rules
### Device features
- expo-speech-recognition (voice dictation)
- expo-location (place tags for photos)
- react-native-android-widget (home screen widget)
- expo-notifications
- expo-audio
- expo-camera
- expo-image-picker
### APIs
- Jamendo (music)
- YouTube Data API v3
### Builds, updates and config
- EAS Build (Android APK) and EAS Update (`expo-updates`)
- Remote config: a JSON file on GitHub (version gate) and a small JSON file for the update link
- Sentry for crash reports (wired in, switched on by adding a project key)
### Version control and tools
- Git, GitHub, VS Code, Expo Go, Node.js
---
 
## 🏗️ System Architecture
 
```
                    +---------------------------+
                    |    React Native App       |
                    |   (Expo, Android APK)     |
                    +-------------+-------------+
                                  |
     +-----------+----------------+--------------+------------+
     |           |                |              |            |
     v           v                v              v            v
 AsyncStorage  Firebase Auth   GitHub JSON    Jamendo /    Phone services
 (phone,       + Firestore     (version       YouTube      (speech engine,
 local first)  (encrypted      gate, update   (music)       location,
     |          journal)       link)                         camera)
     |           |
     +-- merge by id + remembered deletes
                 |
                 v
     Same journal on every phone
 
   Home screen widget  <--->  App (letter, last song, music controls)
 
        EAS Update  --->  New JavaScript reaches installed apps
```
 
---
 
## 🧠 How It Works
 
- **Local-first journal.** Entries are saved on the phone first. If the user is signed in, the app syncs when the journal opens and shortly after each change.
- **Safe sync.** Entries have unique ids and are merged by id. Deleted ids are remembered, so a deleted entry never returns from another device.
- **Encrypted backup.** The key is made on the phone from the user's passcode and never leaves it. Only the title, text and doodle are encrypted, and the cloud holds only scrambled text. A forgotten passcode means the cloud backup cannot be recovered. The journal on the phone stays readable on the phone.
- **Drafts.** What you are typing is saved on the phone while you write and the moment the app goes to the background. Saving or cancelling the entry removes it.
- **Voice dictation.** The phone's speech engine listens in the language you pick. For Hinglish, the app listens as Hindi and converts the result into English letters on the phone, using its own rules, so it is close to how people type but not perfect. Every dictated word can be edited like normal text.
- **Place tags.** After a camera photo is saved, the app looks up the phone's location and turns it into a place name. The photo is saved first, so the shutter never waits. Without a connection, the coordinates are saved and the name stays empty. Place and time are saved with the photo on the phone and never leave it.
- **Home screen widget.** The widget draws itself from the app's own data: today's letter, the user's name and the last song. Taps open the app through deep links, and the music buttons control the player while the app is alive. If the app was fully closed, the play button becomes a link that opens Music.
- **Two languages.** All words live in two files with the same keys. The chosen language is saved in the profile, so changing it in Settings changes every screen and the reminders.
- **Firebase over REST.** Sign-in, token refresh and Firestore access use plain HTTPS requests, which avoids known Expo bundler problems with the Firebase SDK.
- **Over-the-air updates.** JavaScript and content changes, including the widget layout, reach installed apps through EAS Update. A new APK is only needed for native changes (such as dictation, location or the widget itself), and an update only reaches apps built with the same app version.
- **Version gate and update tag.** On launch the app reads a JSON file from GitHub. If the installed version is too old, it shows an update screen. Settings also shows when a newer APK is available. If the user is offline, the app opens normally.
---
 
## 🔒 Privacy at a glance
 
| What | Where it lives |
|------|----------------|
| Photos, and the place and time saved with them | On your phone only. Never sent anywhere |
| Journal | On your phone. Optional encrypted copy in the cloud |
| Name, birthday, language, mood history | On your phone only |
| Voice for dictation | Turned into text by the phone's speech service (Google on most Android phones). The app does not keep recordings |
| Place names for photos | Looked up by the phone's location service when you have a connection |
| Feedback you send | Your message, an optional contact, app version, language and platform. Nothing else |
 
---
 
## ⚠️ Please note
 
Persona's World is a friendly space, **not medical care or therapy**. If you or someone near you is in danger, please call your local emergency number. In India: **112**, or **Tele-MANAS 14416** (free, 24x7).
 
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
 
- 🔎 Journal search and tags
- 🧾 Sync name and birthday across devices
- 🎞️ Real photo filters (black and white and more)
- 🌙 Light theme switch
- 📥 Export journal as PDF
- 🌍 Translate the remaining screens (Music, Memories, Explore, Account) and the widget buttons
- 🧩 More widgets (mood check-in)
- 📦 Store each journal entry as its own cloud document, for very large journals
---
 
## 👨‍💻 Author
 
**Shaik Mohammed Kaif**
Computer Science Engineer (AI & ML)
 
GitHub: https://github.com/KaifCodeur
LinkedIn: https://www.linkedin.com/in/kaifshaikmd/
 
---
 
## ⭐ Support
 
If you found this project interesting, please consider giving it a ⭐ on GitHub.
 
