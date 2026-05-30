## 1. 生产厂家 — 商品 API

厂家自行部署，AI Agent 和商家DNS 调用。公开数据，无需认证。

```
厂家 API 根地址：https://api.<厂家域名>/v1
```

### 1.1 获取单个商品

```http
GET /v1/products/{product_id}
```

使用场景：AI Agent 在商品详情页获取完整信息。

```json
// Response data
{
  "product_id": "prod_001",
  "name": "超轻防水冲锋衣",
  "description": "GORE-TEX面料，适合高海拔徒步",
  "image_urls": ["https://img.example.com/001_1.jpg"],
  "price": 89900,
  "stock": 23,
  "category": "户外装备",
  "specs": { "面料": "GORE-TEX 3L", "重量": "380g" },
  "shipping": [
    { "method": "顺丰标快", "fee": 0, "days_min": 1, "days_max": 3 }
  ],
  "after_sales": "7天无理由退换，1年质保",
  "created_at": 1700000000,
  "updated_at": 1700086400
}
```

### 1.2 批量获取商品

```http
POST /v1/products/batch
Content-Type: application/json

{ "product_ids": ["prod_001", "prod_002", "prod_003"] }
```

使用场景：AI Agent 搜索结果页一次性拉取多个商品摘要。单次最多 50 个。

```json
// Response data
{
  "products": [
    { "product_id": "prod_001", "name": "...", "price": 89900 },
    { "product_id": "prod_002", "name": "...", "price": 45000 }
  ]
}
```

不存在的 ID 静默忽略。

### 1.3 分页列出商品

```http
GET /v1/products?page=1&page_size=20&category=户外装备&price_min=10000&price_max=200000&keyword=冲锋衣
```

使用场景：商家DNS 定时同步；AI Agent 品类浏览。所有 query 参数可选。

### 1.4 按品类统计

```http
GET /v1/products/counts
```

使用场景：AI Agent 展示各品类商品数量。

```json
// Response data
{
  "counts": { "冲锋衣": 45, "徒步鞋": 32, "帐篷": 18 }
}
```

### 1.5 接收订单通知

```http
POST /v1/orders/notify
Authorization: Bearer <担保公司服务令牌>
Content-Type: application/json

{
  "transaction_hash": "0xtx_abc",
  "product_id": "prod_001",
  "quantity": 1,
  "shipping_address": "<端到端加密>",
  "buyer_pseudonym": "user_7xk3a",
  "guarantee_company_id": "guarantee_co_a",
  "guarantee_signature": "base64url_encoded"
}
```

使用场景：交易担保公司完成收款后，通知厂家发货。厂家验签后开始履约。

```json
// Response data
{
  "order_id": "order_001",
  "status": "ACCEPTED"
}
```

---