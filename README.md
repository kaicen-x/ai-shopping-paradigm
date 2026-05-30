# AI Shopping Paradigm / AI购物新范式

> **Integrity and quality run through every link.** A **transaction revolution** that rebuilds commercial trust from the **protocol layer** up — five powers separated, every action verifiable on-chain, trust as a competitive market service.
>
> **诚信与品质贯穿全流程。** 从 **底层协议** 重构商业信任的 **交易革命** —— 五权分立，链上可验证，诚信成为可竞争的市场化服务。

---

## Mind Map / 思维导图

```mermaid
mindmap
  root(("AI Shopping<br/>Paradigm"))
    Manufacturers / 生产厂家
      Self-hosted Product API<br/>自持商品API
      Autonomous Pricing<br/>自主定价
    Merchant DNS / 商家DNS
      API Index & Search<br/>API索引与搜索
      Multi-provider Competition<br/>多家竞争
    Reputation Certification / 信誉认证公司
      Factory Certification<br/>验厂认证
      Reputation Scoring<br/>信誉评分
      Review Management<br/>评价管理
      Multi-provider Competition<br/>多家竞争
    Transaction Guarantee / 交易担保公司
      Trust Escrow<br/>信托账户
      Payment & Release<br/>收款放款
      Dispute Arbitration<br/>纠纷仲裁
      Multi-provider Competition<br/>多家竞争
    AI Agent
      Semantic Search & Comparison<br/>语义理解比价下单
      Multi-provider Competition<br/>多家竞争
    Consumers / 消费者
      Preference Settings<br/>设定偏好
      Receipt Confirmation & Review<br/>确认收货与评价
```

---

## Transaction Flow / 交易流程

```mermaid
flowchart TD
    A[User Input<br/>用户需求] --> B[AI Agent<br/>Parse Intent / 解析意图]
    B --> C[Merchant DNS / 商家DNS<br/>Query API Addresses]
    C --> D[Parallel Query / 并行查询]
    D --> D1[Product API<br/>商品API]
    D --> D2[Reputation API<br/>信誉认证]
    D --> D3[Guarantee API<br/>交易担保]
    D1 --> E[Aggregate All Data<br/>汇总全部数据]
    D2 --> E
    D3 --> E
    E --> F[AI Agent<br/>Rank by Weights / 按权重排序]
    F --> G{Confirm? / 确认下单?}
    G -->|No / 否| A
    G -->|Yes / 是| H[Pay to Escrow<br/>付款至信托账户]
    H --> I[Guarantee Co. Notifies Ship<br/>担保公司通知发货]
    I --> J{Receipt / 收货}
    J -->|Confirm/Timeout<br/>确认/超时| K[Release Funds<br/>放款给厂家]
    J -->|Dispute / 申诉| L[Arbitration / 仲裁]
    L -->|User Wins / 用户胜诉| M[Refund / 退款]
    L -->|Mfr Wins / 厂家胜诉| K
    K --> N[User Reviews<br/>信誉认证记录]
    M --> N
```

---

## Core Roles / 核心角色

| Role / 角色 | Layer / 层级 | Description / 说明 |
|-------------|-------------|-------------------|
| **Manufacturer** / 生产厂家 | Supply / 供给 | Self-hosted Product API, autonomous pricing / 自持商品API，自主定价 |
| **Merchant DNS** / 商家DNS | Index / 索引 | API-only index, no product data, multi-provider / 仅做API索引，不碰商品数据 |
| **Reputation Certification** / 信誉认证公司 | Reputation / 评价 | Certification + scoring + review mgmt, on-chain, never touches funds / 验厂+评分+评价管理，链上存证，绝不碰资金 |
| **Transaction Guarantee** / 交易担保公司 | Payment / 资金 | Escrow + payment + arbitration, never evaluates reputation / 信托+收款+仲裁，绝不参与评价 |
| **AI Agent** | Decision / 决策 | Semantic comparison, weighted ranking, multi-provider / 语义比价、权重排序，多家竞争 |
| **Consumer** / 消费者 | Demand / 需求 | Set preferences, confirm receipt, review / 设定偏好，确认收货，评价反馈 |

> Evaluation never touches money. Money never evaluates. Supply doesn't index. Index doesn't advertise. Decision doesn't take a cut. — **Five-Power Separation**.
>
> 评价不碰钱，资金不评价，供给不索引，索引不广告，决策不抽成 —— **五权分立**。

---

## Core Logic / 核心逻辑

```mermaid
graph TD
    A["AI replaces human decisions<br/>AI替人决策"] --> B["Ads become irrelevant<br/>广告失效"]
    B --> C["Traffic value drops to zero<br/>流量分发价值归零"]
    C --> D["Platform model collapses<br/>平台商业模式瓦解"]
    D --> E["Goods as a Service<br/>商品即服务 GaaS"]
```

---

## Document Navigation / 文档导航

| Chapter / 章节 | English | 中文简体 |
|---------------|---------|----------|
| Main File / 主文件 | [AI-Shopping-Paradigm](English/README.md) | [README](中文简体/README.md) |
| Overview / 概述与愿景 | [01-overview-and-vision](English/01-overview-and-vision.md) | [01-概述与愿景](中文简体/01-概述与愿景.md) |
| Core Architecture / 核心架构 | [02-core-architecture](English/02-core-architecture-and-roles.md) | [02-核心架构与角色](中文简体/02-核心架构与角色.md) |
| Business Value / 商业价值 | [03-business-value](English/03-business-value-and-model.md) | [03-商业价值与商业模式](中文简体/03-商业价值与商业模式.md) |
| Commerce Transformation / 商业变革 | [04-commerce-transformation](English/04-commerce-transformation-and-new-industries.md) | [04-商业变革与新产业](中文简体/04-商业变革与新产业.md) |
| Disruption Path / 颠覆路径 | [05-disruption-path](English/05-disruption-path-and-cold-start.md) | [05-颠覆路径与冷启动](中文简体/05-颠覆路径与冷启动.md) |
| Future Evolution / 未来演进 | [06-future-evolution](English/06-future-evolution.md) | [06-未来演进方向](中文简体/06-未来演进方向.md) |
| REST API / 接口定义 | [API Definitions](English/api/API-definitions.md) | [API接口定义](中文简体/api/API接口定义.md) |
