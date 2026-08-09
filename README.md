# Streaming App for Android

A video-streaming Android application built with Kotlin and Jetpack Compose. It includes a home feed, video details, local favorites, a profile page, and fullscreen video playback.

## Features

- Browse featured movies and categorized video rows
- View movie and TV-show details
- Browse and play TV-show episodes
- Play videos fullscreen with Media3/ExoPlayer
- Save favorite videos locally with Room
- View recently watched videos and favorites on the profile page

## Technology

| Area | Technology |
| --- | --- |
| Language | Kotlin |
| UI | Jetpack Compose and Material 3 |
| Architecture | MVVM and Repository pattern |
| Navigation | Navigation Compose |
| Networking | Retrofit, Gson, and OkHttp |
| Local database | Room |
| Dependency injection | Hilt |
| Images | Coil |
| Video player | Media3/ExoPlayer |

## Architecture

```text
Compose Screen
      | user actions
      v
ViewModel
      |
      v
Repository
      |-- Retrofit API --> Ktor backend
      `-- Room DAO --> Local favorites database

ViewModel StateFlow --> Compose Screen
```

- Screens display data and send user actions to ViewModels.
- ViewModels manage screen state.
- Repositories get data from the backend or Room database.
- Hilt creates and connects the app dependencies.

## Project structure

```text
app/src/main/java/com/laioffer/netflix/
|-- database/       # Room database and favorite data
|-- datamodel/      # Video, profile, episode, and response models
|-- di/             # Hilt dependency modules
|-- navigation/     # App routes and navigation graph
|-- network/        # Retrofit API
|-- player/         # Media3 player screen and ViewModel
|-- repository/     # Remote and local data access
`-- ui/
    |-- components/ # Reusable Compose components
    |-- home/       # Home screen and ViewModel
    |-- profile/    # Profile screen and ViewModel
    |-- theme/      # App theme
    `-- videodetail/# Detail screen and ViewModel
```

## Required software

This project was developed with:

- **Android Studio Panda 2 | 2025.3.2**, released March 3, 2026
- **Standard** installation option in the Android Studio Setup Wizard
- Android SDK 36
- Pixel Android Emulator with API 31 (Android 12.0)
- JDK 17 or newer

## Android Studio setup

1. Download and install **Android Studio Panda 2 | 2025.3.2** from the [Android Studio archive](https://developer.android.com/studio/archive).
2. Select **Standard** when the Setup Wizard asks for the installation type.
3. From the Android Studio welcome screen, open **More Actions > SDK Manager**.
4. In **SDK Platforms**, make sure the latest Android SDK platform is installed. This project uses Android SDK 36.
5. In **SDK Tools**, make sure these tools are installed:

   - Android SDK Build-Tools
   - Android SDK Command-line Tools (latest)
   - Android SDK Platform-Tools
   - Android Emulator

6. Select **Apply** or **OK** to install any missing packages.

## Create the emulator

1. Open **Device Manager** and select **Add Device**.
2. Choose the **Pixel** device profile shown in the screenshot.
3. Select **API 31 "S" (Android 12.0)** as the system image.
4. Download the system image if Android Studio asks for it.
5. Select **Finish** to create the virtual device.

## Companion backend

The frontend gets its catalog, profile, and video data from the companion Ktor backend:

- [Android frontend](https://github.com/Oliver-JL/streaming-app-android)
- [Companion backend](https://github.com/Oliver-JL/streaming-app-backend)

Clone or download both projects. Open the backend project and run `Application.kt` using the IDE's green **Run** button. The backend should start on port `8080`.

## Run the Android app

1. Open the frontend project in Android Studio.
2. Wait for Gradle sync to finish.
3. Start the Pixel API 31 emulator from **Device Manager**.
4. Make sure the backend is already running.
5. Select the `app` configuration and your emulator in the toolbar.
6. Click the green **Run** button.

## Network configuration

The frontend connects to:

```text
http://10.0.2.2:8080/
```

This URL is configured in `di/NetworkModule.kt`. In the standard Android Emulator, `10.0.2.2` points to the computer running the backend.

## Using the app

1. Browse videos on **Home**.
2. Select a video to open its detail page.
3. Select the heart icon to add or remove a favorite.
4. Select **Play** for a movie or select an episode for a TV show.
5. Open **My Netflix** to view the profile, recently watched videos, and favorites.
