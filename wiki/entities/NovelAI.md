---
title: "NovelAI 互動小說生成平台與敘事引擎"
type: entity
created: 2026-11-15
updated: 2026-11-15
tags: [novelai, interactive-fiction, storytelling, kayra, clippy]
sources:
  - "wiki/sources/novelai-lorebook-mechanics.md"
---

# NovelAI 互動小說生成平台與敘事引擎

## 1. 實體概述
**NovelAI** 是一家由 Anlatan 公司營運的訂閱制 AI 互動寫作與小說生成平台。不同於 Character.ai 的「聊天室（Chat）」形態，NovelAI 採用的是純粹的**「續寫（Continuation）與互動式敘事（Text-Adventure）」**模式，介面更像是一個具備 AI 輔助的微軟 Word 或作家文字編輯器。

## 2. 關鍵架構特色
- **專用文學微調模型 (如 Kayra, Clio)**：基於文學作品、經典小說、詩歌、TRPG 劇本進行深度微調，掌握深厚的人稱視角、感官細節描繪與對話節奏。
- **產業標準的 Lorebook 系統**：最早將關鍵字觸發、搜尋深度限制、級聯觸發（Cascading Activation）標準化的平台。
- **Context Viewer (上下文透視工具)**：提供使用者即時檢視每一輪生成時，哪些 Lorebook 條目被加載、消耗了多少 Token、被放置在什麼位置，為技術愛好者提供了高度的可觀測性。
- **隱私優先架構**：承諾對使用者的故事進行客戶端端對端加密（E2EE），不利用使用者生成內容進行模型重訓。

---
## 3. 關聯頁面
- [Lorebook (世界書) 動態注入機制](../concepts/Lorebook-World-Info.md)
- [上下文組裝管線](../concepts/Context-Assembly-Pipeline.md)
