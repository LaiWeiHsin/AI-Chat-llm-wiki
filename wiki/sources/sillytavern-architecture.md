---
title: "SillyTavern 提示詞排序與 Character Card 規範解析"
type: source
created: 2026-11-15
updated: 2026-11-15
tags: [sillytavern, prompt-engineering, character-card, middleware]
sources:
  - "raw/2026-11-15-sillytavern-architecture-and-prompt-ordering.md"
---

# SillyTavern 提示詞排序與 Character Card 規範解析

> 原始文獻存檔：[2026-11-15-sillytavern-architecture-and-prompt-ordering.md](../../raw/2026-11-15-sillytavern-architecture-and-prompt-ordering.md)

## 1. 核心背景
SillyTavern 是目前開源社群中最成熟、影響力最大的 AI Role-Playing 與互動式敘事中介軟體（Middleware）。它不負責模型推理，而是負責**將使用者設定、角色人設、世界觀（Lorebook）與對話歷程，編排成最佳的提示詞上下文結構**，再交付給後端推理引擎（如 vLLM、KoboldCpp、Ollama 或各大商業 API）。

## 2. 核心技術洞察

### 2.1 嚴格的分層提示詞編排（Instruction Hierarchy）
SillyTavern 的 Prompt Manager 實踐了角色扮演中極為關鍵的組裝管線：
- **頂層（System / Main Prompt）**：全域行為約束、文體風格指令、防破防（Jailbreak）結構。
- **使用者人設（User Persona）**：定義玩家角色 `{{user}}` 的外貌、身份、互動關係。
- **角色卡核心定義（Character Card V2/V3）**：包含 `description`、`personality`、`scenario` 以及最關鍵的 `mes_example`（透過少樣本 Few-shot 建立角色的說話語氣與口吻）。
- **對話歷史（Chat History）**：滑動窗口內的即時對話。
- **深入注入（Author's Note / In-chat Injection）**：以特定深度（`@ Depth`）將強烈引導提示插入對話結尾處，確保模型不會因為長上下文遺忘當前情節目標。

### 2.2 Character Card V2/V3 標準
開源社群制定了跨平台的角色卡標準，將 JSON 元數據直接嵌入 PNG 圖片的專用元數據區塊（`tEXt` / `zTXt`），讓一張角色圖片即包含完整人設、世界觀與範例對話，大幅降低跨平台分享門檻。

## 3. 技術啟發
- 互動式小說平台不是單純將對話丟給 LLM，而是依賴精密的**上下文組裝管線（Context Assembly Pipeline）**。
- 將靜態人設與動態情境拆分，並透過範例對話（`mes_example`）固定輸出風格，是解決「AI 說話機械化」的最有效手段。
