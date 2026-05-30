# 03 — Business Value & Business Model

## 1. Value for Each Stakeholder

### For Consumers

| Value Point | Details |
|-------------|---------|
| **True Price Comparison** | AI queries all manufacturers in parallel, zero bidding pollution, results ranked purely by user preferences |
| **Lower Prices** | Savings from commissions (15%) and ad fees (20–40%) translate directly into price reductions |
| **Real Reviews** | Reputation scores backed by competing trust companies, encrypted and signed, tamper-proof |
| **Time Saved** | From "spend 30 minutes manually comparing across platforms" to "say one sentence, AI completes it in 10 seconds" |
| **Full Protection** | Trust escrow + preemptive payout; an independent third party underwrites disputes |

### For Manufacturers

| Value Point | Old E-Commerce | New Paradigm |
|-------------|---------------|--------------|
| Platform Commission | 5–15% of GMV | 0% (no platform) |
| Ad / Traffic Fees | 20–40% of sales | 0 (no bidding ads) |
| API Registration Fee | — | Minimal (e.g., tens of dollars/year) |
| Trust Guarantee Fee | — | 0.5–2% of transaction value |
| **Total Cost** | **15–30% of GMV** | **< 3% of GMV** |

- **Pricing Autonomy**: No platform promotion rules to coerce; free to set prices and inventory independently
- **Portable Reputation**: Trust scores are bound to trust companies, not a single platform; they remain valid when switching AI Agents
- **Data Ownership**: Manufacturer owns its API call data and gains clear customer insights

### For Trust Companies

- **Blue Ocean Market**: Currently, no independent third-party transaction guarantee + reputation rating service exists separate from e-commerce platforms anywhere in the world
- **High Margins**: Guarantee fees + certification fees + insurance commissions; no need to build a platform, buy traffic, or maintain product listings
- **Network Effects**: More certified manufacturers → more consumer trust → more transaction guarantee demand
- **Historical Parallel**: Analogous to the gap filled by early escrow payment tools, but more neutral (not bound to any single platform)

### For AI Agent Developers

- **New Traffic Gateway**: Shopping traffic shifts from "open the app" to "tell the AI"; AI Agents become the first touchpoint for purchase decisions
- **Full Competition**: Users can freely switch Agents; winners are determined by service quality, not capital-burning user acquisition
- **Asset-light**: Agents hold no inventory, process no payments, and handle no physical fulfillment

### For Merchant DNS Operators

- **Asset-light Infrastructure**: No product data storage, no fund processing, no logistics involvement — purely API index maintenance
- **Naturally Supports Multiple Operators**: Like internet DNS root server architecture, Merchant DNS inherently supports mutual backup and competition among multiple operators
- **Near-zero Operating Cost**: Compared to traditional e-commerce server and bandwidth costs, DNS operating cost approaches zero

---

## 2. Business Model Panorama

```mermaid
graph TD
    A[Consumer<br/>Free or Subscription] -->|Uses| B[AI Agent<br/>Multiple Competitors]
    B -->|Queries| C[Merchant DNS]
    B -->|Calls| D[Trust Company]
    B -->|Connects| E[Manufacturer Product API]
    C -->|Revenue| C1[Registration Fees]
    C -->|Revenue| C2[Premium Features]
    D -->|Revenue| D1[Certification Fees]
    D -->|Revenue| D2[Guarantee Fees]
    D -->|Revenue| D3[Insurance Commission]
    D -->|Revenue| D4[Dispute Fees]
    E -->|Revenue| E1[Product Sales Profit]
```

---

## 3. Revenue Sources by Role

| Role | Revenue Source | Pricing Guidance | Notes |
|------|---------------|-----------------|-------|
| **Merchant DNS** | API Registration Fee | Low flat annual fee | Just enough to sustain operations |
| | Premium Features | On-demand | Real-time inventory index, analytics dashboards |
| **Trust Company** | Annual Certification Fee | Tiered by certification level | Basic → Deep → Real-time |
| | Transaction Guarantee Fee | 0.5%–2% of transaction | Higher for high-value goods |
| | Dispute Processing Fee | Prepaid by complainant | Loser pays |
| | Quality Insurance Commission | Premium share | Partnership with underwriters |
| **AI Agent** | Premium Subscription | Monthly / Annual | Basic features free |
| | API Call Fee | Minimal per-transaction | Far below traditional ad costs |
| | Referral Commission | Per completed transaction | Optional model |
| **Manufacturer** | Product Sales Profit | Autonomous pricing | Profit margin expands significantly with cost reduction |

---

## 4. Economics: Paradigm vs. Traditional Platform

| Metric | Traditional Platforms | AI Shopping Paradigm |
|--------|----------------------|---------------------|
| Platform Commission | 5–15% of GMV | 0 |
| Ad / Promotion Fees | 20–40% of GMV | 0 |
| Trust Guarantee Fee | No independent service | 0.5–2% of GMV |
| Registration / Certification | Store setup + deposit | ~Tens of dollars/year |
| **Total Manufacturer Burden** | **15–30% of GMV** | **< 3% of GMV** |
| Consumer Experience | Ad interference, fake reviews | Pure algorithm, real reviews |

Traditional platforms extract 15–30% of GMV as a combined "traffic tax + trust tax." The new paradigm addresses these two taxes separately: the former through free AI algorithms (protocol layer), the latter through competitively priced trust services (< 3%).

---

[← Back to Main File](./AI-Shopping-Paradigm.md)
