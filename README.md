# Prime Physio

Role-based physiotherapy management for patients, physiotherapists and administrators.

## Architecture
Prime Physio is an npm-workspaces monorepo with a React web client, an Expo/React Native iOS + Android client, and shared TypeScript packages. The existing backend remains the system of record.

## Workspaces
- `apps/web` — existing React + Vite web experience (source retained at repository root during incremental migration).
- `apps/mobile` — Expo Router app for Android and iOS.
- `packages/types` — shared domain contracts.
- `packages/api-client` — shared HTTP client.
- `packages/validation` — shared Zod validation.
- `packages/design-tokens` — shared brand tokens.

## Requirements
Node.js 20+ and npm 10+ recommended.

## Getting started
```bash
npm install
npm run dev:web
npm run dev:mobile
```

For device simulators:
```bash
npm run ios
npm run android
```

Read [docs/monorepo-architecture.md](docs/monorepo-architecture.md) before integrating authentication or API endpoints.

**Security note:** the mobile role picker is demo navigation only. Production role assignment must come from the authenticated backend session, with authorization enforced server-side.
