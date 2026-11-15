# Raw Source: SillyTavern Documentation & Prompt Ordering Pipeline

- **Source**: SillyTavern Official Documentation & Community Specifications
- **Date**: 2026-11-15 (Archived)
- **Topics**: Character Cards V2/V3, Prompt Manager, World Info Injection, Context Ordering

---

## 1. Prompt Hierarchy & Compilation Order
SillyTavern acts as an orchestration middleware between the user interface and backend inference engines (vLLM, KoboldCpp, Aphrodite, OpenAI-compatible APIs). When assembling the prompt payload:

1. **System / Main Prompts**: Core behavioral constraints, markdown styling rules, safety bypass/jailbreak formatting.
2. **Persona Description**: User identity profile (`{{user}}` description, attributes, speech style).
3. **World Info (Before Char Defs)**: Lorebook entries explicitly tagged to load early.
4. **Character Card Core Fields**:
   - Name, Description, Personality.
   - Scenario (current setup/starting condition).
   - First Message / Greeting.
   - Example Dialogues (`<START>` ... dialogue examples).
5. **World Info (After Char Defs / Specific Depths)**: High-priority lore entries.
6. **Chat History**: Recent multi-turn dialogue formatted according to model prompt template (e.g. ChatML, Alpaca, Llama-3).
7. **Author's Note (AN)**: In-context nudges placed near the end of context.
8. **Post-History Instructions / Nudges**: Final reinforcement rules before assistant prefill.

---

## 2. Character Card V2/V3 Standard
A Character Card is serialized as JSON or embedded within PNG metadata chunks (`tEXt` or `zTXt`). Key fields:
- `name`: Character name.
- `description`: Detailed physical & background definition.
- `personality`: Personality traits, quirks, behavioral modifiers.
- `scenario`: Setting and premise.
- `first_mes`: Opening narration and dialogue.
- `mes_example`: Multi-turn dialogue examples demonstrating voice, formatting, speech rhythm.
- `character_book`: Bundled World Info / Lorebook containing triggered entries.

---

## 3. World Info (Lorebook) Injection Controls
- **Global vs Character Scope**: Global entries stack first, Character-specific entries stack next.
- **Insertion Order**: Integer sorting (higher numbers placed closer to the active conversation context, yielding higher attention weight).
- **Positioning**: Before Char Defs, After Char Defs, Around Example Messages, Top/Bottom of Author's Note, `@ Depth N` (injected N turns back from current message), or `{{outlet::Name}}` manual macro placement.
