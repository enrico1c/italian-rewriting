# italian-rewriting

A Claude skill that rewrites any source text into natural Italian prose that bypasses AI detectors (GPTZero, Originality.ai, ZeroGPT, Turnitin) and passes trained human editors. Preserves every fact, number, and citation exactly — changes only the language surface.

---

## What it does

- Eliminates all statistical, lexical, syntactic, and typographic AI fingerprints across 4 layers of rules
- Applies 30 quality gates per chunk
- Works on documents of any length via an interactive chunking loop with a Continuity Ledger
- Targets academic Italian by default (`accademico`); supports `saggistico` and `conversazionale` on request

---

## Installation by platform

### Claude Code — VS Code extension

1. Install the [Claude Code VS Code extension](https://marketplace.visualstudio.com/items?itemName=Anthropic.claude-code)
2. Copy `italian-rewriting.md` to your Claude commands directory:
   ```bash
   # macOS / Linux
   cp italian-rewriting.md ~/.claude/commands/

   # Windows (PowerShell)
   Copy-Item italian-rewriting.md "$env:USERPROFILE\.claude\commands\"
   ```
3. Reload VS Code or restart the extension
4. Invoke with `/italian-rewriting` in any Claude Code chat

### Claude Code — Desktop app

The desktop app uses the same `~/.claude/commands/` directory as the VS Code extension. Follow the same steps above — the slash command will be available immediately after copying.

### Claude Code — CLI

Same as above. Copy to `~/.claude/commands/` and invoke with `/italian-rewriting`.

### claude.ai — web (no installation)

No installation needed. The skill is a plain instruction file — paste it directly into any Claude conversation:

1. Open `italian-rewriting.md` in any text editor
2. Select all (`Ctrl+A`) and copy
3. Start a new conversation on [claude.ai](https://claude.ai)
4. Paste the entire file content as your first message, then add:
   ```
   Applica queste regole al testo che segue:

   [paste your source text here]
   ```
5. The interactive chunking loop works identically — reply `Next` between chunks, `Assemble` after the last one
6. Output will be plain markdown — copy-paste into Word or Google Docs

---

## Usage (Claude Code)

```
/italian-rewriting

[paste PDF extract, raw text, or slide content here]
```

Optional flags:
- `--registro accademico` (default) · `--registro saggistico` · `--registro conversazionale`
- `--section "4.1"` — rewrite only a specific section
- `--docx <path>` — generate a `python-docx` script for Word output (local Claude Code only; requires `pip install python-docx`)

---

## How the chunking loop works

For documents longer than ~600 words, the skill splits the text automatically and processes it interactively:

1. Claude announces: `"N chunks identified. Starting chunk 1/N."`
2. After each chunk it prints the updated **Continuity Ledger** (noun variants, structural elements, seam) and stops
3. Type **`Next`** to continue to the next chunk
4. Type **`Assemble`** after the last chunk — Claude runs all 30 quality gates and outputs the final assembled text

Each `Next` gives Claude a fresh attention reset, eliminating prompt fatigue and bypassing the output token limit.

---

## Output

| Environment | Output format |
|---|---|
| Claude Code (local) | Plain markdown (default) or `.docx` script via `--docx` flag |
| claude.ai web | Plain markdown only — copy-paste into Word/Google Docs |

---

## What the skill applies

| Layer | Rules |
|---|---|
| Layer 1 | Lexical blacklist · organic burstiness · pro-drop · dislocation · active voice · anti-sandwich · typography |
| Layer 2 | Asyndeton · -mente cap · weak verb ban · meta-discourse ban · ciò cap · containment rule · list asymmetry |
| Layer 3 | Lexical entrainment · explanatory colon · nominalization · litotes · fixed collocations |
| Layer 4 | Semicolons · complex inciso · epistemic conditional · quote weaving · correlatives |
| Systemic | Perplexity injection · logical non-linearity · functional burstiness audit |

30 quality gates verified on final assembly.

---

## Full pipeline

To get rewritten Italian text **and** a typing script that physically types it into Word or Google Docs with forensic human keystroke simulation, use the [`ai-proof-writer`](https://github.com/enrico1c/ai-proof-writer) orchestrating skill instead.
