# SNM Assist

A personal assistant Android app for meal planning and financial tracking, powered by Firebase.

## Features

- 🍽️ **Meal Planning** - Plan meals, manage recipes, track ingredients
- 💰 **Financial Tracking** - Track income, expenses, and budgets
- 🔐 **User Authentication** - Secure Firebase authentication
- ☁️ **Cloud Sync** - Real-time data sync with Firestore

## Tech Stack

- **Frontend:** Android (Kotlin)
- **Backend:** Firebase (Firestore, Authentication)
- **Architecture:** MVVM with Repository Pattern
- **UI Framework:** Jetpack Compose & Material Design 3

## Getting Started

### Prerequisites

- Android Studio (latest version)
- JDK 11+
- Firebase account

### Setup

1. Clone the repository
2. Create a Firebase project at https://console.firebase.google.com
3. Download `google-services.json` and place it in `app/`
4. Open in Android Studio and sync Gradle
5. Run on emulator or device

### Firebase Setup

1. Enable Firestore Database
2. Enable Firebase Authentication (Email/Password)
3. Set Firestore security rules:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth.uid == userId;
    }
  }
}
```

## Building

```bash
./gradlew build
./gradlew assembleDebug   # Debug APK
./gradlew assembleRelease # Release APK
```

## Project Structure

```
snm-assist/
├── app/
│   ├── src/main/
│   │   ├── java/com/silatech/snmassist/
│   │   │   ├── ui/
│   │   │   ├── viewmodel/
│   │   │   ├── repository/
│   │   │   ├── model/
│   │   │   └── MainActivity.kt
│   │   └── res/
│   ├── build.gradle.kts
│   └── google-services.json
├── gradle/
├── settings.gradle.kts
├── build.gradle.kts
└── README.md
```

## License

MIT License
