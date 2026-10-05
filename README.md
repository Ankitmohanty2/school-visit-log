# School Visit Log

School Visit Log is an Expo + React Native app for field officers to record school visits, even with poor connectivity.

The app supports:
- selecting a field officer profile
- searching schools by name, district, and block
- filling a monthly questionnaire for a selected school
- queueing visit submissions offline
- automatic background sync when network/server become available
- tracking synced, pending, and failed visits in **My Visits**

## Tech Stack

- **React Native** with **Expo**
- **Expo Router** for navigation
- **AsyncStorage** for local/offline persistence
- network awareness via **@react-native-community/netinfo**

## Getting Started

### Prerequisites

- Node.js LTS (recommended)
- npm
- Expo-compatible Android/iOS simulator or a physical device

### Install and run

```bash
cd app
npm install
npm run start
```

Then open the app in:
- Android (`a` in Expo CLI)
- iOS (`i` in Expo CLI, macOS only)
- Web (`w` in Expo CLI)

## Configuration

API base URL can be set with:

```bash
EXPO_PUBLIC_API_URL=http://<your-server>:4000
```

If not provided, the app auto-resolves a local host based on Expo runtime settings.

## Backend API Expectations

The app calls these endpoints under `/api`:
- `GET /health`
- `GET /schools`
- `GET /locations/districts`
- `GET /locations/blocks?districtCode=...`
- `GET /questionnaires/current`
- `GET /visits?userId=...&page=...&limit=...`
- `POST /visits`

## Project Structure

```text
app/
  src/
    app/         # Screens and routes
    api/         # HTTP client + endpoint wrappers
    hooks/       # Data-loading hooks
    offline/     # Offline cache and sync queue
    state/       # User and sync context
    storage/     # AsyncStorage utilities
    utils/       # Validation and date helpers
```

## Offline Behavior

- Visits are first saved to the on-device queue.
- Pending visits are retried automatically when online.
- Permanent server validation failures are marked as **failed** for manual review/removal.
- Last successful school/visit data is reused when server is unavailable.

## Demo Users

The app ships with demo field officer profiles for local testing and flow validation.
