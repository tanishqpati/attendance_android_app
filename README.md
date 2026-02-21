# Attendance App

An Android application for managing employee attendance. Supports both employee and organization roles, with features for clock-in/clock-out, attendance tracking, location-based logging, and organization dashboards.

## Features

### Employee
- Phone number + OTP login
- Profile view (name, organization, hours worked, joining date)
- Attendance calendar and daily details
- Background location logging (optional, sends status to server periodically)
- Mark attendance manually

### Organization
- Organization login and dashboard
- View employee attendance by date and name
- Calendar summary and reports

### Technical
- Jetpack Compose UI
- Retrofit for REST API calls
- DataStore for persisted login state
- WorkManager and foreground service for background logging
- Location and WiFi-based presence verification

## Prerequisites

- **Android Studio** (Ladybug or newer recommended)
- **JDK 11**
- **Android SDK** with:
  - minSdk: 26
  - targetSdk: 36
  - compileSdk: 36
- Physical device or emulator (API 26+)

## Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd attendance_android_app
   ```

2. **Open in Android Studio**
   - Open the project folder in Android Studio
   - Let Gradle sync finish

3. **Configure API (optional)**
   - The app uses `https://eagle-app-dd32851971ff.herokuapp.com/` as the backend
   - To change it, edit `app/src/main/java/com/example/attendanceapp/api/NetworkModule.kt` and update `BASE_URL`

4. **Build and run**
   ```bash
   ./gradlew assembleDebug
   ```
   Or use the Run button in Android Studio to install on a device/emulator

## Permissions

The app requests:
- **Location** (fine, coarse, background) – for presence verification and logging
- **Notification** – for background logging status
- **Phone state** – for device identification (IMEI)
- **WiFi state** – for organization SSID verification

These are requested during onboarding and when needed.

## Project Structure

```
app/src/main/java/com/example/attendanceapp/
├── api/           # API models, Retrofit service, network config
├── data/          # EmployeeDataManager, OrgDataManager, DataStoreManager
├── navigation/    # Compose navigation routes
├── screens/       # Login, Employee, Org, Onboarding, etc.
├── ui/theme/      # Material theme, colors, typography
├── utils/         # DeviceUtils, LocationUtils
└── worker/        # LogStatusWorker, LogStatusForegroundService
```

## API Endpoints

| Endpoint         | Purpose                    |
|------------------|----------------------------|
| `ios_emp_login`  | Employee login (phone, date, IMEI) |
| `ios_org_login`  | Organization login         |
| `log_status`     | Background status logging  |
| `mark_attendance`| Mark attendance            |

## License

Not specified.
