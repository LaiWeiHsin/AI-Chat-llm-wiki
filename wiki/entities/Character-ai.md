---
title: "Character.ai (c.ai) 商業對話平台架構解析"
type: entity
created: 2026-11-15
updated: 2026-11-15
tags: [character-ai, commercial-platform, roleplay, high-concurrency]
sources:
  - "wiki/sources/roleplay-memory-and-security.md"
---

# Character.ai (c.ai) 商業對話平台架構解析

## 1. 實體概述
**Character.ai** 由前 Google 著名科學家 Noam Shazeer 與 Daniel De Freitas 於 2021 年共同創立，是全球流量最大的商業 AI 角色扮演與對話平台。其特點是具備極低的單字推理成本（Inference Cost）與高並發能力，支撐每日數億次對話。

## 2. 關鍵架構特色
- **專有對話大模型**：非單純套用通用開源模型，而是專門針對多輪閒聊與擬人化語料進行大規模預訓練與 RLHF。
- **滑動重選機制 (Swipe to Rerank)**：使用者對機器人的回覆不滿意時，可向右滑動生成另一組回覆。此舉不僅提升了使用者體驗，更重要的是為平台收集了海量的人類偏好比較數據（RLHF / DPO 資料集）。
- **輕量化長時記憶槽 (Memory Pins)**：允許玩家釘選（Pin）特定幾則重要對話，系統會將這些釘選訊息固定加載至 System Prompt 附近，解決角色忘記重大承諾的問題。
- **嚴格的安全審查層 (Safety Filtering Layer)**：在輸入與輸出兩端架設即時過濾模型，攔截違規內容，但也因此引發許多玩家對角色靈魂被閹割的爭議。

---
## 3. 關聯頁面
- [角色扮演記憶架構](../concepts/Roleplay-Memory-Architectures.md)
- [上下文組裝管線](../concepts/Context-Assembly-Pipeline.md)
