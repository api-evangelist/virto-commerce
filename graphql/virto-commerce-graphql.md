# Virto Commerce GraphQL API

## Description

Virto Commerce exposes a unified GraphQL API (the "Experience API" or xAPI) as the primary interface for headless storefronts. Built on top of the GraphQL.NET library, the xAPI aggregates catalog, cart, order, and customer data into a single composable endpoint suited for B2B commerce frontends.

The GraphQL layer is implemented across a set of open-source modules:
- **vc-module-x-catalog** — product and category queries
- **vc-module-x-cart** — cart and wishlist queries and mutations
- **vc-module-x-order** — order queries and payment mutations
- **vc-module-profile-experience-api** — customer (contact/organization) queries and mutations
- **vc-module-x-api** — core infrastructure (auth, middleware, settings)

## Endpoint

```
POST /graphql
```

Demo / sandbox:
```
https://demo.virtocommerce.com/graphql
```

A GraphQL Playground (GraphiQL) is available at:
```
https://<your-store>/graphql/ui
```

## Authentication

Most read queries are public. Authenticated mutations (cart management, order placement, profile updates) require a bearer token obtained via the platform's OAuth2/OpenID Connect flow:
```
POST /connect/token
```

Pass the token as a header:
```
Authorization: Bearer <token>
```

## Key Query Roots

| Query | Description |
|---|---|
| `product(id, storeId, currencyCode, cultureName)` | Single product by ID |
| `products(storeId, query, filter, sort, facet, ...)` | Product search with faceting and pagination |
| `category(id, storeId, cultureName)` | Single category by ID |
| `categories(storeId, query, filter, sort, ...)` | Category search with pagination |
| `cart(storeId, userId, currencyCode, cultureName, cartName, cartType)` | Active shopping cart |
| `wishlists(storeId, userId, currencyCode, cultureName)` | Customer wishlists |
| `order(id, number)` | Single order by ID or order number |
| `orders(filter, sort, cultureName, userId)` | Order history connection |
| `me` | Authenticated user / contact profile |
| `organizations` | B2B organization list |
| `contacts` | Customer contact list |

## Key Mutation Roots

| Mutation | Description |
|---|---|
| `addItem` | Add product to cart |
| `addItems` | Bulk add items to cart |
| `changeCartItemQuantity` | Update cart line item quantity |
| `removeCartItem` | Remove item from cart |
| `addCoupon` / `removeCoupon` | Apply or remove discount coupon |
| `addOrUpdateCartAddress` | Set cart billing/shipping address |
| `addOrUpdateCartShipment` | Configure shipment on cart |
| `addOrUpdateCartPayment` | Configure payment on cart |
| `createOrderFromCart` | Convert cart to order |
| `changeOrderStatus` | Update order status |
| `initializePayment` / `authorizePayment` | Payment gateway integration |
| `createWishlist` / `addWishlistItem` / `removeWishlistItem` | Wishlist management |
| `createContact` / `updateContact` / `deleteContact` | Contact management |
| `createOrganization` / `updateOrganization` | B2B organization management |
| `updateMemberAddresses` | Address book management |
| `registerByInvitation` | Invited user registration |
| `changePassword` / `resetPasswordByToken` | Password management |

## Documentation

- Developer docs: https://docs.virtocommerce.org/
- GraphQL / xAPI overview: https://docs.virtocommerce.org/platform/developer-guide/GraphQL-Storefront-API-Reference-xAPI/
- Source — catalog module: https://github.com/VirtoCommerce/vc-module-x-catalog
- Source — cart module: https://github.com/VirtoCommerce/vc-module-x-cart
- Source — order module: https://github.com/VirtoCommerce/vc-module-x-order
- Source — profile module: https://github.com/VirtoCommerce/vc-module-profile-experience-api
- Source — core xAPI: https://github.com/VirtoCommerce/vc-module-x-api
