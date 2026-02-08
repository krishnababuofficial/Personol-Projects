# Zone Alarm - Location-Based Alarm App

Zone Alarm is an Android application that triggers an alarm or ringtone when the user enters a predefined geographic location (geofence). Built with Kotlin and Android Jetpack components following MVVM architecture.

## Features

- 🗺️ **Google Maps Integration**: Interactive map to select destination
- 📍 **Current Location**: Automatically shows user's current location
- 🎯 **Geofencing**: Creates a 0.5 km radius geofence around selected location
- 🔔 **Background Monitoring**: Reliable location monitoring using foreground service
- ⏰ **Alarm Trigger**: Automatically triggers system alarm when entering geofence
- 🔔 **Notifications**: Shows notification when alarm is triggered
- 🛑 **Alarm Control**: User can start/stop the alarm

## Tech Stack

- **Language**: Kotlin
- **UI**: XML (Material Design)
- **Architecture**: MVVM (Model-View-ViewModel)
- **Maps**: Google Maps SDK for Android
- **Location**: FusedLocationProvider API
- **Geofencing**: Android Geofencing API
- **Background Execution**: Foreground Service + BroadcastReceiver
- **Alarm**: AlarmManager + RingtoneManager
- **Jetpack Components**:
  - ViewModel
  - LiveData
  - Navigation Component

## Project Structure

```
app/
├── src/main/
│   ├── java/com/zonealarm/app/
│   │   ├── ui/                    # Activities
│   │   │   ├── MainActivity.kt
│   │   │   ├── ConfirmationActivity.kt
│   │   │   └── AlarmActivity.kt
│   │   ├── viewmodel/             # ViewModels
│   │   │   └── MainViewModel.kt
│   │   ├── repository/            # Data Repository
│   │   │   └── LocationRepository.kt
│   │   ├── service/               # Services
│   │   │   └── GeofencingService.kt
│   │   ├── receiver/              # Broadcast Receivers
│   │   │   └── GeofenceBroadcastReceiver.kt
│   │   ├── data/model/            # Data Models
│   │   │   └── GeofenceData.kt
│   │   └── utils/                 # Utility Classes
│   │       ├── PermissionsHelper.kt
│   │       └── LocationHelper.kt
│   ├── res/
│   │   ├── layout/                # XML Layouts
│   │   ├── values/                # Strings, Colors, Themes
│   │   └── drawable/              # Drawable Resources
│   └── AndroidManifest.xml
```

## Setup Instructions

### Prerequisites

1. **Android Studio**: Arctic Fox or later
2. **JDK**: Version 17 or higher
3. **Android SDK**: Minimum SDK 24 (Android 7.0), Target SDK 34
4. **Google Maps API Key**: Required for map functionality

### Step 1: Get Google Maps API Key

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Enable the following APIs:
   - Maps SDK for Android
   - Geocoding API (optional, for better location features)
4. Go to "Credentials" → "Create Credentials" → "API Key"
5. Copy your API key

### Step 2: Configure API Key

1. Open `app/src/main/AndroidManifest.xml`
2. Find the line:
   ```xml
   <meta-data
       android:name="com.google.android.geo.API_KEY"
       android:value="YOUR_GOOGLE_MAPS_API_KEY" />
   ```
3. Replace `YOUR_GOOGLE_MAPS_API_KEY` with your actual API key

### Step 3: Build and Run

1. Open the project in Android Studio
2. Sync Gradle files (File → Sync Project with Gradle Files)
3. Connect an Android device or start an emulator
4. Click "Run" (▶️) or press `Shift + F10`

## Permissions

The app requires the following permissions:

- **ACCESS_FINE_LOCATION**: To get precise location
- **ACCESS_COARSE_LOCATION**: To get approximate location
- **ACCESS_BACKGROUND_LOCATION**: To monitor location in background (Android 10+)
- **FOREGROUND_SERVICE**: To run foreground service (Android 9+)
- **FOREGROUND_SERVICE_LOCATION**: For location-based foreground service (Android 14+)
- **POST_NOTIFICATIONS**: To show notifications (Android 13+)
- **INTERNET**: To load Google Maps

All permissions are requested at runtime with proper user explanations.

## How to Use

1. **Launch the App**: Open Zone Alarm on your device
2. **Grant Permissions**: Allow location and notification permissions when prompted
3. **Select Location**: 
   - The map will show your current location
   - Tap anywhere on the map to select a destination
   - A marker and 0.5 km radius circle will appear
4. **Set Zone Alarm**: Click "Set Zone Alarm" button
5. **Confirm**: Review the selected location on the confirmation screen
6. **Activate**: Click "Activate Alarm" to start monitoring
7. **Alarm Trigger**: When you enter the geofence, the alarm will automatically trigger
8. **Stop Alarm**: Click "Stop Alarm" button to stop the alarm and disable monitoring

## Architecture

### MVVM Pattern

- **Model**: `GeofenceData` - Data classes representing geofence information
- **View**: Activities (MainActivity, ConfirmationActivity, AlarmActivity) and XML layouts
- **ViewModel**: `MainViewModel` - Manages UI-related data and business logic
- **Repository**: `LocationRepository` - Handles location and geofence operations

### Key Components

1. **MainActivity**: 
   - Displays Google Map
   - Handles location selection
   - Manages permissions

2. **ConfirmationActivity**: 
   - Shows selected location details
   - Activates geofence monitoring

3. **AlarmActivity**: 
   - Displays when alarm is triggered
   - Plays ringtone and vibration
   - Allows user to stop alarm

4. **GeofencingService**: 
   - Foreground service for background location monitoring
   - Ensures reliable operation even when app is closed

5. **GeofenceBroadcastReceiver**: 
   - Receives geofence transition events
   - Triggers alarm and notifications

## Background Execution

The app uses a **Foreground Service** to ensure reliable location monitoring:

- Service runs with a persistent notification
- Continues monitoring even when app is closed
- Handles Android Doze mode restrictions
- Battery-optimized location updates

## Troubleshooting

### Maps Not Loading
- Verify Google Maps API key is correctly set in AndroidManifest.xml
- Check that Maps SDK for Android is enabled in Google Cloud Console
- Ensure device has internet connection

### Location Not Working
- Grant location permissions when prompted
- Enable location services on device
- For background monitoring, grant background location permission

### Alarm Not Triggering
- Ensure background location permission is granted
- Check that device location services are enabled
- Verify you're within the 0.5 km radius of the selected location
- Ensure foreground service is running (check notification)

### Build Errors
- Sync Gradle files: File → Sync Project with Gradle Files
- Clean and rebuild: Build → Clean Project, then Build → Rebuild Project
- Ensure all dependencies are downloaded

## Battery Optimization

To ensure the app works reliably:

1. Go to Settings → Apps → Zone Alarm
2. Disable battery optimization for the app
3. This ensures background location monitoring continues

## Limitations

- Geofence radius is fixed at 0.5 km (500 meters)
- Requires active internet connection for initial map loading
- Background location monitoring may consume battery
- Some devices may have restrictions on background location access

## Future Enhancements

- Customizable geofence radius
- Multiple geofence support
- Custom alarm sounds
- Geofence history/logs
- Widget for quick access

## License

This project is provided as-is for educational and development purposes.

## Support

For issues or questions, please check:
- Android documentation for Geofencing API
- Google Maps SDK documentation
- Android Foreground Services guide

---

**Note**: This app requires location permissions and may consume battery due to background location monitoring. Use responsibly.


## Test
This is a test push to verify GitHub integration.

