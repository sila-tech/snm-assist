# SNM Assist - Complete Setup Guide

## Overview

SNM Assist is a personal Android app for meal planning and financial tracking using Firebase backend.

## Prerequisites

- Android Studio Giraffe+ 
- JDK 11+
- Firebase account
- Git

## Firebase Setup

### 1. Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Click "Add project" → name it `snm-assist`
3. Enable Google Analytics (optional)
4. Click "Create project"

### 2. Add Android App

1. In Firebase Console, click "Add app" → Select Android
2. Android package name: `com.silatech.snmassist`
3. App nickname: `SNM Assist`
4. Click "Register app"
5. Download `google-services.json`

### 3. Place google-services.json

```bash
# Copy downloaded file to:
app/google-services.json
```

### 4. Configure Firestore

1. Firebase Console → Firestore Database → Create Database
2. Start in **Test mode** (for development)
3. Select closest region

### 5. Set Firestore Security Rules

```firestore
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth.uid == userId;
    }
  }
}
```

### 6. Enable Authentication

Firebase Console → Authentication → Email/Password → Enable

## Local Setup

### 1. Clone Repository

```bash
git clone https://github.com/sila-tech/snm-assist.git
cd snm-assist
```

### 2. Open in Android Studio

- File → Open → Select `snm-assist` folder
- Wait for Gradle sync

### 3. Run App

```bash
# Option 1: Android Studio
Run → Run 'app'

# Option 2: Command line
./gradlew run
```

## Project Structure

```
snm-assist/
├── app/
│   ├── src/main/
│   │   ├── java/com/silatech/snmassist/
│   │   │   ├── di/              # Dependency Injection
│   │   │   ├── model/           # Data classes
│   │   │   ├── repository/      # Data access
│   │   │   ├── ui/
│   │   │   │   ├── screens/     # UI Screens
│   │   │   │   └── theme/       # Theme config
│   │   │   ├── MainActivity.kt
│   │   │   └── SNMAssistApp.kt
│   │   └── res/                 # Resources
│   └── build.gradle.kts
├── .github/workflows/           # CI/CD
└── README.md
```

## Features

### Current
✅ Login/Signup UI  
✅ Home screen with tabs  
✅ Meal and Finance tabs  
✅ Firebase configuration  
✅ Authentication repository  
✅ MVVM architecture ready  

### To Implement
- [ ] Complete Firebase auth integration
- [ ] Add/edit meal functionality
- [ ] Transaction CRUD operations
- [ ] Budget tracking with alerts
- [ ] Data visualization (charts)
- [ ] Offline support with caching
- [ ] Push notifications

## Building APK

### Debug APK
```bash
./gradlew assembleDebug
# Output: app/build/outputs/apk/debug/app-debug.apk
```

### Release APK
```bash
./gradlew assembleRelease
# Output: app/build/outputs/apk/release/app-release.apk
```

## Testing

```bash
# Run unit tests
./gradlew test

# Run instrumented tests
./gradlew connectedAndroidTest
```

## Troubleshooting

### Gradle Sync Issues
```bash
File → Sync Now
# or
./gradlew --refresh-dependencies
```

### Firebase Connection Failed
- Verify `google-services.json` location: `app/google-services.json`
- Check package name matches Firebase console
- Rebuild project: Build → Clean Project → Rebuild Project

### Build Errors
- Ensure JDK 11 in Android Studio: File → Project Structure → SDK Location
- Clear cache: Build → Clean Project

## Development Workflow

1. Create feature branch
   ```bash
   git checkout -b feature/meal-planning
   ```

2. Make changes and commit
   ```bash
   git commit -am "Add meal creation screen"
   ```

3. Push to GitHub
   ```bash
   git push origin feature/meal-planning
   ```

4. Create Pull Request on GitHub

## CI/CD Pipeline

GitHub Actions automatically:
- Builds APK on push to `main`/`develop`
- Runs tests
- Uploads APK artifacts
- View in Actions tab

## Dependencies

### Core
- androidx.core:core-ktx
- androidx.lifecycle:lifecycle-runtime-ktx
- androidx.activity:activity-compose

### Compose & UI
- androidx.compose.ui:ui
- androidx.compose.material3:material3
- androidx.navigation:navigation-compose

### Firebase
- com.google.firebase:firebase-auth-ktx
- com.google.firebase:firebase-firestore-ktx

### DI & Architecture
- com.google.dagger:hilt-android
- androidx.lifecycle:lifecycle-viewmodel-compose

## Next Steps

1. Add Firebase auth implementation in AuthViewModel
2. Create meal/transaction management screens
3. Implement Firestore database operations
4. Add data validation and error handling
5. Deploy to Google Play Store

## Support & Issues

Create issues in GitHub repository for bugs or feature requests.

## License

MIT License
