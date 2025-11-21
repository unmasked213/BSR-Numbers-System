# BSR Numbers System

A deterministic method for converting daily angel number messages into chosen numbers (elegidos) and optional stars.

---

## What This Repository Is

The BSR (Butterfly Spiritual Resonance) 6.0 Numbers System is a numerical decoding method under active development. It processes sequences of repeated or striking numbers observed daily and converts them into final output numbers through a reproducible algorithm based on pattern recognition, convergence analysis, historical verification, and optional scoring.

The system supports two output modes:
- **6-sign mode:** Six chosen numbers, each in the range 1–59
- **5+2 mode:** Five chosen numbers (1–50) plus two stars (1–12)

This repository contains the specification documents, reference materials, daily input logs, and structural pattern rules that define how the system operates. The goal is to transition from an intuitive manual practice to a fully automated, deterministic process.

---

## Folder Structure

Every top-level file and directory in this repository:

| Path | Purpose |
|------|---------|
| `.git/` | Git version control metadata |
| `.gitattributes` | Git line-ending configuration (auto-detect text files, LF normalisation) |
| `.gitignore` | Excludes OS files, editor configs, Python/Node artifacts, archives |
| `CLAUDE.md` | Detailed project instructions for AI assistants |
| `README.md` | This file – repository overview and usage guide |
| `method/` | Core system documentation: specs, phases, scoring/balance rules, master databases |
| `architecture/` | Structural pattern rules: portals, ladders, mirrors, sequences, vibrational meanings |
| `daily-logs/` | Dated angel message logs (input data) organised by day or date ranges |
| `references/` | External reference materials for interpreting angel numbers |

**Note:** The `inbox/` folder mentioned in previous versions does not currently exist.

---

## What's in Each Folder

### `method/` (12 files)

Core system documentation explaining how BSR works:

- **`bsr_code_ready_spec.md`** — The authoritative, deterministic specification for BSR 6.0 automation (206 lines). Defines constellation formation, architecture patterns, operation rules, convergence thresholds, scoring, star extraction, and guiding principles. Contains explicit **implementation assumptions** marked for future refinement.
- **PDF documents:**
  - `_🌟27_10_25-17_21🌟 MEGA DOCUMENTO BSR-BUTTERFLY 6.0.pdf` — Comprehensive master document for BSR-Butterfly 6.0
  - `FASE 1🌟 ATLAS DE FRECUENCIAS BSR 6.0 - MAGISTRAL 💎.pdf` — Phase 1: Frequency atlas
  - `FASE 2 💾 BASE DE DATOS MAESTRA BSR 6.pdf` — Phase 2: Master database
  - `PRE-FASE 3🎉 REVELACIONES CRÍTICAS .pdf` — Pre-Phase 3: Critical revelations
  - `🎯 SISTEMA DE PUNTUACIÓN BSR 6.0.pdf` — Scoring system rules
  - `🏛️ ARQUITECTURA 🔑 LLAVES DE ARQUITECTURA - Guía Completa.pdf` — Complete architecture keys guide
  - `📊 BASE DE DATOS MAESTRA BSR.pdf` — Master BSR database
  - `🦋 REGISTRO MAESTRO DE MENSAJES ÁNGEL V2.0 COMPLETO 💜✨.pdf` — Complete master register of angel messages v2.0
  - `📖JULIO-AGOSTO 2025 - Mensajes AngelRENOVADO COMPLETO DOCUMENTO MAESTRO .pdf` — July-August 2025 master document
  - `2-10 SEPTIEMBRE 2025 Mensajes Angel DOCUMENTO MAESTRO.pdf` — September 2-10, 2025 master document
- **`placeholder.txt`** — Folder purpose description

**Key point:** BSR 6.0 (bsr_code_ready_spec.md) is the current authoritative version. Older documents remain for historical context.

### `architecture/` (5 files)

Documentation of structural patterns used in number decoding:

- `🏛️ ARQUITECTURA 🔑 LLAVES DE ARQUITECTURA - Guía Completa.pdf` — Complete architecture guide
- `Conversores de Palabras en Numeros - Mapa Espiritual de Num 1-59 & Rueda Sagrada.pdf` — Word-to-number converters and spiritual map
- `NÚMEROS Mixtos DE ÁNGEL - NÚMEROS MIXTOS.pdf` — Mixed angel numbers guide
- `Secuencias Angelicales Angel..pdf` — Angelic sequences
- `VIBRACIONES de los NÚMEROS del 0 al 10.pdf` — Vibrations of numbers 0–10

This folder documents the rules for portals, ladders, sequences, mirrors, and other structural patterns. It is intentionally kept small and focused.

### `daily-logs/` (37 files)

Raw input data: dated angel message logs received on specific days or date ranges. These logs are the primary inputs to the BSR system.

**Naming patterns observed:**
- Date ranges: `12 - 14 OCTUBRE`, `18-23 SEPTIEMBRE`, `26_ - 27_ - 28_ & 29_octubre`
- Month names in Spanish: `OCTUBRE`, `NOVIEMBRE`, `SEPTIEMBRE`
- Years: `2025` (when specified)
- Tool attributions: `CLAUDE AI`, `CHAT GPT`
- Emoji markers: 🌟, 🦋, 📅, 📆, 💎, 💜, ✨

**Sample files:**
- `12 - 14 OCTUBRE Mensajes Angel.pdf`
- `11-14 NOVIEMBRE CLAUDE AI - MENSAJES ÁNGEL.pdf`
- `15 de noviembre CHAT GPT Mensajes Angel viene potentísimo 💎🦋.pdf`
- `🦋 8 OCTUBRE 2025.pdf`
- `📆 11 - 12 - 13 - 14 November 2025 —CHAT GPT Mensajes Angel .pdf`

**Note:** Some duplicate files exist (with suffixes like `(1).pdf` or `(2).pdf`).

### `references/` (3 files)

External reference materials for understanding and interpreting angel numbers:

- `🌺 CÓMO LEER NÚMEROS DE ÁNGELES 💫.pdf` — How to read angel numbers
- `analisis-a-conclusion-chatgpt.pdf` — ChatGPT analysis/conclusion document
- `placeholder.txt` — Folder purpose description

---

## How to Add New Documents

### Adding angel message logs to `daily-logs/`

**Recommended naming patterns (based on existing files):**

1. **Date range + month:**
   `[date-range] [MONTH] Mensajes Angel.pdf`
   Example: `12 - 14 OCTUBRE Mensajes Angel.pdf`

2. **Date range + month + year + tool:**
   `[date-range] [MONTH YEAR] [Tool] Mensajes Angel.pdf`
   Example: `11-14 NOVIEMBRE 2025 CLAUDE AI - MENSAJES ÁNGEL.pdf`

3. **Emoji + date:**
   `[emoji] [date] [MONTH YEAR].pdf`
   Example: `🦋 8 OCTUBRE 2025.pdf`

**Guidelines:**
- Use Spanish month names in uppercase (OCTUBRE, NOVIEMBRE, etc.)
- Include year when documenting current or future logs
- Optionally include tool attribution (CLAUDE AI, CHAT GPT)
- Emoji prefixes are optional but semantically meaningful (🌟 important, 🦋 registry, 📅/📆 calendar)
- Place the PDF directly in `daily-logs/`

**No formal deduplication policy exists yet.** If you have multiple versions of the same day's messages, consider using descriptive suffixes.

### Adding system documents to `method/`

**Naming conventions observed:**

1. **Phase markers:**
   `FASE [N][emoji] [Description].pdf`
   Example: `FASE 1🌟 ATLAS DE FRECUENCIAS BSR 6.0 - MAGISTRAL 💎.pdf`

2. **Thematic documents:**
   `[emoji] [Description].pdf`
   - 🎯 = scoring
   - 🏛️ = architecture
   - 📊 = database
   - 🦋 = registry
   - 📖 = master document

3. **Dated documents:**
   `_🌟[DD_MM_YY-HH_MM]🌟 [Description].pdf`
   Example: `_🌟27_10_25-17_21🌟 MEGA DOCUMENTO BSR-BUTTERFLY 6.0.pdf`

**For updating the automation spec (`bsr_code_ready_spec.md`):**

1. Identify ambiguities or missing rules during implementation
2. Propose a deterministic rule (mark as **implementation assumption** if not derived from source PDFs)
3. Update the spec, ensuring compatibility with the seven guiding principles (section 5) and algorithm outline (section 6)
4. Commit with a clear message describing what was clarified or added

### Adding pattern documentation to `architecture/`

Place focused, standalone documents about structural patterns (portals, ladders, sequences, mirrors) in this folder. Keep documents concise and avoid duplicating content from `method/`.

### Adding reference materials to `references/`

External guides, angel number interpretation resources, and third-party reference documents go here.

---

## Current Status and Roadmap

### ✅ What Exists Now

- **Specification:** The code-ready BSR 6.0 specification (`method/bsr_code_ready_spec.md`) defines a deterministic algorithm with explicit inputs, outputs, and processing steps
- **Documentation:** 12 PDFs in `method/` cover system phases, scoring rules, databases, and historical records
- **Pattern rules:** 5 documents in `architecture/` define structural patterns (portals, ladders, mirrors, sequences)
- **Input data:** 37 dated message logs in `daily-logs/` (spanning multiple months in 2025)
- **Reference materials:** 3 files in `references/` for interpreting angel numbers
- **Project instructions:** `CLAUDE.md` provides detailed guidance for AI assistants

### ⚠️ What's in Progress

- **Implementation assumptions:** 6 major assumptions in `bsr_code_ready_spec.md` require validation by the method creator:
  - Constellation formation algorithm (lines 36-51)
  - Dominant message selection (lines 145-149)
  - Family/neighbour rule (lines 126-131)
  - Input normalisation (lines 167-174)
  - Portal usage in 5+2 mode (line 181)
  - Ladder bonuses (line 162)

### 🔄 What's Planned

1. **External data integration:**
   - Add Sacred Scribes angel number index to `references/`
   - Add monthly frequency tables to `method/` or `references/`
   - Document source for daily scripture verses

2. **Test suite:**
   - Create 5–10 example days with known correct outputs
   - Add validation cases for edge scenarios (portal usage, ladder detection, tie-breaking)

3. **Automation:**
   - Implement the BSR 6.0 algorithm in Python (based on `.gitignore` patterns)
   - Build input parser for daily message logs
   - Create output formatter for chosen numbers and stars

4. **Documentation improvements:**
   - Establish formal naming conventions for files in `daily-logs/` and `method/`
   - Define deduplication policy for log files
   - Create migration guide from old system versions to BSR 6.0

5. **Repository organisation:**
   - Decide whether to create `inbox/` folder (mentioned in old README but doesn't exist)
   - Archive or clearly label deprecated documents

---

## How Automation Will Be Developed

The repository is **partially ready** for automation:

**✅ Ready:**
- Deterministic specification exists (`bsr_code_ready_spec.md`)
- Clear inputs defined (angel messages, scripture verse, historical context)
- Clear outputs defined (chosen numbers, stars, balance distribution)
- Algorithm outline provided (section 6 of spec)

**⚠️ Needs attention:**
- 6 implementation assumptions require validation
- Missing external data (Sacred Scribes index, frequency tables)
- No test cases or validation suite yet
- No code or scripts present yet

**Automation development steps:**

1. **Validate assumptions** — Confirm the 6 implementation assumptions with the method creator
2. **Add missing data** — Integrate Sacred Scribes index and monthly frequency tables into repository
3. **Create test suite** — Document 5–10 example days with expected outputs for validation
4. **Implement core algorithm** — Code the BSR 6.0 spec in Python, following the deterministic rules in `bsr_code_ready_spec.md`
5. **Build input parser** — Read and normalise angel message logs from `daily-logs/`
6. **Build output formatter** — Generate chosen numbers, stars, and balance reports
7. **Document the automation workflow** — Create usage guide for running the system

**Algorithm overview (from `bsr_code_ready_spec.md:194-204`):**

1. Prepare inputs: normalise and verify messages; extract numeric hints from verse; load frequency table
2. Group messages into constellations deterministically
3. For each constellation: identify patterns; build pool; generate candidates; prioritise routes
4. Collect candidates across constellations and determine convergence; apply historical verification
5. Apply scoring if needed; include ladder and neighbour bonuses; sort by points
6. Select final numbers ensuring range compliance; compute balance
7. Extract stars (if 5+2 mode) from dominant message
8. Document process for auditing

---

## Working with This Repository

This is a personal project for tracking and processing angel number messages. The repository serves as both documentation and a foundation for future automation.

### For AI Assistants

Detailed instructions for AI assistants working with this repository are in `CLAUDE.md`. Key points:

- Default to BSR 6.0 rules (bsr_code_ready_spec.md)
- Flag ambiguities; do not guess missing rules
- Cite file paths and line numbers when stating facts
- Recognise multiple date formats (Spanish month names, various separator styles)
- Pay attention to version markers (v2.0, BSR 6.0, FASE 1/2/3)
- Preserve original language (many file names and content are in Spanish)
- Respect emoji usage as semantic markers (🌟 = important, 🦋 = registry, 🎯 = scoring, 🏛️ = architecture)

---

## Further Reading

- **`CLAUDE.md`** — Comprehensive project instructions, conventions, TODOs, and gaps
- **`method/bsr_code_ready_spec.md`** — The complete BSR 6.0 algorithm specification
- **`method/` PDFs** — Phase documents, scoring rules, databases, and master registers

For questions about the method itself, consult the documents in `method/`. For questions about repository organisation or automation, consult `CLAUDE.md` or open an issue.

---

**Last updated:** 2025-11-21
**Current branch:** `claude/write-bsr-readme-01SyTQM6hdev3L6rtRRYnnxx`
**Repository status:** Specification complete; automation in planning phase
