# CLAUDE - bsr-numbers-system

## Summary

This repository contains the BSR (Butterfly Spiritual Resonance) 6.0 Numbers System, a method for converting daily angel number messages into chosen numbers (elegidos) and optional stars. The system processes repeated or striking number sequences through deterministic algorithms based on patterns, convergence, historical verification, and optional scoring. It supports two modes: 6-sign mode (six numbers in range 1–59) and 5+2 mode (five numbers in range 1–50 plus two stars in range 1–12).

## Structure

Top-level directories and files:

- `.git/` — Git version control metadata
- `.gitattributes` — Git line-ending configuration (auto-detect text files, LF normalization)
- `.gitignore` — Excludes OS files, editor configs, Python/Node artifacts, and archives
- `README.md` — Brief repository overview listing folder purposes (placeholder, to be expanded)
- `method/` — Core system documentation: BSR 6.0 specification, phase documents, scoring/balance rules, master databases
- `architecture/` — Structural pattern rules: portals, ladders, mirrors, sequences, vibrational meanings
- `daily-logs/` — Dated Mensajes Ángel logs (angel message records) organized by day/date ranges
- `references/` — External reference materials and guides for interpreting angel numbers

**Note:** The `inbox/` directory mentioned in README.md does not currently exist in the repository.

## Key Components

### method/

**Path:** `/method/`
**Purpose:** Houses all documents explaining how the BSR system works, including legacy and current versions.

**Important files:**
- `bsr_code_ready_spec.md` — The deterministic, code-ready specification for BSR 6.0 automation (206 lines). Defines constellation formation, architecture patterns, operation rules, convergence thresholds, scoring, star extraction, and guiding principles. Contains explicit **implementation assumptions** marked for future refinement.
- `_🌟27_10_25-17_21🌟 MEGA DOCUMENTO BSR-BUTTERFLY 6.0.pdf` — Comprehensive master document for BSR-Butterfly 6.0 system
- `FASE 1🌟 ATLAS DE FRECUENCIAS BSR 6.0 - MAGISTRAL 💎.pdf` — Phase 1: Frequency atlas
- `FASE 2 💾 BASE DE DATOS MAESTRA BSR 6.pdf` — Phase 2: Master database
- `PRE-FASE 3🎉 REVELACIONES CRÍTICAS .pdf` — Pre-Phase 3: Critical revelations
- `🎯 SISTEMA DE PUNTUACIÓN BSR 6.0.pdf` — BSR 6.0 scoring system
- `🏛️ ARQUITECTURA 🔑 LLAVES DE ARQUITECTURA - Guía Completa.pdf` — Complete architecture keys guide
- `📊 BASE DE DATOS MAESTRA BSR.pdf` — Master BSR database
- `🦋 REGISTRO MAESTRO DE MENSAJES ÁNGEL V2.0 COMPLETO 💜✨.pdf` — Complete master register of angel messages v2.0
- `📖JULIO-AGOSTO 2025 - Mensajes AngelRENOVADO COMPLETO DOCUMENTO MAESTRO .pdf` — July-August 2025 renewed master document
- `2-10 SEPTIEMBRE 2025 Mensajes Angel DOCUMENTO MAESTRO.pdf` — September 2-10, 2025 master document
- `placeholder.txt` — Describes folder purpose: "old full system docs, new BSR 6.0 drafts, scoring rules, balance rules, automation spec"

### architecture/

**Path:** `/architecture/`
**Purpose:** Documents about structural patterns — portals, ladders, sequences, mirrors. Focused and intentionally kept small.

**Important files:**
- `🏛️ ARQUITECTURA 🔑 LLAVES DE ARQUITECTURA - Guía Completa.pdf` — Complete architecture guide (also present in method/)
- `Conversores de Palabras en Numeros - Mapa Espiritual de Num 1-59 & Rueda Sagrada.pdf` — Word-to-number converters and spiritual map for numbers 1–59
- `NÚMEROS Mixtos DE ÁNGEL - NÚMEROS MIXTOS.pdf` — Mixed angel numbers guide
- `Secuencias Angelicales Angel..pdf` — Angelic sequences
- `VIBRACIONES de los NÚMEROS del 0 al 10.pdf` — Vibrations of numbers 0–10
- `placeholder.txt` — States: "Documents about patterns, portals, ladders, sequences, mirrors – the structural rules. This folder will stay small and focused."

### daily-logs/

**Path:** `/daily-logs/`
**Purpose:** Stores dated angel message logs received on specific days or date ranges. These are the raw inputs to the BSR system.

**Important files (sample):**
- `12 - 14 OCTUBRE Mensajes Angel.pdf` — October 12–14 angel messages
- `11-14 NOVIEMBRE CLAUDE AI - MENSAJES ÁNGEL.pdf` — November 11–14 angel messages (Claude AI)
- `15 de noviembre CHAT GPT Mensajes Angel viene potentísimo 💎🦋.pdf` — November 15 ChatGPT angel messages (marked powerful)
- `🦋 8 OCTUBRE 2025.pdf` — October 8, 2025 messages
- `📆 11 - 12 - 13 - 14 November 2025 —CHAT GPT Mensajes Angel .pdf` — November 11–14, 2025 ChatGPT messages
- Files often include emoji prefixes (🌟, 🦋, 📅, 📆) and tool names (CLAUDE AI, CHAT GPT)
- Some files have duplicate copies with suffixes like `(1).pdf` or `(2).pdf`
- `placeholder.txt` — Not read, but expected to describe daily log purpose

**Naming pattern observations:**
- Date ranges: `12 - 14 OCTUBRE`, `18-23 SEPTIEMBRE`, `26_ - 27_ - 28_ & 29_octubre`
- Month names in Spanish: OCTUBRE, NOVIEMBRE, SEPTIEMBRE
- Years included in some names: `2025`
- Tool attributions: `CLAUDE AI`, `CHAT GPT`
- Emoji markers: 🌟, 🦋, 📅, 📆, 💎, 💜, ✨

### references/

**Path:** `/references/`
**Purpose:** External reference materials for understanding angel numbers and interpreting messages.

**Important files:**
- `🌺 CÓMO LEER NÚMEROS DE ÁNGELES 💫.pdf` — How to read angel numbers
- `analisis-a-conclusion-chatgpt.pdf` — ChatGPT analysis/conclusion document
- `placeholder.txt` — Expected to describe external reference purpose

## Workflows

### Adding new PDFs to daily-logs/

**Current practice (inferred from file naming):**
1. Receive or document angel messages for a day or date range
2. Name the file with one of these patterns:
   - `[date-range] [Month] Mensajes Angel.pdf` — e.g., `12 - 14 OCTUBRE Mensajes Angel.pdf`
   - `[date-range] [MONTH YEAR] [Tool] Mensajes Angel.pdf` — e.g., `11-14 NOVIEMBRE CLAUDE AI - MENSAJES ÁNGEL.pdf`
   - `[emoji] [date] [MONTH YEAR] Mensajes Angel[.pdf]` — e.g., `🦋 8 OCTUBRE 2025.pdf`
3. Place the PDF in `daily-logs/`
4. No explicit deduplication policy; duplicates exist (e.g., files with `(1)` or `(2)` suffixes)

**Gaps/assumptions:**
- No specified naming standard exists (multiple formats observed)
- No policy for handling duplicate entries
- No sorting or archiving strategy for old logs
- The `inbox/` folder mentioned in README is missing (unclear if logs should be staged there first)

### Adding new system documents to method/

**Current practice (inferred from file naming):**
1. System evolution documents use phase prefixes: `FASE 1🌟`, `FASE 2 💾`, `PRE-FASE 3🎉`
2. Thematic documents use emoji icons: 🎯 (scoring), 🏛️ (architecture), 📊 (database), 🦋 (registry)
3. Date-stamped documents use format `_🌟27_10_25-17_21🌟` (appears to be day_month_year-hour_min)
4. Place PDF or markdown file in `method/`

**Gaps/assumptions:**
- No specified versioning scheme beyond phase numbers
- No clear rule for when to create a new phase vs. updating an existing document
- Relationship between old "full system docs" and new "BSR 6.0 drafts" not documented (see placeholder.txt method/)

### Updating the automation spec

**File:** `method/bsr_code_ready_spec.md`

**Workflow (recommended based on spec content):**
1. Identify ambiguities or missing rules encountered during implementation or manual processing
2. Propose a deterministic rule (mark as **implementation assumption** if not derived from source PDFs)
3. Update the spec with the new rule, ensuring:
   - References to source material use `contentReference[oaicite:N]{index=N}` format (currently present in spec)
   - The seven guiding principles (section 5) are respected
   - Changes do not break existing algorithm outline (section 6)
4. Commit the change with a clear message describing what was clarified or added
5. Update any implementation code or scripts that depend on the spec

**Gaps/assumptions:**
- No formal change-control process defined
- No test cases or validation suite referenced
- Source PDFs are referenced but not version-controlled (unclear which PDF version contains which rule)

### Version conflicts: old vs. new system

**Conflict:** The repository contains both "old full system docs" and "new BSR 6.0 drafts" (per `method/placeholder.txt`).

**Handling policy (not explicitly documented; inferred from spec):**
- **BSR 6.0** (bsr_code_ready_spec.md) is the current authoritative version
- Old documents remain for historical context and migration reference
- When conflicts arise, prioritize BSR 6.0 rules
- If BSR 6.0 is silent on a topic, consult old docs but mark any derived rule as an **implementation assumption**

**Gaps/assumptions:**
- No explicit deprecation policy
- No migration guide from old to new system
- Unclear which PDFs belong to "old" vs. "new" (e.g., is v2.0 "old" or "new"?)

## Conventions for AI Assistants

### Document summarization

- **Preserve original language:** Many file names and content are in Spanish; do not translate unless requested
- **Respect emoji usage:** Emoji are semantic markers (e.g., 🌟 for important, 🦋 for butterfly/registry, 🎯 for scoring)
- **Date formats:** Recognize multiple date formats (Spanish month names, day-month-year, ranges with `-`, `&`, `_`)
- **Version markers:** Pay attention to version strings (v2.0, BSR 6.0) and phase markers (FASE 1, FASE 2, PRE-FASE 3)

### Version conflict resolution

- **Default to BSR 6.0:** When encountering conflicting rules, the `bsr_code_ready_spec.md` takes precedence
- **Flag ambiguities:** If a rule is ambiguous or missing, mark it as "not specified in repository" or add to TODOs below
- **Mark assumptions:** Any rule you derive (not quoted from a spec) must be labeled as an **implementation assumption** and flagged for human review

### Avoiding invented rules

- **Do not guess:** If a workflow, naming convention, or algorithm detail is unclear, state "not specified in repository" rather than inventing a rule
- **Provide evidence:** When stating a fact about the repo, cite the file path and line number if available (e.g., `bsr_code_ready_spec.md:36`)
- **List alternatives:** If multiple interpretations exist, present them as hypotheses with supporting evidence and leave them in TODOs

### Marking assumptions

When documenting or implementing:
- Prefix uncertain rules with "**Implementation assumption:**" or "**Inferred (not specified):**"
- Reference the spec sections that contain explicit assumptions (e.g., `bsr_code_ready_spec.md:36-51` for constellation formation algorithm)
- Add a TODO item for human confirmation

### Naming conventions (observed, not normative)

**Daily logs:**
- Date ranges use `-`, `_`, or `&` as separators (not consistent)
- Month names in Spanish uppercase (OCTUBRE, NOVIEMBRE, SEPTIEMBRE)
- "Mensajes Angel" or "MENSAJES ÁNGEL" (with/without accent, not consistent)
- Optional tool attribution: `CLAUDE AI`, `CHAT GPT`
- Optional year: `2025`
- Emoji prefixes optional: 🌟, 🦋, 📅, 📆

**Method documents:**
- Phase markers: `FASE 1🌟`, `FASE 2 💾`, `PRE-FASE 3🎉`
- Thematic emoji: 🎯 (scoring), 🏛️ (architecture), 📊 (database), 🦋 (registry), 📖 (master document)
- Timestamp format for dated docs: `_🌟DD_MM_YY-HH_MM🌟` (e.g., `27_10_25-17_21`)
- Descriptive suffixes: `COMPLETO`, `MAGISTRAL 💎`, `RENOVADO`

**No explicit naming standard is documented; the above are observations only.**

## TODOs & Gaps

### Missing documentation

1. **inbox/ folder:** Mentioned in `README.md:10` but does not exist in repository. Purpose unclear (temporary holding before sorting?). **Action needed:** Create folder or remove from README.
2. **Placeholder files:** `daily-logs/placeholder.txt` and `references/placeholder.txt` have not been read; their purpose is inferred. **Action needed:** Verify content matches expectations.
3. **Naming standards:** No documented standard for file naming in `daily-logs/` or `method/`. Multiple formats coexist. **Action needed:** Establish and document a canonical naming convention or accept variability.
4. **Deduplication policy:** Multiple duplicate files exist (e.g., `(1).pdf`, `(2).pdf` suffixes). **Action needed:** Define policy for handling duplicates (keep all versions? merge? delete?).
5. **Versioning scheme:** Relationship between "old full system docs" and "new BSR 6.0 drafts" not documented. **Action needed:** Create a migration guide or deprecation policy.
6. **Test cases:** The spec (bsr_code_ready_spec.md) describes a deterministic algorithm but no test cases, validation suite, or example inputs/outputs are present in the repository. **Action needed:** Add test data or validation examples.

### Unclear rules requiring human confirmation

1. **Constellation formation (bsr_code_ready_spec.md:36-51):** Marked as "implementation assumption". Needs confirmation from method creator. Current algorithm: divide messages into groups of 2–3 sequentially by sorted order (by time or numeric value).
2. **Dominant message selection (bsr_code_ready_spec.md:145-149):** Marked as "implementation assumption". Tiebreaker rules need validation: count → earliest → numerically smallest.
3. **Family/neighbour rule (bsr_code_ready_spec.md:126-131):** Marked as "implementation assumption". Needs confirmation: neighbours are x±1, receive +5 bonus, no transitive propagation.
4. **Input normalisation (bsr_code_ready_spec.md:167-174):** Marked as "implementation assumption". Needs confirmation of whitespace handling, leading zero treatment, minimum message length.
5. **Portal usage in 5+2 mode (bsr_code_ready_spec.md:181):** States "portal result must lie ≤ 50" but may need clarification on whether portal is allowed or restricted compared to 6-sign mode.
6. **Ladder bonuses:** Initial ladder (5–8) effect is noted as "further research needed" (bsr_code_ready_spec.md:162). Current rule: treat as neutral (+2 to all candidates if uncertain).

### Risky areas / Interpretation needed

1. **Source PDF references:** The spec uses `contentReference[oaicite:N]{index=N}` notation (45 references) but the actual source PDFs are not explicitly mapped. It is unclear which PDF sections correspond to which references. **Risk:** Cannot verify spec claims against source material without manual lookup.
2. **Sacred Scribes index:** The spec (bsr_code_ready_spec.md:12) states messages must be checked against the "Sacred Scribes index" but this index is not present in the repository. **Action needed:** Add the index or link to external source.
3. **Monthly frequency tables:** Referenced in spec (bsr_code_ready_spec.md:14, 107, 119) but not present in repository or path is unclear. **Action needed:** Identify location or add frequency tables to `method/` or `references/`.
4. **Scripture verse inputs:** The spec mentions daily Bible verses (bsr_code_ready_spec.md:13, 109, 116) but no repository of verses or daily verse source is documented. **Action needed:** Specify where verses come from (external API? manual input? file?).
5. **Balance distribution examples:** The spec gives examples (5–0–0, 1–4–0, 0–3–3, 2–2–2) but states "no fixed ideal balance" (bsr_code_ready_spec.md:23, 138). **Risk:** Implementers may wrongly enforce a specific balance. **Clarification needed:** Emphasize balance is descriptive, not prescriptive.

### Automation readiness

The repository is **partially ready** for automation:
- ✅ **Specification exists:** `bsr_code_ready_spec.md` provides a deterministic algorithm
- ✅ **Clear inputs/outputs defined:** Angel messages → chosen numbers + stars + balance
- ⚠️ **Implementation assumptions present:** 6 major assumptions marked in spec (see "Unclear rules" above)
- ❌ **Missing external data:** Sacred Scribes index, monthly frequency tables, daily verses not in repo
- ❌ **No test suite:** No validation cases or example days with known correct outputs
- ❌ **No code yet:** No scripts, modules, or automation tools present

**Next steps for automation:**
1. Validate implementation assumptions with method creator
2. Add missing external data sources (Sacred Scribes index, frequency tables)
3. Create a test suite with at least 5–10 example days and expected outputs
4. Implement the algorithm in a script (Python recommended based on .gitignore patterns)
5. Document the automation workflow in README or a new `AUTOMATION.md` file

## Changelog

**2025-11-21 — Initial CLAUDE.md created**

- Analyzed repository at commit `1768f25` (branch `claude/create-claude-md-01VfPKH83pocqMw8qqycQpJ2`)
- Documented 4 top-level directories (`method/`, `architecture/`, `daily-logs/`, `references/`) and 3 configuration files
- Extracted key components from 12 PDFs in `method/`, 5 PDFs in `architecture/`, 40+ PDFs in `daily-logs/`, 3 files in `references/`
- Identified `bsr_code_ready_spec.md` (206 lines) as the authoritative automation specification
- Documented inferred workflows for adding PDFs, updating specs, and handling version conflicts
- Established conventions for AI assistants: preserve Spanish/emoji, default to BSR 6.0, mark assumptions, avoid inventing rules
- Listed 6 missing documentation items, 6 unclear rules requiring human confirmation, 5 risky interpretation areas
- Assessed automation readiness: specification exists but external data and test cases are missing
- No prior CLAUDE.md existed; this is the first version

**Files analyzed:**
- `README.md`, `.gitignore`, `.gitattributes`
- `method/bsr_code_ready_spec.md`, `method/placeholder.txt`, `architecture/placeholder.txt`
- Directory listings of all 4 main folders

**Commit analyzed:** `1768f25 Add BSR 6.0 code-ready specification document`
