## 4. Transaction Guarantee Company — Funds & Identity

Called by AI Agents. Consumers interact indirectly through their AI Agent. **Those who touch money never evaluate.**
Also responsible for JWT issuance and revocation — serving as the identity anchor of the entire ecosystem.

```
Guarantee company root: https://guarantee.<provider-domain>/v1
```

### 4.0 Public Key Endpoints

```http
GET /.well-known/jwks.json
```

No authentication required. Returns the current list of valid signing public keys.

```http
GET /.well-known/jwt-revoked?since=1700000000
```

No authentication required. Returns the list of `jti`s revoked since the `since` timestamp.

### 4.1 Create Account (Issue First JWT)

```http
POST /v1/accounts
Content-Type: application/json

{
  "real_name": "<end-to-end encrypted>",
  "id_number": "<end-to-end encrypted>"
}
```

Use case: Consumer uses this guarantee company for the first time; completes KYC and opens an account.

```json
// Response data (code: 200)
{
  "account_id": "acct_abc123",
  "user_pseudonym": "user_7xk3a",
  "access_token": "eyJhbGciOiJFUzI1NiIs...",
  "expires_in": 86400
}
```

The `access_token` is the first issued JWT, with `sub` = `user_pseudonym`. The user hands this token to the AI Agent.

### 4.2 Refresh Token

```http
POST /v1/auth/refresh
Authorization: Bearer <soon-to-expire token>
```

Use case: Token is about to expire; AI Agent refreshes on behalf of the user.

```json
// Response data (code: 200)
{
  "access_token": "eyJhbGciOiJFUzI1NiIs...",
  "expires_in": 86400
}
```

### 4.3 Create Transaction (Place Order)

```http
POST /v1/transactions
Authorization: Bearer <buyer token (sub = user_pseudonym)>
Content-Type: application/json

{
  "manufacturer_id": "mfr_alpine_gear",
  "product_id": "prod_001",
  "product_name": "Ultralight Waterproof Jacket",
  "price": 89900,
  "shipping_fee": 0,
  "shipping_method": "SF Express, 1-3 days",
  "guarantee_company_id": "guarantee_co_a",
  "buyer_signature": "base64url_encoded"
}
```

Use case: User confirms the order. Process: Verify JWT → Lock snapshot → Check balance → Transfer funds to escrow → Return transaction hash.

```json
// Response data (code: 200, payment successful)
{
  "transaction_hash": "0xtx_abc",
  "snapshot": {
    "transaction_hash": "0xtx_abc",
    "buyer_pseudonym": "user_7xk3a",
    "manufacturer_id": "mfr_alpine_gear",
    "product_id": "prod_001",
    "product_name": "Ultralight Waterproof Jacket",
    "price": 89900,
    "shipping_fee": 0,
    "shipping_method": "SF Express, 1-3 days",
    "guarantee_fee": 899,
    "guarantee_company_id": "guarantee_co_a",
    "status": "PAID",
    "created_at": 1700000000,
    "updated_at": 1700000000,
    "snapshot_hash": "0xsnap_abc"
  }
}
```

```json
// Response (code: 422, payment failed)
{
  "code": 422,
  "msg": "Insufficient balance. Current balance: 5000 cents; required: 90799 cents (including guarantee fee of 899 cents)",
  "data": {
    "error_code": "INSUFFICIENT_BALANCE",
    "current_balance": 5000,
    "required": 90799
  }
}
```

### 4.4 Confirm Receipt

```http
POST /v1/transactions/{transaction_hash}/confirm
Authorization: Bearer <buyer token>
Content-Type: application/json

{
  "buyer_signature": "base64url_encoded"
}
```

Use case: Buyer confirms after satisfactory receipt; funds are released from escrow to the manufacturer. Auto-released if not confirmed within the timeout.

### 4.5 File Dispute

```http
POST /v1/transactions/{transaction_hash}/dispute
Authorization: Bearer <buyer or manufacturer token>
Content-Type: application/json

{
  "complainant_id": "user_7xk3a",
  "reason": "Fabric does not match description — advertised as GORE-TEX but is actually ordinary nylon",
  "evidence_urls": ["https://img.example.com/evidence_1.jpg"]
}
```

Use case: Disputes over product not matching description, quality issues, etc. The guarantee company arbitrates based on the transaction snapshot, referencing both parties' reputation scores from certification companies.

### 4.6 Query Guarantee Rate

```http
GET /v1/guarantee-rate?manufacturer_id=mfr_alpine_gear&amount=89900
```

No authentication required. Use case: AI Agent displays fee breakdown before placing an order.

```json
// Response data
{
  "rate": 0.01,
  "fee": 899,
  "avg_payout_hours": 4.2
}
```

### 4.7 Query Transaction Snapshot

```http
GET /v1/transactions/{transaction_hash}
Authorization: Bearer <user or guarantee company token>
```

Use case: View order details; certification companies retrieve the original promises made at the time of ordering for arbitration purposes.

### 4.8 List Transactions (Paginated)

```http
GET /v1/transactions?page=1&page_size=20&status=CONFIRMED&start_time=1700000000&end_time=1710000000
Authorization: Bearer <buyer token>
```

Use case: User views order history. Constraint: can only query transactions belonging to the token holder (`sub` = `user_pseudonym`).

### 4.9 Manufacturer Records Shipment

```http
POST /v1/transactions/{transaction_hash}/ship
Authorization: Bearer <manufacturer token>
Content-Type: application/json

{
  "tracking_number": "SF1234567890",
  "carrier": "SF Express",
  "manufacturer_signature": "base64url_encoded"
}
```

Use case: After packing and shipping, the manufacturer records the tracking number with the guarantee company. The guarantee company notifies the AI Agent to update the order status.

```json
// Response data
{ "status": "SHIPPED", "updated_at": 1700100000 }
```

---