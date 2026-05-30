# AI Shopping Paradigm / AI购物新范式

> A **transaction revolution** that rebuilds global commerce from the **protocol layer** up — dismantling platform monopolies with AI Agents, liberating supply with open APIs, and ending trust monopolies through market-based competition.
>
> 从 **底层协议** 重构全球商业的 **交易革命** —— 用 AI Agent 瓦解平台霸权，用开放 API 解放供给端，用市场化信任竞争终结评价垄断。

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
    Trust Companies / 信任与担保公司
      Factory Certification<br/>验厂认证
      Reputation Scoring<br/>信誉评分
      Transaction Guarantee<br/>交易担保
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
    A[User Input<br/>用户自然语言需求] --> B[AI Agent<br/>Parse Intent / 解析意图]
    B --> C[Merchant DNS / 商家DNS<br/>Query API Addresses / 查询API地址]
    C --> D[Parallel Query / 并行查询<br/>Product APIs + Trust APIs]
    D --> E[Aggregate / 汇总<br/>Price + Inventory + Reputation + Guarantee<br/>价格 + 库存 + 信誉 + 担保]
    E --> F[AI Agent<br/>Rank by User Weights<br/>按权重排序推荐]
    F --> G{Confirm Order?<br/>确认下单?}
    G -->|No / 否| A
    G -->|Yes / 是| H[Payment to Trust Escrow<br/>付款至信托账户]
    H --> I[Notify Manufacturer to Ship<br/>通知厂家发货]
    I --> J{Receipt Status<br/>收货状态}
    J -->|Confirmed / Timeout<br/>确认/超时| K[Release Funds<br/>放款给厂家]
    J -->|Dispute / 申诉| L[Trust Arbitration<br/>信任公司仲裁]
    L -->|User Wins / 用户胜诉| M[Preemptive Refund<br/>先行赔付退款]
    L -->|Manufacturer Wins / 厂家胜诉| K
```

---

## Core Roles / 核心角色

| Role / 角色                      | Description / 说明                                                                                                             |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Manufacturer** / 生产厂家      | Self-hosted Product API, autonomous pricing, free from platform control / 自持商品API，自主定价，摆脱平台绑架                  |
| **Merchant DNS** / 商家DNS       | API-only index, no product data stored, multi-provider competition / 仅做API索引，不碰商品数据，多家竞争                       |
| **Trust Company** / 信任担保公司 | Factory certification + reputation scoring + trust escrow, market-based competition / 验厂+信誉分+信托担保，市场化竞争         |
| **AI Agent**                     | Semantic comparison, weighted ranking, one-click ordering, multi-provider competition / 语义比价、权重排序、一键下单，多家竞争 |
| **Consumer** / 消费者            | Set preferences, confirm receipt, review & feedback / 设定偏好，确认收货，评价反馈                                             |

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

| Chapter / 章节                     | English                                                                                | 中文简体                                                   |
| ---------------------------------- | -------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Main File / 主文件                 | [AI-Shopping-Paradigm](English/AI-Shopping-Paradigm.md)                                | [AI购物新范式](中文简体/AI购物新范式.md)                   |
| Overview / 概述与愿景              | [01-overview-and-vision](English/01-overview-and-vision.md)                            | [01-概述与愿景](中文简体/01-概述与愿景.md)                 |
| Core Architecture / 核心架构       | [02-core-architecture](English/02-core-architecture-and-roles.md)                      | [02-核心架构与角色](中文简体/02-核心架构与角色.md)         |
| Business Value / 商业价值          | [03-business-value](English/03-business-value-and-model.md)                            | [03-商业价值与商业模式](中文简体/03-商业价值与商业模式.md) |
| Commerce Transformation / 商业变革 | [04-commerce-transformation](English/04-commerce-transformation-and-new-industries.md) | [04-商业变革与新产业](中文简体/04-商业变革与新产业.md)     |
| Disruption Path / 颠覆路径         | [05-disruption-path](English/05-disruption-path-and-cold-start.md)                     | [05-颠覆路径与冷启动](中文简体/05-颠覆路径与冷启动.md)     |
| Future Evolution / 未来演进        | [06-future-evolution](English/06-future-evolution.md)                                  | [06-未来演进方向](中文简体/06-未来演进方向.md)             |
