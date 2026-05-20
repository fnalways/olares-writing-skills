# Olares Localization Glossary

The single source of truth for **how each translatable term should be rendered in each target language**, plus per-language style and formatting rules.

## Scope and authority

This glossary owns:

- **Approved target-language translations** for translatable Olares terms (built-in apps, technical concepts, brand-prefixed forms).
- **Per-language style and formatting rules** (punctuation, spacing, sort order, plural and gender handling, etc.).

This glossary does **not** own:

- **Source-English usage rules.** See [`wordlist.md`](wordlist.md) for the A–Z reference of which English words to use, when, and how (e.g., `delete` vs `remove`, `sign in` vs `log in`, `app` vs `application`).
- **The list of non-translatable terms.** See [`non-translatable-elements.md`](non-translatable-elements.md) for everything that stays in English in all locales.
- **General UI writing patterns.** See [`ux-writing-guidelines.md`](ux-writing-guidelines.md).
- **Translation-friendly source-writing rules and per-locale UX guidance.** See [`ux-localization-guidelines.md`](ux-localization-guidelines.md).

## How to use

- **AI agents**: Load this file before translating any batch. Apply the rules for each term encountered.
- **Human reviewers**: Check translations against this glossary during review.
- **Adding terms**: Add a new entry when a term first causes inconsistency or ambiguity across translations.

---

## 1. Brand names and product trademarks

Always English. Never translated, transliterated, or abbreviated. See [Non-Translatable Elements §1](non-translatable-elements.md#1-olares-brand-and-product-names) for full rules.

| Term | All locales |
|---|---|
| Olares | Olares |
| Olares OS | Olares OS |
| Olares ID | Olares ID |
| Olares Space | Olares Space |
| LarePass | LarePass |

---

## 2. Built-in apps and surfaces

The split between "always English" and "translated" is a **product positioning** decision, not a linguistic one. Brand-bound surfaces stay English the same way Apple keeps `Safari` and `iMovie`. Generic surfaces translate the same way Apple translates `Settings → 设置` and `Terminal → 终端`. See [Non-Translatable Elements §2](non-translatable-elements.md#2-olares-built-in-apps-and-surfaces) for full rationale.

### 2a. Always English (brand-bound surfaces)

| Term | All locales | Rationale |
|---|---|---|
| Vault | Vault | Flagship trust/storage product |
| Profile | Profile | Web3 personal homepage / digital identity (closer to `Apple ID` than "account info") |
| Studio | Studio | Industry convention (cf. Android Studio, Visual Studio Code) |
| Wise | Wise | Coined name |

### 2b. Translated to natural target-language equivalent

| Source | zh-CN | ja-JP | ko-KR | Notes |
|---|---|---|---|---|
| Desktop | 桌面 | TODO | TODO | |
| Market | 应用市场 | TODO | TODO | |
| Files | 文件管理器 | TODO | TODO | When using zh-CN as a translation reference for other locales (e.g., feeding to a translator targeting ja-JP), use the shorter form **`文件`** as the input — it's closer to the universal "Files" meaning and avoids over-specifying. |
| Settings | 设置 | TODO | TODO | |
| Control Hub | 控制面板 | TODO | TODO | |
| Dashboard | 仪表盘 | TODO | TODO | |

### 2c. Brand-prefixed forms

The translation of `Olares X` depends on what `X` is. Translators translate the source faithfully — the writer decides whether the `Olares` prefix appears in the source string.

| Source | zh-CN | Why |
|---|---|---|
| `Olares Market` | `Olares 应用市场` | Generic surface translates; prefix stays |
| `Olares Files` | `Olares 文件管理器` | Same |
| `Olares Vault` | `Olares Vault` | Brand-bound surface — whole phrase stays English |
| `Olares Profile` | `Olares Profile` | Same |
| `Olares Space` | `Olares Space` | Fixed product name |

---

## 3. Technical terms

Olares-specific concepts that require approved translations.

| Term | Definition | zh-CN | ja-JP | ko-KR |
|---|---|---|---|---|
| Cluster | An Olares node group | TODO | TODO | TODO |
| Node | A single device in a cluster | TODO | TODO | TODO |

> **Note** Whether `Cluster` and `Node` should be translated or kept English is context-dependent. In admin/developer surfaces, keep English (consistent with Kubernetes ecosystem conventions). In end-user surfaces, translate. Confirm per-locale usage with the localization lead before filling in.

---

## 4. Source-English usage

Per-word usage rules in source English (when to use `delete` vs `remove`, `sign in` vs `log in`, etc.) are owned by [`wordlist.md`](wordlist.md). Don't duplicate them here. When a glossary user needs to know "what English word should we use," send them to the wordlist.

---

## 5. Per-language conventions

This is the canonical location for per-language style and formatting rules. Other documents reference this section.

### Simplified Chinese (zh-CN)

**Brand and term handling**
- Brand names are not paired with a Chinese descriptor. ✅ `打开 LarePass` / ❌ `打开 LarePass 应用`
- Brand names are not transliterated. ✅ `Olares` / ❌ `奥拉雷斯`

**Punctuation and spacing**
- Use full-width punctuation (`，。：；！？`) within Chinese sentences.
- Add a half-width space between Chinese characters and adjacent Latin or numeric content. ✅ `Olares 系统已更新到 v2.5` / ❌ `Olares系统已更新到v2.5`
- Don't italicize Chinese characters — italic CJK fonts render poorly. Use bold or color for emphasis.

**Numerals**
- Use Arabic numerals (`1`, `2`, `3`) for ordinary numbers.
- Use Chinese numerals (`一`, `二`, `三`) only in formal or literary contexts.

**Width**
- Each Chinese character is roughly 2× the width of an English letter. Strings shrink in character count but may not shrink in pixel width.

**zh-CN vs zh-TW**
- Never auto-convert one to the other. Vocabulary differs (`软件` vs. `軟體`, `视频` vs. `影片`). Treat as separate locales.

### Japanese (ja-JP)

**Brand and term handling**
- Brand names stay in Latin script. No katakana transliteration, no katakana phonetic gloss. ✅ `Olares` / ❌ `オラレス` / ❌ `Olares（オラレス）`

**Scripts and typography**
- Japanese mixes kanji, hiragana, katakana, and Latin in the same sentence. Line-break rules are complex; don't force breaks.
- Don't italicize — italic CJK looks broken.

**Punctuation**
- Use full-width `。` and `、`, not Western period and comma.

**Honorifics**
- Keigo (polite forms) is expected in product UI. The translator handles this; don't try to encode politeness in the source.

### Korean (ko-KR)

- Brand names stay in Latin script. No Hangul transliteration.
- Korean uses postpositional particles (`은/는`, `이/가`) that depend on the preceding character. Translators handle this; don't concatenate variables before particles.
- TODO: complete approved translations for the built-in apps in §2b.

### German (de-DE)

- Long compound words (`Datenschutzeinstellungen`) can exceed 30 characters. Allow text wrapping; disabling wrap will cause overflow.
- German capitalizes all nouns — grammatical, not stylistic. Don't lowercase translations.
- Default to formal `Sie` for product UI unless the brand voice is explicitly informal. Be consistent.

### French (fr-FR)

- French uses non-breaking spaces before `:`, `;`, `?`, `!`, `»`. Translators include these; don't strip them.
- Quotation marks: `« … »` (guillemets), not `"…"`.
- French requires articles where English drops them. "Open file" becomes "Ouvrir le fichier."

### Spanish (es-ES, es-MX, es-LA)

- Inverted punctuation: `¿Qué pasa?` `¡Hola!`
- `es-ES` and `es-LA` differ in vocabulary (`ordenador` vs. `computadora`) and `vosotros` vs. `ustedes`. Pick a target market and stick with it.

### Russian (ru-RU)

- Cyrillic characters are usually wider than Latin. Allow extra horizontal space.
- Russian has 6 grammatical cases. Numbers in particular need different forms based on the value. Use the framework's plural rules — don't hardcode.

### Arabic (ar-SA, ar-EG) and Hebrew (he-IL)

- Right-to-left languages. The entire UI mirrors; direction-bearing icons (back/forward, chevrons) flip.
- Brand names stay in Latin script even within RTL text. Use Unicode direction marks if rendering breaks.
- Mixed-direction text (numbers, Latin words within RTL) stays LTR within an RTL paragraph.
