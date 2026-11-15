# Raw Source: NovelAI Lorebook Mechanics, Recursive Activation, and Token Budgets

- **Source**: NovelAI Knowledge Base & Lorebook Technical Guide
- **Date**: 2026-11-15 (Archived)
- **Topics**: Search Depth, Cascading Activation / Recursive Keys, Insertion Order, Token Reservation

---

## 1. Search Depth / Range
- Measured as **Search Range in characters** (up to 10,000 characters) scanned backwards from the end of the active story text.
- If an activation key appears inside this window, the entry is activated and prepared for injection into the context buffer.

---

## 2. Recursive Keys / Cascading Activation
- Default behavior only evaluates raw story text for trigger keys.
- **Cascading Activation**: When enabled, if Entry A is activated and pulled into context, the text *inside* Entry A is also scanned for keywords belonging to Entry B.
- If Entry B's keyword appears inside Entry A, Entry B triggers and is also inserted.
- Creates hierarchical world-building chains (e.g. `City -> Guild -> Guild Master -> Magic Item`).
- Risk: Runaway cascades triggering token budget exhaustion if common words are used as keys.

---

## 3. Insertion Position & Priority
- **Insertion Order**: Entries sorted by integer priority. Higher order numbers receive priority evaluation and first rights to token budget.
- **Insertion Position**: Relative index in prompt stack (0 = top, -1 = bottom).
- **Key-Relative Insertion**: Positions lore entry immediately adjacent to where the trigger keyword appeared in the text buffer.

---

## 4. Token Budgets & Reserved Space
- **Token Budget**: Hard limit on maximum tokens allocated to Lorebook entries (either absolute token count or percentage of total context window). When budget is exceeded, lower-priority matching entries are pruned.
- **Reserved Tokens**: Pre-allocates a guaranteed token slice for high-value entries so that dynamic context expansion does not squeeze them out if activated.
