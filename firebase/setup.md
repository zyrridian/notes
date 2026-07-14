# Firebase Setup for Flutter

## Prerequisites

- Flutter SDK installed
- Dart SDK (comes with Flutter)
- Node.js and npm installed

## 1. Install the Firebase CLI

```bash
npm install -g firebase-tools
```

## 2. Login to Firebase

```bash
firebase login
```

## 3. Install the FlutterFire CLI

```bash
dart pub global activate flutterfire_cli
```

## 4. Configure your Flutter project

```bash
flutterfire configure
```

This command:
- Creates `firebase_options.dart`
- Links your Flutter app to your Firebase project
- Configures Android, iOS, macOS, web, and other selected platforms