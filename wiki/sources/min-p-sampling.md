---
title: "Min-P 取樣演算法：提升敘事生成多樣性與連貫性"
type: source
created: 2026-11-15
updated: 2026-11-15
tags: [min-p, sampling, temperature, decoding]
sources:
  - "raw/2026-11-15-min-p-sampling-for-creative-roleplay.md"
---

# Min-P 取樣演算法：提升敘事生成多樣性與連貫性

> 原始文獻存檔：[2026-11-15-min-p-sampling-for-creative-roleplay.md](../../raw/2026-11-15-min-p-sampling-for-creative-roleplay.md)

## 1. 核心背景
在 AI Chat 與互動小說領域，傳統的 Top-p（Nucleus Sampling）與 Top-k 常常讓創作者陷入兩難：調高 Temperature 會導致模型胡言亂語（Hallucination / Gibberish），調低則會出現詞彙單調、復讀（Repetition Loop）與套路化對話。arXiv:2407.01082 提出的 **Min-p 取樣** 徹底改變了這個局面。

## 2. 演算法原理

Min-p 的截斷門檻值並非固定累計機率，而是**隨當前預測最高機率的 Token 動態縮放**：

$$\text{Threshold} = \text{min\_p} \times P(\text{top\_token})$$

任何機率低於此門檻的候選 Token 都被濾除。

### 對比傳統取樣模式：
| 取樣方式 | 模型高度自信時 ($P_{top} = 0.9$) | 模型猶豫/開放生成時 ($P_{top} = 0.1$) | 互動小說常見問題 |
| :--- | :--- | :--- | :--- |
| **Top-k (如 k=40)** | 強制保留 40 個，混入 39 個垃圾詞 | 僅保留 40 個，截斷可能精彩的字彙 | 高自信時胡言亂語，低自信時詞彙貧乏 |
| **Top-p (如 p=0.9)** | 僅保留 1~2 個（合理） | 累積至 0.9 時納入大量極低機率詞 | 扁平機率分佈時引入亂碼 |
| **Min-p (如 p=0.05)** | 門檻 = 0.045（只保留極高機率詞） | 門檻 = 0.005（候選池平滑擴展） | **在高溫度下兼顧天馬行空的文筆與邏輯收斂** |

## 3. 技術啟發
- Min-p 允許在互動小說中將 Temperature 提升至 1.1 ~ 1.4，大幅解鎖小說角色的「性格鮮明度」與「情感張力」。
- 現代開源推理後端（vLLM、SGLang、KoboldCpp）已將 Min-p 列為互動敘事的必選標配。
