# Virto Commerce (virto-commerce)

Virto Commerce is an open-source, API-first B2B e-commerce platform built on .NET Core. It provides REST and GraphQL APIs for catalog management, pricing, inventory, order management, customer organizations, marketing, payments, shipping, subscriptions, and complex B2B purchasing workflows including quotes, contracts, and approval routing. The modular architecture offers 100+ independently deployable modules covering the full commerce stack for enterprise deployments.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/virto-commerce/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/virto-commerce/refs/heads/main/apis.yml)

## Tags

- B2B E-Commerce
- Catalog Management
- Order Management
- Pricing
- Inventory
- Shopping Cart
- Customer Management
- Marketing
- Payments
- Shipping
- Subscriptions
- Headless Commerce
- Open Source
- .NET

## Timestamps

- **Created:** 2026-06-13
- **Modified:** 2026-06-13

## APIs

### Virto Commerce Catalog API

Product information management API for managing catalogs, categories, products, variations, properties, and attributes. Supports master and virtual catalogs, multi-language content, digital and physical products, and full-text search.

- **Human URL:** [https://docs.virtocommerce.org/](https://docs.virtocommerce.org/)
- **Base URL:** `https://virtostart-demo-admin.govirto.com/api`

#### Tags

- Catalog
- Products
- Categories
- PIM

#### Properties

- [Documentation](https://docs.virtocommerce.org/)
- [OpenAPI](https://virtostart-demo-admin.govirto.com/docs/v3/VirtoCommerce.Catalog) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GitHub Repository](https://github.com/VirtoCommerce/vc-module-catalog)
- [Graph Q L](graphql/virto-commerce-graphql.md)

### Virto Commerce Pricing API

Robust pricing management API based on price lists and dynamic evaluation. Supports tier pricing, bulk pricing, contract-based pricing, personalized pricing, promotions, and price list assignments across stores and customer segments.

- **Human URL:** [https://docs.virtocommerce.org/](https://docs.virtocommerce.org/)
- **Base URL:** `https://virtostart-demo-admin.govirto.com/api`

#### Tags

- Pricing
- Price Lists
- Tiers
- Promotions

#### Properties

- [Documentation](https://docs.virtocommerce.org/)
- [OpenAPI](https://virtostart-demo-admin.govirto.com/docs/v3/VirtoCommerce.Pricing) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GitHub Repository](https://github.com/VirtoCommerce/vc-module-pricing)

### Virto Commerce Inventory API

Product inventory management API for tracking stock levels, fulfillment centers, reservations, and availability across multiple warehouses and locations.

- **Human URL:** [https://docs.virtocommerce.org/](https://docs.virtocommerce.org/)
- **Base URL:** `https://virtostart-demo-admin.govirto.com/api`

#### Tags

- Inventory
- Stock
- Warehouses
- Fulfillment

#### Properties

- [Documentation](https://docs.virtocommerce.org/)
- [OpenAPI](https://virtostart-demo-admin.govirto.com/docs/v3/VirtoCommerce.Inventory) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GitHub Repository](https://github.com/VirtoCommerce/vc-module-inventory)

### Virto Commerce Order Management API

Document-based flexible order management API supporting complex B2B order flows. Manages orders, payments, shipments, refunds, invoices, split shipments, draft orders, and approval workflows with full audit history.

- **Human URL:** [https://docs.virtocommerce.org/](https://docs.virtocommerce.org/)
- **Base URL:** `https://virtostart-demo-admin.govirto.com/api`

#### Tags

- Orders
- Payments
- Shipments
- OMS
- B2B

#### Properties

- [Documentation](https://docs.virtocommerce.org/)
- [OpenAPI](https://virtostart-demo-admin.govirto.com/docs/v3/VirtoCommerce.Orders) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GitHub Repository](https://github.com/VirtoCommerce/vc-module-order)

### Virto Commerce Shopping Cart API

Shopping cart and checkout API supporting complex B2B cart scenarios including multi-line items, coupons, promotions, tax calculations, split shipments, and cart sharing for collaborative purchasing.

- **Human URL:** [https://docs.virtocommerce.org/](https://docs.virtocommerce.org/)
- **Base URL:** `https://virtostart-demo-admin.govirto.com/api`

#### Tags

- Cart
- Checkout
- Shopping

#### Properties

- [Documentation](https://docs.virtocommerce.org/)
- [OpenAPI](https://virtostart-demo-admin.govirto.com/docs/v3/VirtoCommerce.Cart) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GitHub Repository](https://github.com/VirtoCommerce/vc-module-x-cart)

### Virto Commerce Customer API

Customer contact and organization management API. Supports B2B company hierarchies, contacts, roles, delegated purchasing permissions, login-on-behalf, and multi-account structures for enterprise B2B commerce.

- **Human URL:** [https://docs.virtocommerce.org/](https://docs.virtocommerce.org/)
- **Base URL:** `https://virtostart-demo-admin.govirto.com/api`

#### Tags

- Customers
- Contacts
- Organizations
- CRM
- B2B

#### Properties

- [Documentation](https://docs.virtocommerce.org/)
- [OpenAPI](https://virtostart-demo-admin.govirto.com/docs/v3/VirtoCommerce.Customer) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GitHub Repository](https://github.com/VirtoCommerce/vc-module-customer)

### Virto Commerce Marketing API

Marketing and promotions management API for dynamic content, discount rules, coupon campaigns, banners, and promotion engines applied across catalog, cart, and checkout workflows.

- **Human URL:** [https://docs.virtocommerce.org/](https://docs.virtocommerce.org/)
- **Base URL:** `https://virtostart-demo-admin.govirto.com/api`

#### Tags

- Marketing
- Promotions
- Coupons
- Discounts

#### Properties

- [Documentation](https://docs.virtocommerce.org/)
- [OpenAPI](https://virtostart-demo-admin.govirto.com/docs/v3/VirtoCommerce.Marketing) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GitHub Repository](https://github.com/VirtoCommerce/vc-module-marketing)

### Virto Commerce Quotes API

Quote request and approval workflow API enabling B2B buyers to initiate quote requests online, negotiate pricing, obtain approvals, and convert approved quotes directly into orders.

- **Human URL:** [https://docs.virtocommerce.org/](https://docs.virtocommerce.org/)
- **Base URL:** `https://virtostart-demo-admin.govirto.com/api`

#### Tags

- Quotes
- RFQ
- Approvals
- B2B

#### Properties

- [Documentation](https://docs.virtocommerce.org/)
- [OpenAPI](https://virtostart-demo-admin.govirto.com/docs/v3/VirtoCommerce.Quote) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GitHub Repository](https://github.com/VirtoCommerce/vc-module-quote)

### Virto Commerce Store API

Multi-store management API for configuring individual store settings, currencies, languages, payment methods, shipping providers, and SEO per storefront in a multi-tenant commerce architecture.

- **Human URL:** [https://docs.virtocommerce.org/](https://docs.virtocommerce.org/)
- **Base URL:** `https://virtostart-demo-admin.govirto.com/api`

#### Tags

- Store
- Multi-Store
- Configuration

#### Properties

- [Documentation](https://docs.virtocommerce.org/)
- [OpenAPI](https://virtostart-demo-admin.govirto.com/docs/v3/VirtoCommerce.Store) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GitHub Repository](https://github.com/VirtoCommerce/vc-module-store)

### Virto Commerce Platform API

Core platform REST API providing access to security, users, roles, settings, modules, jobs, notifications, export/import, and system administration functions. All platform capabilities accessible via REST and documented via Swagger/OpenAPI.

- **Human URL:** [https://docs.virtocommerce.org/](https://docs.virtocommerce.org/)
- **Base URL:** `https://virtostart-demo-admin.govirto.com/api`

#### Tags

- Platform
- Security
- Administration
- Settings

#### Properties

- [Documentation](https://docs.virtocommerce.org/)
- [OpenAPI](https://virtostart-demo-admin.govirto.com/docs/v3/VirtoCommerce.Platform) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GitHub Repository](https://github.com/VirtoCommerce/vc-platform)

## Common Properties

- [Website](https://virtocommerce.com/)
- [Documentation](https://docs.virtocommerce.org/)
- [Git Hub Org](https://github.com/VirtoCommerce)
- [LinkedIn](https://www.linkedin.com/company/virto-commerce/)
- [Blog](https://virtocommerce.com/blog)
- [Pricing](https://virtocommerce.com/virto-commerce-cloud)
- [X (Twitter)](https://x.com/VirtoCommerce)
- [Plans](plans/virto-commerce-plans-pricing.yml)
- [Rate Limits](rate-limits/virto-commerce-rate-limits.yml)
- [Fin Ops](finops/virto-commerce-finops.yml)
- [Swagger U I](https://virtostart-demo-admin.govirto.com/docs/index.html)
- [Support](https://help.virtocommerce.com/support/home)
- [Community](https://www.virtocommerce.org/)
- [Changelog](https://www.virtocommerce.org/c/news-digest/14)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
