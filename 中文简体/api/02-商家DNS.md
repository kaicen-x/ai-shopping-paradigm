## 2. 商家DNS — 注册与搜索

供 AI Agent、厂家和其他 DNS 调用。公开查询无需认证，注册/注销需厂家令牌。

```
DNS 根地址：https://dns.<提供商域名>/v1
```

### 2.1 注册厂家

```http
POST /v1/manufacturers
Authorization: Bearer <厂家令牌（由担保公司签发）>
Content-Type: application/json

{
  "manufacturer_id": "mfr_alpine_gear",
  "name": "高山户外装备有限公司",
  "api_root_url": "https://api.alpine-gear.example.com/v1",
  "categories": ["户外装备", "运动服饰"],
  "region": "浙江杭州"
}
```

使用场景：厂家首次接入生态，或从其他 DNS 迁移至此。
约束：同一厂家只能在一个 DNS 注册。若已在其他 DNS 注册，需先申请注销。

```json
// Response data (code: 200)
{ "success": true }
// Response (code: 409)
{ "success": false, "conflict_dns_id": "dns_provider_b" }
```

### 2.2 申请注销

```http
POST /v1/manufacturers/{manufacturer_id}/deregister
Authorization: Bearer <厂家令牌>
Content-Type: application/json

{
  "reason": "更换DNS服务商",
  "target_dns_id": "dns_provider_b"
}
```

流程：提交申请 → DNS 审核 → 批准后 Sync 广播 → 厂家方可向新 DNS 注册。

```json
// Response data
{
  "status": "APPROVED",
  "message": "注销已批准，Sync 协议已广播"
}
```

### 2.3 获取厂家信息

```http
GET /v1/manufacturers/{manufacturer_id}
```

使用场景：AI Agent 查看厂家详情。

### 2.4 搜索厂家

```http
GET /v1/manufacturers/search?keyword=冲锋衣&categories=户外装备&region=浙江&page=1&page_size=20
```

使用场景：AI Agent 根据用户需求搜索匹配品类的厂家。

### 2.5 DNS 间增量同步

```http
GET /v1/sync?since=1700000000&page=1&page_size=100
Authorization: Bearer <DNS节点令牌>
```

使用场景：其他 DNS 节点拉取增量变更。`since=0` 获取全量。

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