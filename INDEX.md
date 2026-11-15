# LLM Wiki — AI 互動式小說與角色扮演 (Role-Playing) 技術架構索引

本知識庫專注於解析 AI Chat 平台、互動式小說與角色扮演系統的底層技術架構、記憶機制、提示詞編排與取樣動力學。

---

## 視覺化簡報 (Interactive Presentation)
- **[互動式 HTML 簡報 (首頁入口)](index.html)** | **[備用連結 (presentation.html)](presentation.html)**  
  *專為演講與展示設計的 16:9 深色科技風格簡報，內建全螢幕支援、鍵盤快捷鍵換頁，以及可即時拖曳拉桿體驗的「Min-P 動態取樣互動模擬器」！*

---

## 導覽目錄 (Table of Contents)

### 1. 綜合架構與專題探討 (Syntheses)
- [AI 互動式小說與角色扮演平台：完整技術架構與運作原理全景](wiki/syntheses/AI-Interactive-Fiction-Architecture.md)  
  *深入解析從前端輸入、中介層組裝、世界書檢索、Min-P 解碼到狀態回寫的端到端資料流與四大技術柱石，附完整 Mermaid 架構圖。*

---

### 2. 核心概念與技術原理 (Concepts)
- [上下文組裝管線 (Context Assembly Pipeline)](wiki/concepts/Context-Assembly-Pipeline.md)  
  *剖析 System Prompt、Character Card、Few-shot 對話範例、Author's Note (@ Depth) 及 Prefill 的分層組裝技術。*
- [Lorebook (世界書 / World Info) 動態注入機制](wiki/concepts/Lorebook-World-Info.md)  
  *解析基於關鍵字/正則的動態檢索、搜尋字元範圍、級聯遞迴觸發（Cascading）與 Token 預算管理，並對比向量 RAG 的差異。*
- [Min-P 取樣演算法 (Min-P Sampling)](wiki/concepts/Min-P-Sampling.md)  
  *數學原理剖析：根據最高機率 Token 動態縮放門檻，讓高溫度小說生成兼具豐富詞彙與邏輯連貫性，告別機械化復讀。*
- [角色扮演對話系統的記憶架構演進](wiki/concepts/Roleplay-Memory-Architectures.md)  
  *從初代滑動窗口、滾動摘要、向量 RAG 到當前主流的「混合狀態機 + 動態世界書」之架構演進與優缺點權衡。*

---

### 3. 實體、平台與工具 (Entities)
- [SillyTavern 開源角色扮演中介軟體](wiki/entities/SillyTavern.md)  
  *全球最受歡迎的開源 LLM 角色扮演前端，支援 Character Card V2/V3、深度注入、全動態 Lorebook 與多樣擴充套件。*
- [Character.ai (c.ai) 商業對話平台架構解析](wiki/entities/Character-ai.md)  
  *超高並發商業平台、專用對話模型微調、滑動重選（Swipe）RLHF 飛輪與記憶釘選（Pin）機制。*
- [NovelAI 互動小說生成平台與敘事引擎](wiki/entities/NovelAI.md)  
  *專用文學微調模型（Kayra）、標準化 Lorebook 級聯系統與 Context Viewer 深度透視。*

---

### 4. 原始文獻與摘要 (Sources)
- [SillyTavern 提示詞排序與 Character Card 規範解析](wiki/sources/sillytavern-architecture.md)
- [NovelAI Lorebook 運作機制與級聯觸發解析](wiki/sources/novelai-lorebook-mechanics.md)
- [Min-P 取樣演算法：提升敘事生成多樣性與連貫性](wiki/sources/min-p-sampling.md)
- [角色扮演系統之長短期記憶權衡與安全注入防禦](wiki/sources/roleplay-memory-and-security.md)

---
*最後自動更新時間：2026-11-15 (由 Agent 自動維護)*
