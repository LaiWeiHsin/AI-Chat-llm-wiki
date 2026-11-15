---
title: "NovelAI Lorebook（世界書）運作機制與級聯觸發解析"
type: source
created: 2026-11-15
updated: 2026-11-15
tags: [novelai, lorebook, world-info, dynamic-context]
sources:
  - "raw/2026-11-15-novelai-lorebook-mechanics-and-cascading.md"
---

# NovelAI Lorebook（世界書）運作機制與級聯觸發解析

> 原始文獻存檔：[2026-11-15-novelai-lorebook-mechanics-and-cascading.md](../../raw/2026-11-15-novelai-lorebook-mechanics-and-cascading.md)

## 1. 核心背景
NovelAI 是專為文學創作與互動小說設計的代表性商業平台。面對動輒數十萬字的小說世界觀，如何避免超出 Context Window 限制並降低 Token 成本，其核心解法正是 **Lorebook（世界書 / 動態條目注入系統）**。

## 2. 核心技術機制

### 2.1 搜尋範圍（Search Range）
系統並非無限制掃描整本小說，而是設定倒數 $N$ 個字元（例如最後 1,000 ~ 10,000 字元）進行關鍵字比對。只有在最近情節被提及的名詞，才會觸發對應條目。

### 2.2 級聯觸發（Cascading Activation / Recursive Scanning）
當條目 A（例如「艾爾登帝國」）因正文提及而被載入上下文後，系統會進一步掃描條目 A 內部文字是否包含條目 B（例如「皇帝拉達岡」）的觸發詞。若包含，則條目 B 也會被一併注入。這種「樹狀遞迴觸發」完美模擬了人類大腦的關聯性聯想。

### 2.3 插入優先順序與 Token 預算控制
- **Insertion Order**：以整數權重排序條目，權重高的條目優先佔用 Token 空間並放在更具影響力的上下文位置。
- **Token Budget & Reserved Tokens**：為世界書設定總容量上限（例如不超過總上下文的 20%），並可為核心條目設定「保留 Token」，防止一般背景設定擠掉關鍵角色設定。

## 3. 技術啟發
- 在角色扮演與互動小說中，**基於規則與正則的精確關鍵字觸發（Keyword Triggered Lorebook）在特定狀態追蹤上遠優於純向量檢索（Semantic RAG）**。
- 級聯觸發必須設定遞迴深度或嚴格的停用詞過濾，否則容易引起「Token 爆炸（Token Flood）」。
