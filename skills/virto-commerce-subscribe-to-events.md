---
name: virto-commerce-subscribe-to-events
description: >-
  Receive Virto Commerce domain events — register an HTTP webhook against the live event
  catalog, choose the payload properties, verify delivery through the audit feed, or route the
  same events to a message queue as CloudEvents via the Event Bus module.
api: Virto Commerce Webhooks API
generated: '2026-08-13'
method: generated
source: >-
  openapi/virto-commerce-webhooks-api-openapi.yml,
  openapi/virto-commerce-event-bus-api-openapi.yml,
  asyncapi/virto-commerce-webhooks.yml
operations:
  - WebHooks_GetAllRegisteredEvents
  - WebHooks_GetEventObjectProperties
  - WebHooks_SaveWebhooks
  - WebHooks_Search
  - WebHooks_GetWebhookById
  - WebHooks_Run
  - WebHooks_SearchWebhookFeed
  - WebHooks_DeleteWebHooks
  - Subscriptions_Get
  - Subscriptions_CreateSubscription
  - ConnectionsLog_SearchProviderConnectionLog
---

# Subscribe to Virto Commerce events

Both event surfaces require the corresponding module to be installed on the target deployment
(`VirtoCommerce.WebHooks`, `VirtoCommerce.EventBus`). Check first — a 404 on these paths means
the module is not installed, not that you got the path wrong.

## Discover the event catalog — do not guess event names

```
GET /api/webhooks/events        # WebHooks_GetAllRegisteredEvents
```

Virto discovers events by reflecting over every `DomainEvent` type in the platform **and every
installed module at runtime**. There is no static list, and no two deployments necessarily
expose the same one. This endpoint requires authentication (an anonymous probe returns 401), so
you must be authenticated before you can even enumerate what you can subscribe to.

Then, for the event you picked:

```
GET /api/webhooks/properties    # WebHooks_GetEventObjectProperties
```

This returns the entity properties available for that event — the menu you compose a payload
from.

## Register the webhook

```
POST /api/webhooks              # WebHooks_SaveWebhooks
```

Three things to get right:

1. **Payload composition is selective.** You name the specific properties to include, and you
   can include their **previous values** — which is how you do change tracking without diffing
   on your side.
2. **Choose the endpoint authentication.** Supported: None, HTTP Basic, Bearer Token, Custom
   Header.
3. **There is no HMAC signature.** Virto does not sign webhook bodies. Your receiver's only
   authenticity signal is the credential you configured, so use Bearer or a custom header,
   serve HTTPS, and do not treat an unauthenticated POST as trustworthy.

## Test it before you trust it

```
POST /api/webhooks/send         # WebHooks_Run
```

Fires the webhook on demand. Then read the audit feed:

```
POST /api/webhooks/feed/search  # WebHooks_SearchWebhookFeed
```

Every attempt is persisted with request and response headers, body, HTTP status, error message
and attempt count. This feed is the debugging surface — use it instead of guessing why a
receiver never fired.

## Delivery semantics your receiver must handle

- **Debounce**: dispatch is delayed 5 seconds after the event, to collapse rapid sequences.
- **Batching**: webhooks are processed in batches of 20.
- **Retries**: 3 by default (`Webhooks.General.SendRetryCount`), with exponential backoff at
  1, 2 and 4 minutes.
- Therefore: **your receiver must be idempotent.** A retried delivery is a re-POST of the same
  event, and Virto sends no delivery id header for you to de-duplicate on — de-duplicate on
  the entity id plus a timestamp from the payload you composed.

Required permissions: `webhooks:access`, `webhooks:read`, `webhooks:update`, `webhooks:delete`,
`webhooks:feed:read`.

## The other surface: Event Bus (CloudEvents to a queue)

Use this instead of webhooks when you want durable, queue-based fan-out rather than HTTP
callbacks.

```
GET  /api/eventbus/events                 # Subscriptions_Get
POST /api/eventbus/subscriptions          # Subscriptions_CreateSubscription
POST /api/eventbus/logs/search            # ConnectionsLog_SearchProviderConnectionLog
```

- Events are emitted as **CloudEvents** by the built-in Azure Event Grid provider; the provider
  model is pluggable.
- Each subscription takes a **JsonPath filter** (`JsonPathFilter`, default `$` = everything) so
  you filter server-side rather than receiving everything.
- Each subscription can carry a **Liquid/Scriban template** (`PayloadTransformationTemplate`)
  to reshape the payload before it leaves the platform.
- Connections and subscriptions can be declared in `appsettings.json` **or** managed at runtime
  through this API. If an operator declared them in configuration, they will not appear as
  editable records — check both.

## What is not available

- No AsyncAPI document describes either surface.
- No published static event catalog.
- No replay or dead-letter queue beyond the retry policy and the audit/connection logs.
