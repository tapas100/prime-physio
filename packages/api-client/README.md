# API client

Create one client instance per application and supply the API base URL from environment configuration. Provide a secure token getter backed by Expo SecureStore on mobile and the existing secure web session mechanism on web. Never store access tokens in AsyncStorage or hardcode secrets. Align paths and response DTOs with the existing backend before use.