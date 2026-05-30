## 2. Merchant DNS — Registration & Search

Called by AI Agents, manufacturers, and other DNS nodes. Public queries require no authentication; registration/deregistration requires a manufacturer token.

```
DNS root: https://dns.<provider-domain>/v1
```

### 2.1 Register Manufacturer

```http
POST /v1/manufacturers
Authorization: Bearer <manufacturer token (issued by guarantee company)>
Content-Type: application/json

{
  "manufacturer_id": "mfr_alpine_gear",
  "name": "Alpine Outdoor Gear Co., Ltd.",
  "api_root_url": "https://api.alpine-gear.example.com/v1",
  "categories": ["Outdoor Gear", "Sportswear"],
  "region": "Zhejiang, Hangzhou"
}
```

Use case: Manufacturer joins the ecosystem for the first time, or migrates from another DNS.
Constraint: A manufacturer may only be registered with one DNS at a time. If already registered elsewhere, deregistration must be requested first.

```json
// Response data (code: 200)
{ "success": true }
// Response (code: 409)
{ "success": false, "conflict_dns_id": "dns_provider_b" }
```

### 2.2 Request Deregistration

```http
POST /v1/manufacturers/{manufacturer_id}/deregister
Authorization: Bearer <manufacturer token>
Content-Type: application/json

{
  "reason": "Switching DNS provider",
  "target_dns_id": "dns_provider_b"
}
```

Process: Submit request → DNS review → upon approval, Sync broadcast → manufacturer may then register with the new DNS.

```json
// Response data
{
  "status": "APPROVED",
  "message": "Deregistration approved, Sync protocol broadcast sent"
}
```

### 2.3 Get Manufacturer Info

```http
GET /v1/manufacturers/{manufacturer_id}
```

Use case: AI Agent views manufacturer details.

### 2.4 Search Manufacturers

```http
GET /v1/manufacturers/search?keyword=jacket&categories=Outdoor%20Gear&region=Zhejiang&page=1&page_size=20
```

Use case: AI Agent searches for manufacturers matching the user's product category needs.

### 2.5 DNS-to-DNS Incremental Sync

```http
GET /v1/sync?since=1700000000&page=1&page_size=100
Authorization: Bearer <DNS node token>
```

Use case: Other DNS nodes pull incremental changes. Use `since=0` for a full sync.

```json
// Response data
{
  "page": 1, "page_size": 100, "total": 12, "total_pages": 1,
  "items": [
    { "action": "register", "entry": { "manufacturer_id": "mfr_new", ... } },
    { "action": "deregister", "entry": { "manufacturer_id": "mfr_old", ... } }
  ],
  "has_more": false
}
```

---