---
name: virto-commerce-authenticate
description: >-
  Obtain a token for a Virto Commerce Platform instance and make an authenticated call.
  Establishes the base URL, picks between the OAuth2 token grants and the platform API key,
  and explains what a 401 versus a 403 actually means on this API.
api: Virto Commerce Platform API
generated: '2026-08-13'
method: generated
source: >-
  openapi/virto-commerce-virtocommerce-platform-api-openapi.yml,
  well-known/virto-commerce-openid-configuration.json (probed 2026-08-13),
  authentication/virto-commerce-authentication.yml
operations:
  - Authorization_Exchange
  - StoreModule_GetUserAllowedStores
---

# Authenticate against a Virto Commerce Platform

## Before anything else: find the base URL

Virto Commerce is self-hosted software, not a multi-tenant SaaS API. **There is no global
api.virtocommerce.com.** The base URL is whatever host the operator deployed the platform to,
and every path below hangs off it:

```
<platform-host>/api/...
<platform-host>/connect/token
<platform-host>/graphql
```

Virto's own public reference deployment is `https://virtostart-demo-admin.govirto.com`. Ask the
operator for theirs; never assume one.

Confirm the host is a Virto platform before doing anything else — it serves its discovery
document anonymously:

```
GET <platform-host>/.well-known/openid-configuration
```

## Choose a credential

Two mechanisms work. They are not interchangeable.

**1. OAuth 2.0 token (`Authorization_Exchange`, `POST /connect/token`).** Preferred for
anything acting on behalf of a user or a service identity.

- `grant_type=client_credentials` — service-to-service integration.
- `grant_type=password` — acts as a specific platform user.
- `grant_type=refresh_token` — renew without re-authenticating.

The live discovery document also advertises `authorization_code` (with PKCE `S256`) and two
Virto-specific grants, `impersonate` and `external_sign_in`.

Send the resulting token as `Authorization: Bearer <token>` on every call. Tokens are RS256
JWTs; the signing keys are at `<platform-host>/.well-known/jwks` (note: **not** `jwks.json`).

**2. Platform API key.** Two schemes are declared: `api_key_header` (header) and `api_key`
(query string). Use the header. The query-string variant puts a credential in access logs and
should be avoided.

The MCP adapter and most machine integrations use the API key path; it is the one that carries
platform permissions without a user session.

## Then verify the identity actually works

```
GET /api/stores/allowed/{userId}     # StoreModule_GetUserAllowedStores
```

This returns the stores the principal may act on — which is exactly the scoping you need
before any catalog, order or pricing call, since almost every search criteria takes
`storeId`/`storeIds`.

## Reading failures correctly

Virto's 401 and 403 mean different things and both come back with an **empty body** — there is
no error document to parse.

- **401** — no token, expired token, or missing API key. Re-authenticate.
- **403** — you are authenticated but the principal lacks the *module permission* the
  operation requires. Virto permissions are colon-namespaced strings (`webhooks:read`,
  `webhooks:update`). **These are not in the OpenAPI**, so you cannot discover the required
  permission programmatically — read the module's docs or grant broader role permissions in
  the platform's Security section.
- **405** with an `Allow` header — right path, wrong method.

Only one error body in the entire API has a schema: `POST /connect/token` returns
`OpenIddictResponse` with standard OAuth `error` / `errorDescription` / `errorUri` fields. If
authentication itself fails, that is the one place you get a readable reason.

## What is NOT here

- No OAuth **scopes** for API authorization. `scopes_supported` is `["openid",
  "offline_access"]` only — access control is Virto's permission system, not scopes.
- No idempotency keys. A retried `POST` can duplicate. See
  `conventions/virto-commerce-conventions.yml`.
- No rate-limit headers. Any throttling you hit was configured by the operator's gateway, and
  it will not tell you when to retry.
