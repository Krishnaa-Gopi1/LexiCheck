# ✦ LexiCheck — Compiler-Based English Spell Checker

A web-based spelling identification and correction tool built using a **compiler-inspired pipeline** — tokenization, lexical analysis, symbol-table validation, and grammar heuristics — all rendered in a polished, interactive frontend.

---

##  Features

| Feature | Details |
|---|---|
| **Lexical Tokenizer** | Splits input into a typed token stream (WORD, NUMBER, PUNCTUATION, WHITESPACE, MIXED) |
| **Symbol Table Lookup** | Validates each word token against a curated dictionary |
| **Levenshtein Distance** | Generates up to 5 ranked spelling suggestions per error |
| **Grammar Heuristics** | Detects repeated words, pronoun capitalisation, confusable homophones (`their/there/they're`, `its/it's`, etc.) |
| **Auto-Correction** | One-click apply of top suggestion for every misspelled word |
| **File Upload** | Drag-and-drop or browse `.txt` files |
| **4-Tab Output** | Annotated view · Token stream table · Suggestions panel · Auto-corrected text |

---

##  Compiler Pipeline

```
INPUT TEXT
    │
    ▼
┌─────────────┐
│   LEXER     │  → Tokenizes raw text into typed lexemes
└─────┬───────┘
      │
      ▼
┌─────────────┐
│   PARSER    │  → Reads token stream, builds context (sentence position, word pairs)
└─────┬───────┘
      │
      ▼
┌─────────────────┐
│   VALIDATOR     │  → Symbol-table lookup + grammar rules
│  (Symbol Table) │
└─────┬───────────┘
      │
      ▼
┌─────────────┐
│   OUTPUT    │  → Annotated HTML, token table, suggestions, corrected text
└─────────────┘
```

---

##  Getting Started

This is a **pure client-side** application — no server, no build step.

```bash
# Clone
git clone https://github.com/<your-username>/lexicheck.git
cd lexicheck

# Open directly in browser
open index.html
```

Or simply visit the **GitHub Pages** deployment:
`https://<your-username>.github.io/lexicheck/`

---

##  Project Structure

```
lexicheck/
├── index.html     # Full application (HTML + CSS + JS, self-contained)
└── README.md
```

---

##  How It Works

### 1. Lexer (Tokenizer)
```js
function tokenize(text) {
  // Splits on word boundaries, preserving punctuation & whitespace
  // Returns: [{ lexeme, type, pos, len }, ...]
}
```
Token types: `WORD | NUMBER | PUNCTUATION | WHITESPACE | MIXED`

### 2. Symbol Table (Dictionary)
A JavaScript `Set` of ~2,000 common English words. Each `WORD` token is looked up in `O(1)`.

### 3. Validator
- **Spell check**: dictionary lookup; flags unknown words
- **Suggestion engine**: Levenshtein edit distance ≤ 3 against all dictionary entries, sorted by distance
- **Grammar heuristics**: repeated words, pronoun `I`, confusable homophones

### 4. Auto-Corrector
Replaces each misspelled token's position with the top-ranked suggestion.

---

##  Output Tabs

| Tab | Content |
|---|---|
| **Annotated** | Original text with red wavy underlines (spelling) and amber underlines (grammar) |
| **Tokens** | Full lexical token stream table with type and status |
| **Suggestions** | Per-error card with clickable suggestion chips |
| **Corrected** | Clean auto-corrected text with copy-to-clipboard |

---

##  Extending

- **Larger dictionary**: replace the `DICTIONARY` string with a fetch from a JSON wordlist
- **More grammar rules**: extend `GRAMMAR_RULES` and `COMMON_CONFUSABLES`
- **API backend**: swap `getSuggestions()` for a call to a spell-check API

---
