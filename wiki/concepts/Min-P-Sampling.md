---
title: "Min-P 取樣演算法 (Min-P Sampling)"
type: concept
created: 2026-11-15
updated: 2026-11-15
tags: [sampling, min-p, temperature, decoding-strategies]
sources:
  - "wiki/sources/min-p-sampling.md"
---

# Min-P 取樣演算法 (Min-P Sampling)

## 1. 概念定義
**Min-P 取樣** 是由 Nguyen 等人於 2024 年提出的一種自適應截斷取樣策略。其核心設計理念是解決傳統 **Top-P (Nucleus Sampling)** 在大語言模型創作場景（角色扮演、小說撰寫）中容易出現的**「高溫度失真」**與**「低溫度詞彙單調」**問題。

$$\text{Threshold} = \text{min\_p} \times P(\text{top\_token})$$

候選詞庫中，任何單一機率 $P(t) < \text{Threshold}$ 的 Token 將被直接剔除，剩餘候選詞再重新進行歸一化機率分配並進行隨機抽樣。

---

## 2. 核心工作原理

```text
假設詞彙分佈經 Softmax 後：
情況 A (模型非常篤定，例如語法關鍵字):
  P(top_token) = 0.80
  若 min_p = 0.05
  門檻 = 0.80 * 0.05 = 0.04
  --> 只有機率 >= 4% 的詞能被保留，大幅收斂候選詞，防止低品質雜訊混入。

情況 B (模型面臨開放創作情境，有多種合理詞彙):
  P(top_token) = 0.12
  若 min_p = 0.05
  門檻 = 0.12 * 0.05 = 0.006
  --> 機率只要 >= 0.6% 的詞就能被納入候選池，候選池自然擴大，容許富有創意的詞彙被選中。
```

---

## 3. 在 AI Chat 與互動小說中的革命性優勢

1. **釋放更高溫度 (Higher Temperature Headroom)**：
   - 傳統 Top-P 在 `Temperature > 1.0` 時，因為累積機率計算會把尾部的大量無意義 Token 納入，常出現錯字、幻覺或胡言亂語。
   - Min-P 允許創作者放心地將溫度拉高至 `1.1 ~ 1.4`，使 AI 在描述戰鬥、情緒波瀾或文學修辭時展現出遠超以往的生動感，同時保持故事邏輯線不崩潰。
2. **根除機械化復讀 (Repetition Loops)**：
   - 當模型陷入特定口癖或句型循環時，傳統解法是加重 `Repetition Penalty`，但這往往會導致模型連正常的常用字詞都避開，造成文句生硬。
   - Min-P 透過自然拉開與壓縮候選池，使模型具備有機的詞彙輪替能力。

---

## 4. 推薦參數配置 (Roleplay 推薦標準)
- `min_p`: `0.05` ~ `0.10`（新手建議 `0.05` 或 `0.08`）
- `temperature`: `1.05` ~ `1.25`
- `top_p`: 設為 `1.0`（完全停用 Top-P，由 Min-P 主導截斷）
- `top_k`: 設為 `0`（完全停用 Top-K）

---

## 5. 關聯頁面
- [上下文組裝管線](../concepts/Context-Assembly-Pipeline.md)
- [SillyTavern](../entities/SillyTavern.md)
