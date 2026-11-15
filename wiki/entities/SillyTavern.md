---
title: "SillyTavern 開源角色扮演中介軟體"
type: entity
created: 2026-11-15
updated: 2026-11-15
tags: [sillytavern, open-source, middleware, frontend, ui]
sources:
  - "wiki/sources/sillytavern-architecture.md"
---

# SillyTavern 開源角色扮演中介軟體

## 1. 實體概述
**SillyTavern** 是目前全球開源 AI 社群中最受歡迎的 LLM 前端中介軟體。它本身不包含模型權重，而是作為強大的**提示詞編排（Prompt Orchestration）與客戶端介面**，支援連接本地端推理後端（如 KoboldCpp, vLLM, Ollama, LM Studio）以及各大雲端商用 API（OpenAI, Anthropic Claude, Google Gemini, OpenRouter 等）。

## 2. 核心功能亮點
- **Character Card V2/V3 支援**：支援將人設、問候語、範例對話打包進 PNG 圖片。
- **全動態 World Info (Lorebook)**：支援正則表達式、遞迴觸發、插入深度與順序權重微調。
- **Author's Note (@ Depth 注入)**：動態干預上下文結尾。
- **取樣參數全自訂**：領先業界支援 [Min-P 取樣](../concepts/Min-P-Sampling.md)、Mirostat、Repetition Penalty 等高級解碼設定。
- **擴充套件生態系**：支援文字轉語音 (TTS/XTTS)、圖像生成 (Stable Diffusion 插件)、語音輸入 (STT)、動態角色立繪 (Live2D / 表情包動態切換)。

## 3. 技術定位與意義
SillyTavern 是將純文字 LLM 轉變為「身歷其境互動式視覺小說」的集大成者，證明了「優秀的上下文工程與中介層」能讓普通開源大模型展現出媲美專屬商業平台的沉浸式對話水準。

---
## 4. 關聯頁面
- [上下文組裝管線](../concepts/Context-Assembly-Pipeline.md)
- [Lorebook 機制](../concepts/Lorebook-World-Info.md)
- [Min-P 取樣演算法](../concepts/Min-P-Sampling.md)
