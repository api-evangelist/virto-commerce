---
name: virto-commerce-place-b2b-order
description: >-
  Create a B2B sales order in Virto Commerce from a customer identifier and a list of SKUs —
  resolve the buyer, resolve SKUs to product ids, evaluate contract pricing, then post the
  order document. This is the exact chain Virto's own MCP adapter runs for create-sales-order.
api: Virto Commerce Order Management API
generated: '2026-08-13'
method: generated
source: >-
  openapi/virto-commerce-order-management-api-openapi.yml,
  openapi/virto-commerce-catalog-api-openapi.yml, openapi/virto-commerce-pricing-api-openapi.yml,
  openapi/virto-commerce-companies-and-contacts-api-openapi.yml,
  https://github.com/VirtoCommerce/vc-onX-adapter/blob/main/docs/API.md
operations:
  - CustomerModule_GetMemberById
  - CustomerModule_SearchMember
  - CatalogModuleIndexedSearch_SearchProducts
  - PricingModule_EvaluatePrices
  - OrderModule_CreateOrder
  - OrderModule_GetById
  - OrderModule_UpdateOrder
  - OrderModule_CalculateTotals
---

# Place a B2B sales order

Authenticate first — see `virto-commerce-authenticate`. You need a `storeId`; without one,
pricing and fulfillment cannot be resolved.

## 1. Resolve the buyer

```
GET  /api/members/{id}          # CustomerModule_GetMemberById
POST /api/members/search        # CustomerModule_SearchMember
```

`Member` is the polymorphic base for every party — Contact, Organization, Vendor, Employee — so
there is no "customer" endpoint. Search returns `{ totalCount, results[] }`.

For B2B, read two fields off the resolved `Contact`: `defaultOrganizationId` and
`currentOrganizationId`. **`currentOrganizationId` is the buy-on-behalf-of axis** — one person
can purchase for several organizations, and it determines which contract pricing applies. Put
it on the order as `organizationId`.

## 2. Resolve SKUs to product ids

```
POST /api/catalog/search/products    # CatalogModuleIndexedSearch_SearchProducts
```

Virto's own adapter does this with a single search using
`searchPhrase: "code:sku1,sku2,sku3"`. Order line items reference product ids, not SKUs, so
this step is not optional.

Variants are self-referential: a variation IS a `CatalogProduct` whose `mainProductId` points
at its parent. If you asked for a SKU and got a product back, check whether it is the parent or
the variation before adding it to the order.

## 3. Evaluate contract pricing

```
POST /api/pricing/evaluate           # PricingModule_EvaluatePrices
```

Send a `PriceEvaluationContext` carrying `storeId`, `catalogId`, `currency` and `customerId`.

**Do not read a price off the product.** B2B prices in Virto are evaluated against pricelist
assignments for that customer, organization and store — the list price on the catalog record
is not what this buyer pays. Skipping this step is how integrations quietly bill the wrong
amount.

## 4. Create the order

```
POST /api/order/customerOrders       # OrderModule_CreateOrder
```

`CustomerOrder` is a **document aggregate**: `items`, `addresses`, `shipments`, `inPayments`,
`discounts` and `taxDetails` are all carried inline on the one object. You post the whole
document, not a set of sub-resources.

Set `customerId`, `organizationId`, `storeId`, and — if this order came from a cart — retain
`shoppingCartId` so the lineage survives. Put any external system's order id in `outerId`;
every top-level Virto entity has that slot, and it is the intended integration key.

Use `PUT /api/order/customerOrders/recalculate` (`OrderModule_CalculateTotals`) if you need
totals recomputed before committing to a payment flow.

### There are no idempotency keys

Virto declares no idempotency header on any of its 452 operations. If `POST
/api/order/customerOrders` times out, **do not blindly retry** — you will create a second
order. Instead, search first:

```
POST /api/order/customerOrders/search   # OrderModule_SearchCustomerOrder
```

filtering on your own `outerId` or `number`. Treat `outerId` as your de-duplication key; it is
the only one you control.

## 5. Update or cancel — read, modify, write, re-read

```
GET /api/order/customerOrders/{id}     # OrderModule_GetById
PUT /api/order/customerOrders          # OrderModule_UpdateOrder
GET /api/order/customerOrders/{id}     # OrderModule_GetById
```

Cancellation is a **status change on the document**, not a dedicated endpoint. So is adding a
shipment (fulfillment) and placing a hold. Always re-fetch after the write: the server
recalculates derived fields and assigns ids to newly-added shipments, and only the re-read
tells you what they are.

## Failure modes worth pre-empting

- **403 with an empty body** — a missing permission, not a bad request. The required
  permission is not expressed in the OpenAPI.
- **Prices look wrong** — you skipped step 3, or sent the wrong `organizationId`.
- **Duplicate orders** — a retry without an `outerId` check.
- **`Accept` header** — every operation also advertises `text/plain` and `text/json`. Send
  `Accept: application/json` explicitly.
