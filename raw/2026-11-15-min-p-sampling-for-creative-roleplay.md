# Raw Source: Min-p Sampling for Creative and Coherent LLM Outputs

- **Source**: Nguyen et al., arXiv:2407.01082 / Hugging Face Transformers & vLLM documentation
- **Date**: 2026-11-15 (Archived)
- **Topics**: Next-token Sampling, Nucleus vs Min-p, High-Temperature Roleplay, Repetition Suppression

---

## 1. Mathematical Formulation
Min-p dynamically prunes the logits distribution before sampling by establishing a probability floor tied directly to the highest probability token in the current distribution:

$$\text{Threshold} = \text{min\_p} \times P(\text{top\_token})$$

Any token $t_i$ where $P(t_i) < \text{Threshold}$ is masked out.

---

## 2. Comparison with Top-p (Nucleus) and Top-k
- **Top-k**: Fixed size $K$. When the model is uncertain over 100 valid words, it truncates abruptly at $K$. When the model is 99% confident in 1 word, it still forces $K-1$ irrelevant tokens into the candidate pool.
- **Top-p**: Cumulative probability sum. When probability is flat (high entropy), the candidate pool explodes with low-quality tail tokens, causing incoherent "hallucinations" or nonsensical text.
- **Min-p**: Scales dynamically with model certainty.
  - *High certainty ($P_{top} = 0.8$, $\text{min\_p} = 0.05$)*: Threshold = 0.04. Only tokens with $\ge 4\%$ probability remain. Candidate pool is narrow and focused.
  - *Low certainty ($P_{top} = 0.1$, $\text{min\_p} = 0.05$)*: Threshold = 0.005. Candidate pool organically expands to allow creative/diverse word choices without accepting zero-probability noise.

---

## 3. Impact on Roleplay & Creative Storytelling
- Allows users to elevate `Temperature` (e.g. 1.1 ~ 1.4) to achieve colorful vocabulary, varied syntax, and strong character personality without descending into gibberish.
- Significantly reduces repetition loops without inducing the robotic stiffness caused by aggressive Frequency/Presence penalties.
