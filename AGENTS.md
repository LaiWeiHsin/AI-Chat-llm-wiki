# AGENTS.md — LLM Wiki 規範與維護手冊

本文件是此 LLM Wiki 的核心架構規則與操作規範。所有在此知識庫作業的 AI Agent 必須嚴格遵守以下約定。

---

## 1. 專案願景與主題範疇

本知識庫旨在建立一個以 **「AI Chat 與互動式小說 / 角色扮演 (Role-Playing) 平台之後端技術與架構原理」** 為核心的沉浸式知識庫。

### 探討核心範疇：
1. **系統架構與提示詞工程 (Prompt Engineering & Architecture)**：
   - 角色人設（Persona）、世界觀（World Info / Lorebook）、使用者設定（User Persona）、範例對話（Few-shot Dialogues）的上下文編排。
   - 動態上下文組裝順序（Context Ordering / Formatting Templates，如 ChatML, Alpaca, Llama-3-instruct）。
2. **記憶與檢索機制 (Memory & Retrieval)**：
   - 滑動窗口（Sliding Window）、摘要快取（Summary Buffer）、關鍵字觸發式記憶（Regex / Keyword Lorebook）、向量檢索（RAG）在 RP 場景的局限與優化。
3. **文本生成與取樣調校 (Generation & Sampling Dynamics)**：
   - 避免復讀與卡頓的取樣機制：Temperature, Top-P, Min-P, Top-K, Repetition Penalty, Frequency/Presence Penalty, Mirostat。
4. **模型微調與開源生態 (Fine-tuning & Open-Source RP Models)**：
   - 開源社群技術棧（SillyTavern, KoboldAI, Text-Generation-WebUI, vLLM, Ollama）。
   - 商業代表產品架構分析（Character.ai, NovelAI, AI Dungeon, JanitorAI, Chub.ai）。
   - 專用小說與 RP 模型（如 Starcoder/Llama/Mistral 衍生之微調模型）。

---

## 2. 目錄結構規範

```text
d:/CGU/生成式AI/LLM Wiki/
├── AGENTS.md               # [本文件] 知識庫架構與操作指南
├── index.md                # 內容導覽目錄（依主題分類，每次 Ingest 自動更新）
├── log.md                  # 時間軸日誌（append-only，記錄每次異動）
├── raw/                    # 不可變原始資料層（Agent 抓取或使用者放入的資料，絕不直接修改）
│   └── assets/             # 圖片、架構圖、截圖
└── wiki/                   # 知識產出層（Agent 擁有並持續維護）
    ├── sources/            # 原始文獻/文章的結構化摘要與評析
    ├── concepts/           # 核心概念與技術原理（如 Lorebook、Min-P、Sliding-Window 等）
    ├── entities/           # 平台、工具、開源前端與模型（如 SillyTavern, Character.ai 等）
    └── syntheses/          # 跨主題綜合研討、架構全景與技術演化對比
```

---

## 3. 檔案與格式約定

### 3.1 語言與文風
- 主要語言：**繁體中文（台灣習慣用語）**。
- 專有名詞保留英文或中英對照（如：`Prompt Injection`, `Lorebook / 世界書`, `Context Window`, `Sampling Parameter`）。
- 嚴謹客觀、具備軟體工程架構與演算法深度，善用 Mermaid 繪製資料流與狀態圖。

### 3.2 鏈結語法 (Standard Markdown Links)
- 因未來將匯出為 HTML Slide 與標準網頁，**一律採用標準 Markdown 相對路徑鏈結**，不使用 Obsidian 專用語法：
  - 位於 Wiki 子目錄時寫法範例：`[Lorebook 機制](../concepts/Lorebook-World-Info.md)` 或 `[SillyTavern](../entities/SillyTavern.md)`。
  - 位於根目錄時寫法範例：`[Lorebook 機制](wiki/concepts/Lorebook-World-Info.md)` 或 `[SillyTavern](wiki/entities/SillyTavern.md)`。

### 3.3 輕量化 YAML Frontmatter
每個 `wiki/` 下的頁面頂部需包含簡潔的 YAML 標頭：
```yaml
---
title: "頁面標題"
type: concept | entity | source | synthesis
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [ai-chat, memory, architecture]
sources:
  - "raw/2026-xx-xx-article-name.md"
---
```

---

## 4. Agent 三大核心操作流程

### 4.1 Ingest（資料攝取 — 全自動化流程）
當引入新資料或執行主題爬梳時，Agent 需循序執行以下步驟：
1. **保存原始檔案**：將爬取或獲取的原始文章/規格書完整儲存於 `raw/YYYY-MM-DD-<slug>.md`。
2. **建立來源摘要**：於 `wiki/sources/<slug>.md` 撰寫結構化摘要（含：背景、核心觀點、架構細節、技術啟發）。
3. **擴散更新知識層**：
   - 建立或更新對應的 `wiki/concepts/*.md`。
   - 建立或更新對應的 `wiki/entities/*.md`。
   - 若引發架構層級的宏觀洞察，在 `wiki/syntheses/*.md` 補充或更新。
4. **衝突與演進處理**：若新資料與舊筆記有差異或觀點衝突，**不直接刪除舊內容**，而是新增 `### 技術演進與觀點對比` 章節，詳述版本演變或兩派流派的差異。
5. **更新目錄**：於 `index.md` 登錄新頁面並更新關聯性說明。
6. **追加日誌**：於 `log.md` 附加一行/一段紀錄：
   ```markdown
   ## [YYYY-MM-DD] ingest | 摘要主題說明
   - Raw: `raw/...`
   - Created: `wiki/...`
   - Updated: `wiki/...`
   ```

### 4.2 Query（深度問答與成果回寫）
1. 查詢時優先讀取 `index.md` 定位核心檔案，再進入相關頁面合成答案。
2. 若使用者的問題產出了具備長遠價值的綜合性比較、架構圖或演算法分析，**主動提議或直接將該成果回寫為 `wiki/syntheses/` 的新頁面**。
3. 同步更新 `index.md` 與 `log.md`。

### 4.3 Lint（知識庫健康檢查）
定期或依指令執行檢查：
- **斷鏈檢查 (Broken Links)**：確認所有相對路徑都能指向實體檔案。
- **孤立頁面 (Orphan Pages)**：檢查哪些頁面未在 `index.md` 或其他頁面中被引用。
- **空缺分析 (Knowledge Gaps)**：掃描各頁面中被提及但尚未建立獨立說明的關鍵概念，列入下一階段探究清單。
- 檢查結果記錄於 `log.md` 並更新待辦清單。

---

## 5. 未來 HTML Slide 輸出準備
本知識庫沉澱之內容將作為後續生成**互動式 HTML 簡報（Slide Deck）**之原料。在撰寫 `syntheses/` 與核心 `concepts/` 時，應具備模組化的段落結構（標題、核心痛點、架構解法、Mermaid 圖表、優缺點對照表），便於無縫轉譯為 Slide 頁面。
