# Prime Physio monorepo architecture

## Decisions
- npm workspaces monorepo.
- Web: existing React + Vite application, retained at repository root during the first migration increment and exposed through apps/web workspace scripts.
- Mobile: Expo + React Native + Expo Router; one app with patient, physiotherapist and admin role-aware entry points.
- Backend: existing backend remains authoritative. No replacement backend or persistence layer is introduced.
- Shared packages: domain types, API client, validation schemas and design tokens.

## Workspaces
- apps/web: web workspace entry point; current root Vite source is intentionally preserved during migration.
- apps/mobile: native iOS and Android app.
- packages/types: shared role, patient, therapist, appointment and session summary contracts.
- packages/api-client: typed fetch client with bearer-token injection.
- packages/validation: Zod schemas shared across clients.
- packages/design-tokens: platform-neutral palette, spacing, radius and typography.

## Mobile role handling
Authentication must return a trusted role claim from the existing backend. The role selector in the initial sign-in screen is demo-only and MUST be replaced by backend authentication before production. Route guards and server-side authorization are required; hiding a tab is not authorization.

## Native feel
Use React Native primitives and platform conventions, not embedded web pages. Respect safe areas, native system bars, keyboard behavior, touch targets, Android back navigation and iOS navigation gestures. Use platform-specific components when picker, sheet or navigation behavior differs.

## Local development
- npm install
- npm run dev:web
- npm run dev:mobile
- npm run ios
- npm run android

The first mobile increment is a navigable UI scaffold only. API URL, auth endpoints, token lifecycle, role claims and data contracts must be aligned with the existing backend before enabling real sign-in.
