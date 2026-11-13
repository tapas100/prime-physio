# Prime Physio Mobile

Expo SDK 52 + React Native application for iOS and Android.

## Run
From the repository root:
```bash
npm install
npm run dev:mobile
```

Then press `i` for the iOS simulator or `a` for an Android emulator. Physical devices can scan the Expo QR code.

## Configuration
Copy `.env.example` to `.env.local` and set `EXPO_PUBLIC_API_BASE_URL` to the existing backend URL reachable from the device. Do not use localhost for a physical phone unless the backend is running on the phone itself.

## Demo workspaces
The sign-in screen currently lets you preview Patient, Physiotherapist and Admin navigation. It does not authenticate or save data. Replace this selector with the existing backend's real sign-in contract before production.

## Routes
- Patient: Home, Appointments, Appointment Details, Visit History, Profile.
- Physiotherapist: Today, Appointments, Appointment Details, Session Summary.
- Admin: Overview, Patients, Physiotherapists, Appointments.

## Native behavior
The app uses native React Native views, Expo Router stack transitions, safe-area handling, Android ripple feedback and iOS/Android haptic selection on the shared primary button. Platform-specific sheets and date/time pickers should be introduced for workflows that need them.
