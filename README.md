# OnePlayer

OnePlayer is a modular Android media player project. It showcases multiple playback backends (Media3/ExoPlayer, VLC, IJK) behind a shared core, with a Jetpack Compose sample app.

This README was created on November 22, 2025 to help new contributors quickly build and run the project.

## At a glance
- App ID: `dev.sajidali.oneplayer`
- UI: Jetpack Compose
- Min SDK: 24 (app)
- Target SDK: 33
- Compile SDK: 34 (app), 33 (libraries)
- Kotlin: 1.8.10
- Android Gradle Plugin: 8.1.2

## Modules
- `app` — Compose sample app that depends on the Media3 backend.
- `oneplayer` — Core player abstractions (Android library). Note: this folder exists in the repo and is referenced by other modules.
- `media3` — ExoPlayer/Media3-based backend. Depends on `:oneplayer` and wraps Media3 (`androidx.media3:media3-exoplayer`).
- `vlc` — VLC-based backend (Android library placeholder).
- `ijk` — IJK-based backend (Android library placeholder).
- `exoffmpeg` — Local AAR wrapper that provides `exoffmpeg.aar` as a dependency.

> Heads-up: The current `settings.gradle.kts` includes `:base`, but the repository contains `oneplayer` and other modules reference `:oneplayer`. If you encounter a Gradle error like "Project :base not found", replace the include with `include(":oneplayer")` in `settings.gradle.kts`.

## Getting started
### Prerequisites
- Android Studio (Giraffe/Koala or newer)
- JDK 17 (recommended for AGP 8.x)
- Android SDK platforms for API 33 and 34

### Build from the command line
```bash
./gradlew clean assembleDebug
```
Artifacts will be written under each module's `build/outputs/` directory. The app debug APK is typically at `app/build/outputs/apk/debug/`.

### Run in Android Studio
1. Open the repository root in Android Studio.
2. Let Gradle sync finish.
3. Select the `app` run configuration.
4. Run on a device or emulator (API 24+).

## Tech notes
- Compose is enabled in `app` (Compose BOM 2023.03.00, Material 3).
- The `media3` backend exports Media3 ExoPlayer APIs and depends on `:exoffmpeg` via a local AAR.
- Library modules use Java 8 bytecode and Kotlin JVM target 1.8.

## Testing
- Unit tests: `./gradlew test`
- Instrumented tests (if any): `./gradlew connectedAndroidTest`

## Project layout
```
app/           — Jetpack Compose demo application
oneplayer/     — Core player abstractions (Android library)
media3/        — Media3/ExoPlayer backend (Android library)
vlc/           — VLC backend (Android library)
ijk/           — IJK backend (Android library)
exoffmpeg/     — Local AAR published via Gradle configuration
```

## License
No license file was found in this repository as of November 22, 2025. If you intend to open‑source this project, consider adding a LICENSE file (e.g., MIT, Apache-2.0).

## Troubleshooting
- Gradle include mismatch: see the note above about `:base` vs `:oneplayer`.
- If Gradle asks for a higher JDK, switch the Gradle JVM in Android Studio to JDK 17.
- If Compose compiler version conflicts, align the Android Studio Kotlin plugin and the `composeOptions.kotlinCompilerExtensionVersion`.
