# Virto Commerce (virto-commerce)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
