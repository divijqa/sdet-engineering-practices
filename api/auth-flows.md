# Auth Flows

Authentication and authorization tests verify identity, session behavior, and access policy across supported clients.

## Coverage

Cover valid and invalid credentials, token expiry, refresh and logout, role permissions, tenant boundaries, missing or malformed credentials, and sensitive resource access. Use synthetic accounts and secrets from the CI secret store. Never commit tokens or rely on shared mutable identities in parallel tests.
