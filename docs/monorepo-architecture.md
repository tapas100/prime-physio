# Prime Physio monorepo architecture

## Decisions
- npm workspaces monorepo.
- Web: React + TypeScript + Vite in apps/web.
- Mobile: Expo + React Native + Expo Router in apps/mobile; one app supports patient, physiotherapist and admin role workspaces.
- Backend: the existing backend remains the system of record. No replacement backend or new persistence service is introduced.
- Shared packages: domain types, API client, validation schemas and design tokens.

## Workspaces
- apps/web: existing React web UI, migrated from the repository root.
- apps/mobile: native Android and iOS application.
- packages/types: role, patient, physiotherapist, appointment and session-summary contracts.
- packages/api-client: typed HTTP client with bearer-token injection.
- packages/validation: Zod schemas for shared validation.
- packages/design-tokens: platform-neutral color, spacing, radius and typography tokens.

## Mobile routes
- Patient: dashboard, appointments, appointment details, visit history, profile.
- Physiotherapist: today's dashboard, appointment list, appointment details, single appointment session summary.
- Admin: clinic overview, patients, physiotherapists and appointments.

## Security and integration
The demo role chooser is only a navigation preview. Production sign-in must call the existing backend, persist tokens in SecureStore on mobile, and take the role from the verified backend response. Route visibility is not authorization; all permissions must be enforced by the backend.
The API base URL is configurable via EXPO_PUBLIC_API_BASE_URL. Do not invent endpoint paths: map the API client to the existing backend's actual auth and resource contracts before enabling real data.

## Native feel
Use React Native primitives rather than embedded web pages. Respect safe areas, system bars, keyboard behavior, 44px touch targets, Android back navigation and iOS navigation gestures. Use native/platform-specific sheets and pickers where appropriate. Shared domain logic and tokens are shared; platform UI is implemented separately.

## Local development
- npm install
- npm run dev:web
- npm run dev:mobile
- npm run ios
- npm run android

For a physical device, set EXPO_PUBLIC_API_BASE_URL to a backend URL reachable from that device, not localhost.
