# Raw Source: Roleplay AI Platform Architecture, Memory Management & Security Vulnerabilities

- **Source**: Industry Analysis & Academic Security Audits on Roleplay LLMs (Character.ai, JanitorAI, Chub)
- **Date**: 2026-11-15 (Archived)
- **Topics**: Instruction Hierarchy, Long-term Memory Tradeoffs, Prompt Injection in RP

---

## 1. Instruction Hierarchy & Roleplay Framing
Commercial and open-source roleplay platforms use layered prompt wrapping:
1. System boundary (Base instructions, strict output formatting, safety filters).
2. Persona definition (Character attributes, quirks, psychological profiles).
3. Dynamic Lorebook entries (State/World Info triggered by regex or keywords).
4. Dialogue buffer (Sliding window or vector-retrieved episodic memory).
5. User input wrapped in structural delimiters (`<user>`, `<human>`, `{{user}}`).

---

## 2. Long-Term Memory Mechanisms in Roleplay
- **Sliding Window**: Simple FIFO buffer of recent turns. Perfect short-term consistency, high narrative flow, but inevitable long-term amnesia.
- **Rolling Summarization**: A background worker periodically condenses turns $N-20$ to $N-10$ into a summary paragraph. Risk: loss of emotional nuances, exact inventory details, and conversational tone.
- **Semantic Vector Memory (RAG)**: Chunks past chat messages into embedding vectors.
  - *Major RP Flaw*: Semantic similarity does NOT equal narrative relevance. Asking "What did we have for dinner yesterday?" might retrieve a dinner conversation from 30 chapters ago instead of the most recent narrative state.
- **State/Variable Tracking (Hybrid)**: Storing explicit key-value status (Location, Inventory, Relationship Level, Time of Day) updated via function calling or regex triggers, injected into system context every turn.

---

## 3. Cognitive Jailbreaking & Role Confusion
- **OOC (Out Of Character) Exploits**: Attackers prefix prompts with `[OOC: ...]` or `(System Note: ...)` tricking the model into believing the command comes from the simulation administrator rather than the roleplay partner.
- **Memory Poisoning**: Iteratively nudging false historical facts or overriding system directives into the long-term summary buffer so that subsequent turns accept malicious rules as established canon.
- **Defenses**: Strict XML tags (`<narrative>`, `<user_input>`), separate developer-role prompt channels, and LLM-as-a-judge memory sanitizers.
