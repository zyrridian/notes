# Firebase Setup for Flutter

```bash
npm install -g firebase-tools
firebase login
dart pub global activate flutterfire_cli
flutterfire configure
```

This command:
- Creates `firebase_options.dart`
- Links your Flutter app to your Firebase project
- Configures Android, iOS, macOS, web, and other selected platforms
