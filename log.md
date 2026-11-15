# Wiki Event Log

本檔案依時間軸記錄知識庫的所有自動維護操作（Ingest, Query, Lint, Refactor）。

---

## [2026-11-15] init | 知識庫初始化建立
- 建立了 `AGENTS.md` 作為規範合約。
- 初始化目錄結構與 `index.md`, `log.md`。
- 確立目標主題：AI Chat 與互動式小說 / 角色扮演（Role-Playing）平台技術架構與原理。


## [2026-11-15] ingest | AI 互動小說與角色扮演底層架構第一次知識攝取
- **Raw Sources**:
  - `raw/2026-11-15-sillytavern-architecture-and-prompt-ordering.md`
  - `raw/2026-11-15-novelai-lorebook-mechanics-and-cascading.md`
  - `raw/2026-11-15-min-p-sampling-for-creative-roleplay.md`
  - `raw/2026-11-15-characterai-and-rp-memory-architecture.md`
- **Created Sources**:
  - `wiki/sources/sillytavern-architecture.md`
  - `wiki/sources/novelai-lorebook-mechanics.md`
  - `wiki/sources/min-p-sampling.md`
  - `wiki/sources/roleplay-memory-and-security.md`
- **Created Concepts**:
  - `wiki/concepts/Lorebook-World-Info.md`
  - `wiki/concepts/Context-Assembly-Pipeline.md`
  - `wiki/concepts/Min-P-Sampling.md`
  - `wiki/concepts/Roleplay-Memory-Architectures.md`
- **Created Entities**:
  - `wiki/entities/SillyTavern.md`
  - `wiki/entities/Character-ai.md`
  - `wiki/entities/NovelAI.md`
- **Created Syntheses**:
  - `wiki/syntheses/AI-Interactive-Fiction-Architecture.md`
- **Updated Catalog**:
  - `index.md` (全站目錄建置完成)


## [2026-11-15] presentation | 產出 HTML 互動式簡報與專屬貼圖素材
- **Created Assets**:
  - `assets/sillytavern-badge.svg` (SillyTavern 開源中介層徽章)
  - `assets/character-ai-badge.svg` (Character.ai 對話氣泡徽章)
  - `assets/novelai-badge.svg` (NovelAI 文學羽毛筆與魔導書徽章)
  - `assets/lorebook-icon.svg` (Lorebook 世界書圖鑑圖示)
  - `assets/ai-storyteller-mascot.svg` (AI 互動敘事地下城主吉祥物貼圖)
- **Created Presentation**:
  - `presentation.html` (10 頁 16:9 互動簡報，支援全螢幕、方向鍵換頁、內建 Min-P 即時模擬拉桿)
- **Updated Catalog**:
  - `index.md` (在頂端新增視覺化簡報導覽捷徑)


## [2026-11-15] lint | 知識庫全站斷鏈與孤立頁面健康檢查
- **Inspection Metrics**:
  - Total Files Scanned: 20 (`.md` & `.html`)
  - Initial Broken Links Detected: 2 (in `AGENTS.md` syntax examples) -> Fixed.
  - Initial Orphan Files Detected: 4 (`raw/*.md` only referenced in YAML frontmatter) -> Added explicit markdown hyperlinks in `wiki/sources/*.md` -> Fixed.
  - Final Broken Links Count: 0
  - Final Orphan Pages Count: 0
- **Status**: 全站健康度 100%，所有交叉引用路徑均有效解析。


## [2026-11-15] deploy | 準備 GitHub Pages 部署環境
- 建立了 `index.html`（作為 GitHub Pages 根網址直接預設首頁）。
- 保留 `presentation.html`（維持舊有外部連結相容性）。
- 新增 `.nojekyll` 檔案（跳過 GitHub Pages 內建 Jekyll 解析，避免 Markdown 與靜態資源解析衝突）。
- 更新 `index.md` 雙向導航。
