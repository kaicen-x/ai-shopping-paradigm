## 1. Manufacturer — Product API

Deployed by manufacturers. Called by AI Agents and Merchant DNS. Public data, no authentication required.

```
Manufacturer API root: https://api.<manufacturer-domain>/v1
```

### 1.1 Get Single Product

```http
GET /v1/products/{product_id}
```

Use case: AI Agent fetches full product details on the product page.

```json
// Response data
{
  "product_id": "prod_001",
  "name": "Ultralight Waterproof Jacket",
  "description": "GORE-TEX fabric, suitable for high-altitude hiking",
  "image_urls": ["https://img.example.com/001_1.jpg"],
  "price": 89900,
  "stock": 23,
  "category": "Outdoor Gear",
  "specs": { "Fabric": "GORE-TEX 3L", "Weight": "380g" },
  "shipping": [
    { "method": "SF Express", "fee": 0, "days_min": 1, "days_max": 3 }
  ],
  "after_sales": "7-day no-questions return, 1-year warranty",
  "created_at": 1700000000,
  "updated_at": 1700086400
}
```

### 1.2 Batch Get Products

```http
POST /v1/products/batch
Content-Type: application/json

{ "product_ids": ["prod_001", "prod_002", "prod_003"] }
```

Use case: AI Agent fetches multiple product summaries at once on the search results page. Max 50 per request.

```json
// Response data
{
  "products": [
    { "product_id": "prod_001", "name": "...", "price": 89900 },
    { "product_id": "prod_002", "name": "...", "price": 45000 }
  ]
}
```

Non-existent IDs are silently ignored.

### 1.3 List Products (Paginated)

```http
GET /v1/products?page=1&page_size=20&category=Outdoor%20Gear&price_min=10000&price_max=200000&keyword=jacket
```

Use case: Merchant DNS periodic sync; AI Agent category browsing. All query parameters are optional.

### 1.4 Count by Category

```http
GET /v1/products/counts
```

Use case: AI Agent displays product counts per category.

```json
// Response data
{
  "counts": { "Jackets": 45, "Hiking Shoes": 32, "Tents": 18 }
}
```

### 1.5 Receive Order Notification

```http
POST /v1/orders/notify
Authorization: Bearer <guarantee company service token>
Content-Type: application/json

{
  "transaction_hash": "0xtx_abc",
  "product_id": "prod_001",
  "quantity": 1,
  "shipping_address": "<end-to-end encrypted>",
  "buyer_pseudonym": "user_7xk3a",
  "guarantee_company_id": "guarantee_co_a",
  "guarantee_signature": "base64url_encoded"
}
```

Use case: After the Transaction Guarantee Company completes payment, it notifies the manufacturer to ship. The manufacturer verifies the signature before fulfilling.

```json
// Response data
{
  "order_id": "order_001",
  "status": "ACCEPTED"
}
```

---