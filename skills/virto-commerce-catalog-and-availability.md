---
name: virto-commerce-catalog-and-availability
description: >-
  Answer "can this buyer get this product, at what price, from where" in Virto Commerce —
  search the indexed catalog, resolve variations, read inventory across fulfillment centers,
  and evaluate customer-specific pricing.
api: Virto Commerce Catalog API
generated: '2026-08-13'
method: generated
source: >-
  openapi/virto-commerce-catalog-api-openapi.yml, openapi/virto-commerce-inventory-api-openapi.yml,
  openapi/virto-commerce-pricing-api-openapi.yml, openapi/virto-commerce-store-api-openapi.yml,
  data-model/virto-commerce-data-model.yml
operations:
  - CatalogModuleIndexedSearch_SearchProducts
  - CatalogModuleIndexedSearch_GetProductSuggestions
  - CatalogModuleProducts_GetProductById
  - CatalogModuleProducts_GetByCodes
  - CatalogModuleProducts_GetProductByOuterId
  - InventoryModule_SearchInventories
  - InventoryModule_GetProductInventories
  - InventoryModule_SearchFulfillmentCenters
  - PricingModule_EvaluatePrices
  - PricingModule_EvaluateProductPrices
  - StoreModule_GetStoreById
---

# Catalog, inventory and price for a buyer

Three separate modules answer this question and none of them answers it alone. Authenticate
first (see `virto-commerce-authenticate`) and get a `storeId` — it scopes all three.

## 1. Establish the store context

```
GET /api/stores/{id}            # StoreModule_GetStoreById
```

Read `mainFulfillmentCenterId` and `additionalFulfillmentCenterIds`. **Store is the
multi-tenancy axis** in Virto: it determines which fulfillment centers count as "available",
which catalog is in scope, and which pricelist assignments apply. Availability computed
without a store is meaningless.

## 2. Find products

```
POST /api/catalog/search/products              # CatalogModuleIndexedSearch_SearchProducts
POST /api/catalog/search/products/suggestions   # CatalogModuleIndexedSearch_GetProductSuggestions
```

This is the indexed search (Elasticsearch/OpenSearch/Lucene depending on the deployment) and
the one to use for anything user-facing. It takes `skip`/`take`/`sort` and returns
`{ totalCount, results[] }`.

To resolve known identifiers instead of searching:

```
POST /api/catalog/{catalogId}/products-by-codes  # CatalogModuleProducts_GetByCodes
GET  /api/catalog/products/{id}                  # CatalogModuleProducts_GetProductById
GET  /api/catalog/products/outer/{outerId}       # CatalogModuleProducts_GetProductByOuterId
```

`GetProductByOuterId` is the one to reach for when your system of record is an ERP or PIM —
`outerId` is the external-correlation slot on every Virto entity.

Widen or narrow the returned graph with `responseGroup` (spelled `respGroup` and
`ResponseGroup` in some modules — check the operation's own parameter name). Requesting the
default group and then complaining that `variations` or `properties` are missing is the most
common mistake here.

**Variations are products.** A variant is a `CatalogProduct` whose `mainProductId` points at
its parent. There is no separate SKU type — so "get variants" is a product search filtered by
`mainProductId`, and a SKU lookup can return either level.

## 3. Read inventory

```
POST /api/inventory/search                  # InventoryModule_SearchInventories
GET  /api/inventory/products                # InventoryModule_GetProductInventories
POST /api/inventory/fulfillmentcenters/search  # InventoryModule_SearchFulfillmentCenters
```

Inventory is held **per product per fulfillment center**, not per product. A single "available
quantity" number does not exist in the data — you compute it by summing the centers that the
store in step 1 actually draws from. Virto's own MCP adapter does exactly this: resolve SKUs to
product ids, search inventory, then calculate availability client-side.

## 4. Evaluate the price — never read it off the product

```
POST /api/pricing/evaluate                  # PricingModule_EvaluatePrices
GET  /api/products/{productId}/prices       # PricingModule_EvaluateProductPrices
```

Send a `PriceEvaluationContext` with `storeId`, `catalogId`, `currency` and `customerId`.

B2B prices come from pricelist assignments resolved against the customer, their organization
and the store. The number on the catalog record is a list price and is frequently not what this
buyer pays. This is the single most consequential rule in this skill.

## Storefront alternative

For buyer-facing reads, the GraphQL xAPI does all four steps in one round trip — the `product`,
`products`, `categories` and `pricesSum` queries return price and availability already resolved
for the authenticated buyer. Endpoint: `POST <platform-host>/graphql`, and it requires a
non-empty `GraphQL-Require-Preflight` header or the server answers 400 with
`extensions.code: CSRF_PROTECTION`. Use the REST operations above for back-office and
integration work; use the xAPI for storefront reads.

## Pitfalls

- Omitting `storeId` — availability and price both become wrong rather than absent.
- Trusting the catalog list price.
- Assuming one inventory row per product.
- Forgetting `responseGroup` and concluding a field does not exist.
- 403 with an empty body is a missing permission, not a bad query.
