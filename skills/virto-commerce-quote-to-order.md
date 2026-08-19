---
name: virto-commerce-quote-to-order
description: >-
  Run the B2B quote negotiation loop in Virto Commerce — create a quote request, recalculate
  totals after a price concession, move it through status, and convert the accepted quote into
  a sales order.
api: Virto Commerce Quotes API
generated: '2026-08-13'
method: generated
source: >-
  openapi/virto-commerce-quotes-api-openapi.yml,
  openapi/virto-commerce-order-management-api-openapi.yml,
  graphql/virto-commerce-schema.graphql
operations:
  - QuoteModule_Create
  - QuoteModule_Search
  - QuoteModule_GetById
  - QuoteModule_Update
  - QuoteModule_CalculateTotals
  - QuoteModule_UpdateStatus
  - QuoteModule_GetShipmentMethods
  - QuoteModule_CreateOrderFromQuote
---

# Quote to order

Quoting is the flow that distinguishes Virto's B2B model from a B2C checkout: the buyer asks,
an internal user negotiates price, and only then does an order exist. Authenticate first (see
`virto-commerce-authenticate`).

## 1. Create the quote request

```
POST /api/quote/requests             # QuoteModule_Create
```

`QuoteRequest` is a document aggregate like an order — `items`, `addresses`, `attachments`,
`taxDetails` and `dynamicProperties` all live inline. Set `customerId`, `organizationId` and
`storeId`; `employeeId` identifies the internal user handling it.

## 2. Find and read quotes

```
POST /api/quote/requests/search      # QuoteModule_Search
GET  /api/quote/requests/{id}        # QuoteModule_GetById
```

Search takes a criteria body with the standard `skip` / `take` / `sort` triple and returns
`{ totalCount, results[] }`.

## 3. Negotiate — set prices, then recalculate

```
PUT /api/quote/requests              # QuoteModule_Update
PUT /api/quote/requests/recalculate  # QuoteModule_CalculateTotals
```

The internal user sets prices for quantity breaks or discounts on the quote items. **Call
recalculate after any line change** — totals, taxes and fees are server-computed, and a quote
whose items were edited without a recalculation carries stale totals into the order.

Attachments are part of the negotiation record:
`GET /api/quote/requests/attachments/options` (`QuoteModule_GetAttachmentOptions`) tells you
what the deployment accepts before you upload.

## 4. Resolve shipping options

```
GET /api/quote/requests/{id}/shipmentmethods   # QuoteModule_GetShipmentMethods
```

Methods are resolved per quote — they depend on the store, the addresses on the quote, and the
fulfillment centers configured on that store.

## 5. Move status

```
PUT /api/quote/requests/{id}/status  # QuoteModule_UpdateStatus
```

Status values are deployment-configurable (the platform ships a state machine module and
operators extend it), so read the current value from the quote rather than hard-coding a
vocabulary.

## 6. Convert to an order

```
POST /api/quote/requests/{id}/order  # QuoteModule_CreateOrderFromQuote
```

This is the one place you should NOT build the order yourself. Converting server-side carries
the negotiated prices, addresses and line structure across intact. Building an order manually
from quote fields re-evaluates pricing and silently discards the concession that was the whole
point of the quote.

After conversion, re-read the order with `OrderModule_GetById` to pick up its generated
`number` and totals.

## Storefront equivalent

If you are acting as the buyer-facing application rather than the back office, the same flow
exists in the GraphQL xAPI with buyer-shaped semantics: `createQuote`, `createQuoteFromCart`,
`addQuoteItems`, `changeQuoteItemQuantity`, `submitQuoteRequest`, `approveQuoteRequest`,
`declineQuoteRequest`, `cancelQuoteRequest`. Those mutations enforce buyer permissions; the
REST operations above are the administrative side. Do not mix the two in one flow.

## Notes

- No idempotency keys anywhere — set `outerId` on the quote and search on it before retrying a
  create.
- 403 with an empty body means a missing platform permission, not a malformed request.
