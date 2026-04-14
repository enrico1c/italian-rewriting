---
name: italian-rewriting
description: Rewrite source material (PDF, raw text, docx content) into natural, academic Italian prose — eliminating AI-generated patterns, em-dashes, and mechanical phrasing while preserving every factual claim exactly.
level: 3
---

# Italian Rewriting

Rewrite source material into fluent, academic Italian prose suitable for university coursework. Preserves every fact, number, legal reference, and structural claim exactly — changes only the language surface. Eliminates all AI-generation fingerprints (em-dashes, bullet-to-prose dumps, robotic connectives) and replaces them with idiomatic Italian academic register.

## When to Use

Use this skill when:
- the user provides a PDF, docx, or raw text and asks to rewrite it in Italian
- the source is a slide deck, bullet-point outline, or rough draft to be converted into continuous prose
- the goal is academic Italian (university paper, group project, thesis chapter)
- the user says "riscrivilo in italiano", "rendi il testo più naturale", or similar
- the output must have no em-dashes, no list dumps masquerading as paragraphs, no AI slop

Do **not** use when:
- the user wants a translation only (not a rewrite/naturalisation)
- the source language is already polished Italian
- the output target is informal or non-academic Italian

---

## Core Principles

### 1. Factual fidelity — zero tolerance for invention
Every number, citation, legal article, institution name, percentage, date, and proper noun must match the source exactly. If the source says "55-65% delle previsioni", the output must say exactly that — not "circa il 60%". If uncertain about a fact, keep the source wording verbatim inside the rewritten sentence.

### 2. Em-dash elimination
Em-dashes (—) are an AI fingerprint in Italian. Replace every instance:
- " — " (space–em-dash–space) → ", " or restructure the clause
- "— " at sentence/bullet start → delete or rephrase as full sentence
- Bare "—" → "," or restructure
- After replacement: clean up ", ," → "," · ": ," → ":" · ",." → "." · ",;" → ";"

### 3. Academic register
Target: Italian university paper (Scienza delle Finanze / Law / Economics level). This means:
- Complex but readable sentences (not telegraphic, not overly convoluted)
- Appropriate hedging: "si può osservare", "appare evidente", "vale la pena sottolineare"
- Passive constructions where natural: "è stato documentato", "si prevede", "viene classificato"
- No colloquialisms, no anglicisms unless the technical term has no Italian equivalent
- Numbered section headings in the form "1.  Titolo" (two spaces after the dot)

### 4. No bullet dumps
Bullet lists from the source must be absorbed into prose paragraphs. Each bullet becomes a clause or sentence. Use connectives: "In primo luogo … In secondo luogo … Infine …", "da un lato … dall'altro …", "sotto il profilo giuridico … sotto quello tecnico …"

Exception: structured tables (legal maps, comparison grids, sensitivity tables) stay as tables — do not prose-ify data.

### 5. Paragraph structure
Each paragraph should:
- Open with a topic sentence that carries the main claim
- Develop it with 2-4 supporting sentences
- Close with a consequence or transition
- Run 80–180 words (academic norm, not a hard cap)

### 6. Italian punctuation norms
- Quotation marks: «testo» (guillemets), not "testo"
- Abbreviations: art., D.L., L., D.Lgs., c.c. (no spaces inside)
- Decimal separator: comma (3,8% not 3.8%)
- Thousands separator: punto (1.000 not 1,000)
- Subscripts: P₀, Fₜ, VT (keep Unicode as-is if source uses them)

---

## Workflow

### Step 0 — Understand the source
Read the full source before writing a single word. Identify:
- Document type (slides / draft / raw PDF extract)
- Section structure (what are the h1/h2 sections?)
- All factual anchors: numbers, citations, laws, institutions
- Any em-dashes or AI slop patterns to flag

### Step 1 — Plan the output structure
Map source sections → output sections. If the source is a slide deck, infer a prose structure (intro → body sections → conclusion → bibliography). Show the user the planned structure before writing if the source is large or ambiguous.

### Step 2 — Rewrite section by section
For each section:
1. Absorb all bullet points into flowing prose
2. Eliminate em-dashes with the substitution rules above
3. Apply academic register
4. Verify every factual claim against the source text
5. Check paragraph length and structure

### Step 3 — Post-process pass
After drafting, run a final check:
- [ ] Zero em-dashes remaining
- [ ] Every number/citation matches source
- [ ] No double commas, colon-commas, or period-commas
- [ ] Section numbering is sequential and consistent
- [ ] Bibliography (if present) is collected at the end as a single block

### Step 4 — Output format
If writing to a Word document (.docx), generate a Python script using `python-docx` that:
- Uses Calibri 11pt Normal style
- Uses heading level 1 (navy `#1F497D`) for h1, heading level 2 (blue `#2E74B5`) for h2
- Justifies all body paragraphs
- Adds tables with `'Table Grid'` style
- Outputs to the user-specified path

If writing to plain text, output raw Italian markdown.

---

## Em-Dash Substitution Reference

| Source pattern | Italian replacement |
|---|---|
| `X — Y` (parenthetical) | `X, Y` or `X: Y` depending on context |
| `X — Y — Z` (nested aside) | rephrase as subordinate clause |
| `— item` (bullet marker) | delete; item becomes a standalone sentence |
| `X —` (trailing) | `X,` or end sentence |
| `ovvero —` | `ovvero:` |
| `cioè —` | `cioè:` |

---

## Italian Academic Connectives Palette

Use these to replace mechanical bullet-list structure:

**Additive:** inoltre, altresì, d'altra parte, va aggiunto che, occorre precisare che  
**Contrastive:** tuttavia, ciononostante, pur riconoscendo che, al contrario, per converso  
**Causal:** pertanto, ne consegue che, da ciò deriva, si evince che, in ragione di  
**Sequential:** in primo luogo … in secondo luogo … infine; dapprima … successivamente … da ultimo  
**Exemplificative:** a titolo esemplificativo, si consideri il caso di, come emerge da, come documentato da  
**Concessive:** pur ammettendo che, anche laddove, sebbene, nonostante  
**Reformulating:** in altri termini, vale a dire, detto altrimenti, più precisamente  

---

## Quality Gates

Before delivering the output, verify:
1. **Factual accuracy** — spot-check 5 random facts against source
2. **Em-dash count** — search output for `—`; must be zero
3. **Register consistency** — no colloquialisms or anglicisms
4. **Structure completeness** — all source sections represented
5. **Bibliography** — single block at end if source had references

---

## Usage

```
/italian-rewriting
```

Then paste or attach the source material. Optionally specify:
- Output format: `--docx <path>` or `--markdown` (default)
- Target section: `--section "4.1"` to rewrite only a specific section
- Register: `--register accademico` (default) or `--registro saggistico`

### Example invocation

```
/italian-rewriting --docx "C:/Users/.../output.docx"

[paste PDF extract or raw text below]
```

---

## What the Skill Produces (from session evidence)

In the session that defined this skill, the input was a pair of PDFs (slides + rough draft) and the output was:

- Two polished Italian docx chapters (~8,000 words combined)
- Zero em-dashes (verified by regex scan)
- Natural Italian paragraph structure throughout
- All legal citations (art. 11-quinquies DL 203/2005, L. 89/2014, etc.) preserved verbatim
- All statistics (SCIP 55-65%, FIV geographic distribution, sensitivity table values) intact
- Academic register appropriate for LUISS Scienza delle Finanze coursework
- Final merged file via `create_final.py` with page break between chapters

Scripts used:
- `gen_doc1.py` — generates chapter 1 (vendita/razionalità)
- `gen_doc2.py` — generates chapter 2 (valorizzabilità)
- `create_final.py` — merges both into final docx, strips remaining em-dashes
