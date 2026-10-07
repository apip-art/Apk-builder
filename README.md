# APK Builder - Simple Kotlin Template

Template sederhana untuk membuat APK menggunakan Kotlin dengan automated build menggunakan GitHub Actions.

## 🚀 Features

✅ Simple Kotlin MainActivity  
✅ Material Design UI  
✅ AndroidX libraries  
✅ GitHub Actions CI/CD  
✅ Automated APK Build & Upload  
✅ Debug & Release builds  

## 📁 Struktur Proyek

```
├── .github/
│   └── workflows/
│       └── build-apk.yml          # GitHub Actions workflow
├── app/
│   ├── build.gradle.kts           # App configuration
│   ├── proguard-rules.pro
│   └── src/
│       └── main/
│           ├── kotlin/            # Kotlin source code
│           │   └── com/example/simpleapp/
│           │       └── MainActivity.kt
│           ├── res/               # Resources
│           │   ├── layout/
│           │   │   └── activity_main.xml
│           │   └── values/
│           │       ├── strings.xml
│           │       └── themes.xml
│           └── AndroidManifest.xml
├── build.gradle.kts               # Root configuration
├── settings.gradle.kts
└── README.md
```

## 🔨 Build Lokal

### Prerequisites
- Android SDK 24 atau lebih tinggi
- Java 17+
- Gradle 8.0+

### Debug Build
```bash
./gradlew assembleDebug
```
Output: `app/build/outputs/apk/debug/app-debug.apk`

### Release Build
```bash
./gradlew assembleRelease
```
Output: `app/build/outputs/apk/release/app-release.apk`

## 🤖 GitHub Actions - Automated Build

Workflow otomatis akan dijalankan ketika:
- Push ke branch `main` atau `develop`
- Pull request dibuka ke `main` atau `develop`
- Create tag untuk release

### Status Build
Lihat status build di: https://github.com/apip-art/Apk-builder/actions

### Download APK
1. Buka [Actions tab](https://github.com/apip-art/Apk-builder/actions)
2. Pilih run yang ingin didownload
3. Scroll ke bawah → "Artifacts"
4. Download `debug-apk` atau `release-apk`

## 📝 Workflow Details

File: `.github/workflows/build-apk.yml`

**Jobs yang dijalankan:**
1. ✅ Checkout code
2. ✅ Setup JDK 17
3. ✅ Setup Android SDK
4. ✅ Build Debug APK
5. ✅ Build Release APK
6. ✅ Upload artifacts
7. ✅ Create release (jika tag dibuat)

## 🔧 Customization

### Ubah Package Name
1. Edit `app/build.gradle.kts`:
   ```kotlin
   applicationId = "com.yourcompany.yourapp"
   namespace = "com.yourcompany.yourapp"
   ```
2. Rename folder: `app/src/main/kotlin/com/example/simpleapp/` → `app/src/main/kotlin/com/yourcompany/yourapp/`
3. Edit `app/src/main/AndroidManifest.xml`

### Ubah App Name
Edit `app/src/main/res/values/strings.xml`:
```xml
<string name="app_name">Your App Name</string>
```

### Ubah Theme
Edit `app/src/main/res/values/themes.xml` untuk mengubah warna dan style.

### Tambah Dependencies
Edit `app/build.gradle.kts` di section `dependencies`:
```kotlin
implementation("com.library:package:version")
```

## 📦 Release ke Play Store

Untuk membuat signed release APK:

1. Generate keystore:
```bash
keytool -genkey -v -keystore release.keystore -keyalg RSA -keysize 2048 -validity 10000 -alias release
```

2. Update `app/build.gradle.kts`:
```kotlin
signingConfigs {
    create("release") {
        storeFile = file("release.keystore")
        storePassword = "your_password"
        keyAlias = "release"
        keyPassword = "your_password"
    }
}

buildTypes {
    release {
        signingConfig = signingConfigs.getByName("release")
        isMinifyEnabled = true
        proguardFiles(...)
    }
}
```

## 🐛 Troubleshooting

### Build gagal - SDK tidak ditemukan
```bash
# Update SDK
sdkmanager --update
sdkmanager "platforms;android-34"
```

### Gradle daemon error
```bash
./gradlew --stop
./gradlew clean build
```

### GitHub Actions timeout
- Increase timeout di `.github/workflows/build-apk.yml`
- atau gunakan self-hosted runner

## 📚 Resources

- [Android Developer Docs](https://developer.android.com)
- [Kotlin Documentation](https://kotlinlang.org/docs)
- [Gradle Android Plugin](https://developer.android.com/studio/releases/gradle-plugin)
- [GitHub Actions](https://docs.github.com/en/actions)

## 📄 License

MIT License - Feel free to use this template for any project!

---

**Dibuat dengan ❤️ untuk memudahkan development APK Android**
