# Zone Alarm - Quick Setup Guide

## Prerequisites

- Android Studio Arctic Fox or later
- JDK 17 or higher
- Android device or emulator (API 24+)
- Google Maps API Key

## Step-by-Step Setup

### 1. Open Project in Android Studio

1. Launch Android Studio
2. Select "Open" or "Open an Existing Project"
3. Navigate to the Zone Alarm project folder
4. Click "OK"

### 2. Get Google Maps API Key

1. Visit [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or select existing)
3. Enable **Maps SDK for Android**:
   - Go to "APIs & Services" → "Library"
   - Search for "Maps SDK for Android"
   - Click "Enable"
4. Create API Key:
   - Go to "APIs & Services" → "Credentials"
   - Click "Create Credentials" → "API Key"
   - Copy the generated API key

### 3. Configure API Key in Project

1. Open `app/src/main/AndroidManifest.xml`
2. Find this line (around line 50):
   ```xml
   <meta-data
       android:name="com.google.android.geo.API_KEY"
       android:value="YOUR_GOOGLE_MAPS_API_KEY" />
   ```
3. Replace `YOUR_GOOGLE_MAPS_API_KEY` with your actual API key:
   ```xml
   <meta-data
       android:name="com.google.android.geo.API_KEY"
       android:value="AIzaSyBxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" />
   ```

### 4. Sync Gradle

1. Click "Sync Now" if prompted
2. Or go to: File → Sync Project with Gradle Files
3. Wait for sync to complete

### 5. Run the App

1. Connect an Android device via USB (with USB debugging enabled)
   - OR start an Android emulator
2. Click the "Run" button (▶️) or press `Shift + F10`
3. Select your device/emulator
4. Wait for the app to install and launch

## First Run

1. **Grant Permissions**: The app will request:
   - Location permission (Allow)
   - Background location permission (Allow) - Required for geofencing
   - Notification permission (Allow) - Required for Android 13+

2. **Select Location**:
   - Map will show your current location
   - Tap anywhere on the map to select a destination
   - A red circle (0.5 km radius) will appear

3. **Set Alarm**:
   - Click "Set Zone Alarm"
   - Review location on confirmation screen
   - Click "Activate Alarm"

4. **Test**:
   - Move to the selected location (within 0.5 km)
   - Alarm will trigger automatically

## Troubleshooting

### Maps Not Loading
- ✅ Verify API key is correct in AndroidManifest.xml
- ✅ Check Maps SDK for Android is enabled in Google Cloud Console
- ✅ Ensure device has internet connection
- ✅ Check API key restrictions (if any) allow your app

### Location Not Working
- ✅ Grant location permissions when prompted
- ✅ Enable location services on device (Settings → Location)
- ✅ For background monitoring, grant background location permission

### Alarm Not Triggering
- ✅ Ensure background location permission is granted
- ✅ Check device location services are enabled
- ✅ Verify you're within 0.5 km of selected location
- ✅ Check foreground service notification is visible

### Build Errors
- ✅ Sync Gradle: File → Sync Project with Gradle Files
- ✅ Clean project: Build → Clean Project
- ✅ Rebuild: Build → Rebuild Project
- ✅ Invalidate caches: File → Invalidate Caches / Restart

## Battery Optimization

For reliable background monitoring:

1. Go to Settings → Apps → Zone Alarm
2. Tap "Battery" or "Battery usage"
3. Select "Don't optimize" or "Unrestricted"
4. This ensures geofencing continues in background

## API Key Security (Production)

For production apps, restrict your API key:

1. In Google Cloud Console, go to your API key
2. Under "Application restrictions":
   - Select "Android apps"
   - Add your app's package name: `com.zonealarm.app`
   - Add your app's SHA-1 certificate fingerprint
3. Under "API restrictions":
   - Select "Restrict key"
   - Choose "Maps SDK for Android"

## Project Structure Overview

```
Zone Alarm/
├── app/
│   ├── src/main/
│   │   ├── java/com/zonealarm/app/
│   │   │   ├── ui/              # Activities
│   │   │   ├── viewmodel/        # ViewModels
│   │   │   ├── repository/       # Data layer
│   │   │   ├── service/          # Services
│   │   │   ├── receiver/         # BroadcastReceivers
│   │   │   ├── data/model/       # Data models
│   │   │   └── utils/            # Utilities
│   │   ├── res/                  # Resources
│   │   └── AndroidManifest.xml
│   └── build.gradle
├── build.gradle
├── settings.gradle
└── README.md
```

## Next Steps

- Customize geofence radius (currently fixed at 0.5 km)
- Add multiple geofence support
- Implement custom alarm sounds
- Add geofence history/logs

---

**Need Help?** Check the main README.md for detailed documentation.

