# React Native + Expo + CLI Commands Cheat Sheet

## 1. Create a New Expo Project

| Command                                                 | Purpose                          |
| ------------------------------------------------------- | -------------------------------- |
| `npx create-expo-app MyApp`                             | Create a new Expo project        |
| `npx create-expo-app@latest MyApp`                      | Create project using latest Expo |
| `npx create-expo-app MyApp --template blank-typescript` | TypeScript template              |
| `npx create-expo-app MyApp --template tabs`             | Tabs template                    |
| `npx create-expo-app --help`                            | Show help                        |

---

## 2. Start Development Server

| Command                      | Purpose                       |
| ---------------------------- | ----------------------------- |
| `npx expo start`             | Start Expo development server |
| `npm start`                  | Same as Expo start            |
| `npx expo start --clear`     | Clear Metro cache             |
| `npx expo start --tunnel`    | Use tunnel connection         |
| `npx expo start --localhost` | Use localhost                 |
| `npx expo start --lan`       | LAN mode                      |
| `npx expo start --offline`   | Offline mode                  |

---

## 3. Install Packages

| Command                      | Purpose                         |
| ---------------------------- | ------------------------------- |
| `npx expo install <package>` | Install Expo-compatible package |
| `npm install <package>`      | Install package                 |
| `npm install`                | Install all dependencies        |
| `npm uninstall <package>`    | Remove package                  |
| `npm update`                 | Update packages                 |
| `npm outdated`               | Show outdated packages          |
| `npx expo install <modules>` | Install Native Modules          |

---

## 4. Expo Doctor

| Command                  | Purpose              |
| ------------------------ | -------------------- |
| `npx expo-doctor`        | Check project health |
| `npx expo install --fix` | Fix package versions |

---

## 5. Build Android

| Command                                  | Purpose              |
| ---------------------------------------- | -------------------- |
| `npx expo run:android`                   | Native Android build |
| `npx expo run:android --device`          | Run on device        |
| `npx expo run:android --variant release` | Release build        |

---

## 6. Build iOS

| Command                        | Purpose         |
| ------------------------------ | --------------- |
| `npx expo run:ios`             | Run iOS         |
| `npx expo run:ios --device`    | Physical device |
| `npx expo run:ios --simulator` | Simulator       |

---

## 7. Prebuild

| Command                     | Purpose                        |
| --------------------------- | ------------------------------ |
| `npx expo prebuild`         | Generate Android & iOS folders |
| `npx expo prebuild --clean` | Clean prebuild                 |

---

## 8. Expo Login

| Command           | Purpose         |
| ----------------- | --------------- |
| `npx expo login`  | Login           |
| `npx expo logout` | Logout          |
| `npx expo whoami` | Current account |

---

## 9. EAS Build

| Command                    | Purpose        |
| -------------------------- | -------------- |
| `eas build:configure`      | Configure EAS  |
| `eas build -p android`     | Android build  |
| `eas build -p ios`         | iOS build      |
| `eas build --platform all` | Both platforms |
| `eas build:list`           | List builds    |
| `eas build:view`           | View build     |
| `eas build:cancel`         | Cancel build   |

---

## 10. EAS Submit

| Command                 | Purpose        |
| ----------------------- | -------------- |
| `eas submit -p android` | Upload APK/AAB |
| `eas submit -p ios`     | Upload IPA     |

---

## 11. Expo Update

| Command                          | Purpose           |
| -------------------------------- | ----------------- |
| `eas update`                     | OTA update        |
| `eas update --branch production` | Production update |
| `eas update --message "Bug Fix"` | Update message    |

---

## 12. Expo Credentials

| Command             | Purpose             |
| ------------------- | ------------------- |
| `eas credentials`   | Manage certificates |
| `eas device:create` | Register iPhone     |
| `eas device:list`   | List devices        |

---

## 13. React Native CLI

| Command                          | Purpose               |
| -------------------------------- | --------------------- |
| `npx react-native init MyApp`    | Create RN CLI project |
| `npx react-native run-android`   | Android               |
| `npx react-native run-ios`       | iOS                   |
| `npx react-native doctor`        | Diagnose environment  |
| `npx react-native clean-project` | Clean project         |

---

## 14. Metro

| Command                                | Purpose           |
| -------------------------------------- | ----------------- |
| `npx react-native start`               | Metro server      |
| `npx react-native start --reset-cache` | Reset cache       |
| `npx expo start --clear`               | Clear Metro cache |

---

## 15. Android (ADB)

| Command                         | Purpose       |
| ------------------------------- | ------------- |
| `adb devices`                   | List devices  |
| `adb reverse tcp:8081 tcp:8081` | Reverse port  |
| `adb logcat`                    | Device logs   |
| `adb shell`                     | Open shell    |
| `adb uninstall package.name`    | Uninstall app |

---

## 16. Gradle

| Command                     | Purpose       |
| --------------------------- | ------------- |
| `./gradlew clean`           | Clean Android |
| `./gradlew assembleDebug`   | Debug APK     |
| `./gradlew assembleRelease` | Release APK   |
| `./gradlew bundleRelease`   | Generate AAB  |

---

## 17. CocoaPods

| Command           | Purpose      |
| ----------------- | ------------ |
| `pod install`     | Install pods |
| `pod update`      | Update pods  |
| `pod deintegrate` | Remove pods  |

---

## 18. Cache Cleaning

| Command                   | Purpose                |
| ------------------------- | ---------------------- |
| `npx expo start --clear`  | Clear Metro            |
| `npm cache clean --force` | Clear npm              |
| `watchman watch-del-all`  | Clear Watchman         |
| `rm -rf node_modules`     | Remove modules         |
| `npm install`             | Reinstall dependencies |

---

## 19. TypeScript

| Command           | Purpose         |
| ----------------- | --------------- |
| `npx tsc --init`  | Create tsconfig |
| `npx tsc`         | Compile         |
| `npx tsc --watch` | Watch           |

---

## 20. ESLint

| Command                 | Purpose     |
| ----------------------- | ----------- |
| `npm run lint`          | Lint        |
| `npm run lint -- --fix` | Auto fix    |
| `npx eslint .`          | Manual lint |

---

## 21. Prettier

| Command                  | Purpose          |
| ------------------------ | ---------------- |
| `npx prettier --write .` | Format           |
| `npx prettier --check .` | Check formatting |

---

## 22. Daily Commands

| Command                         | Purpose              |
| ------------------------------- | -------------------- |
| `npm install`                   | Install dependencies |
| `npx expo start`                | Start project        |
| `npx expo start --clear`        | Clear cache          |
| `npx expo-doctor`               | Health check         |
| `npx expo install package-name` | Install Expo package |
| `npm install package-name`      | Install package      |
| `npm uninstall package-name`    | Remove package       |
| `npx expo run:android`          | Android              |
| `npx expo run:ios`              | iOS                  |
| `eas build -p android`          | Build Android        |
| `eas update`                    | OTA update           |
| `npm run lint`                  | Lint                 |
| `npm test`                      | Run tests            |
