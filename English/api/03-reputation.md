## 3. Reputation Certification Company — Reviews & Certification

Called by AI Agents and Transaction Guarantee Companies. **Those who evaluate never touch the money.**
Reputation queries are free for consumers and AI Agents; guarantee companies pay per query (extremely low pricing, absorbed into the guarantee company's operating costs).

```
Certifier root: https://cert.<provider-domain>/v1
```

### 3.1 Query Single Manufacturer Reputation Score

```http
GET /v1/reputation/{manufacturer_id}
Authorization: Bearer <user token or guarantee company token>
```

Use case: AI Agent displays reputation on the product page (free); guarantee company references it during arbitration (paid).
Pricing: Consumer / AI Agent tokens are free; guarantee company token queries include billing info in the response.

```json
// Response data
{
  "manufacturer_id": "mfr_alpine_gear",
  "score": 892,
  "return_rate": 0.023,
  "avg_delivery_days": 1.8,
  "total_reviews": 1203,
  "updated_at": 1700086400,
  "score_hash": "0xabc123..."
}
```

### 3.2 Batch Query Reputation Scores

```http
POST /v1/reputation/batch
Authorization: Bearer <user token>
Content-Type: application/json

{ "manufacturer_ids": ["mfr_001", "mfr_002", "mfr_003"] }
```

Use case: AI Agent fetches reputation scores for all candidate manufacturers on the search results page for ranking. Max 50 per request.
Caller: AI Agent (free).

### 3.3 Query Product Reputation Score

```http
GET /v1/reputation/product/{product_id}
```

No authentication required. Use case: AI Agent displays the product rating on the product detail page.

```json
// Response data
{
  "product_id": "prod_001",
  "score": 4.6,
  "total_reviews": 87,
  "score_hash": "0xprod_abc..."
}
```

Product-level scores are independently calculated per `content_hash` version — if the manufacturer changes the actual product, the new version's score starts from zero; old version ratings do not carry over. The AI Agent displays a comparison of current and historical version scores to prevent "using old good reviews to sell inferior goods."

Specify a version when querying:
```
GET /v1/reputation/product/{product_id}?content_hash=abc123
```
Omitting the parameter returns the latest version's score.

### 3.4 Query Manufacturer Certification

```http
GET /v1/certifications/{manufacturer_id}
```

No authentication required. Use case: Display certification level and validity period.

```json
// Response data
{
  "certification_id": "cert_deep_2024_001",
  "manufacturer_id": "mfr_alpine_gear",
  "level": "DEEP",
  "auditor": "SGS",
  "issued_at": 1700000000,
  "expires_at": 1731536000,
  "report_hash": "0xdef456..."
}
```

### 3.5 List Reviews (Paginated)

```http
GET /v1/reviews?manufacturer_id=mfr_alpine_gear&rating_min=4&page=1&page_size=20
```

No authentication required. Use case: Display review list on the product detail page. Items with `review_type = FOLLOW_UP` are follow-up reviews.

```json
// Response data item
{
  "review_id": "rev_001",
  "transaction_hash": "0xtx_abc",
  "manufacturer_id": "mfr_alpine_gear",
  "user_pseudonym": "user_7xk3a",
  "rating": 5,
  "content": "Great quality, excellent waterproofing",
  "review_type": "INITIAL",
  "parent_review_id": "",
  "product_content_hash": "0xabc123",
  "created_at": 1700086400
}
```

`review_type` values: `INITIAL` (first review), `FOLLOW_UP` (follow-up review). Follow-up reviews link to the initial review via `parent_review_id`.

### 3.6 Submit Review

```http
POST /v1/reviews
Authorization: Bearer <consumer token>
Content-Type: application/json

{
  "transaction_hash": "0xtx_abc",
  "manufacturer_id": "mfr_alpine_gear",
  "rating": 5,
  "content": "Great quality, excellent waterproofing",
  "user_signature": "base64url_encoded_signature"
}
```

Use case: Consumer reviews after confirming receipt. The certification company queries the guarantee company on its own to verify whether the transaction hash is valid — if valid, the review is accepted and recorded on-chain; if invalid, it is rejected. No need for the guarantee company to "notify unlock" in advance.

```json
// Response data (code: 200)
{ "review_id": "rev_001" }
```

### 3.7 Submit Follow-Up Review

```http
POST /v1/reviews/{review_id}/follow-up
Authorization: Bearer <consumer token>
Content-Type: application/json

{
  "rating": 3,
  "content": "The zipper broke after two months, after-sales refused to handle it",
  "user_signature": "base64url_encoded"
}
```

Use case: After the initial review, the consumer provides a supplementary review on long-term usage experience or after-sales service. Constraints:

- Follow-up reviews can only be submitted within **90 days** of the initial review
- The follow-up is bound to the same `transaction_hash`; the certification company must still verify the transaction validity with the guarantee company
- The follow-up may change the rating (e.g., from 5 stars to 3 stars) — follow-up ratings carry **1.5× weight** compared to the initial review
- Follow-up content is also recorded on-chain and is immutable
- Only **1 follow-up** is allowed per transaction

```json
// Response data
{
  "review_id": "rev_002",
  "review_type": "FOLLOW_UP",
  "parent_review_id": "rev_001"
}
```

Follow-up reviews are displayed below the initial review, labeled "追加评价" (follow-up review). In reputation score calculation, follow-up reviews carry higher weight — long-term experience is more informative than first impressions at unboxing.

### 3.8 Migrate Manufacturer Reputation

```http
POST /v1/reputation/migrate
Authorization: Bearer <manufacturer token>
Content-Type: application/json

{
  "manufacturer_id": "mfr_alpine_gear",
  "target_certifier_id": "cert_company_b",
  "manufacturer_signature": "base64url_encoded"
}
```

Use case: Manufacturer switches certification companies; reputation records follow. Migration fees are paid by the receiving party or the manufacturer.

---