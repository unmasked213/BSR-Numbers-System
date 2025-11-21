# architecture/

## Purpose

This folder documents the **structural patterns and symbolic meanings** that form the foundation of how numbers relate to each other in the BSR system. While the `method/` folder explains the rules and algorithms, this folder explains the underlying patterns those rules recognize.

Think of this as a reference library of "number relationships" – the bridges, connections, and transformations that give certain number combinations special significance.

## What Belongs Here

Documents in this folder describe specific types of patterns and relationships:

### Pattern Types

1. **Portals** – Special numbers or number combinations that act as bridges or gateways, transforming one number into another through mathematical operations
2. **Ladders** – Sequential patterns where numbers form steps or progressions (e.g., 5-6-7-8)
3. **Mirrors** – Numbers that reflect or complement each other in meaningful ways
4. **Sequences** – Ordered patterns with specific angelic or spiritual significance
5. **Mixed numbers** – Combinations that blend multiple meanings or energies

### Symbolic Meanings

1. **Vibrational meanings** – The spiritual, energetic, or symbolic qualities associated with individual numbers (0-59)
2. **Word-to-number converters** – Systems for translating words, concepts, or names into numeric equivalents
3. **Sacred wheels and maps** – Visual or conceptual frameworks showing how numbers relate spatially or symbolically

## Current Documents

- **`🏛️ ARQUITECTURA 🔑 LLAVES DE ARQUITECTURA - Guía Completa.pdf`** – The comprehensive architecture guide covering all key pattern types
- **`Conversores de Palabras en Numeros - Mapa Espiritual de Num 1-59 & Rueda Sagrada.pdf`** – Word-to-number conversion systems and spiritual maps
- **`NÚMEROS Mixtos DE ÁNGEL - NÚMEROS MIXTOS.pdf`** – Guide to mixed angel number patterns
- **`Secuencias Angelicales Angel..pdf`** – Angelic sequence patterns and their meanings
- **`VIBRACIONES de los NÚMEROS del 0 al 10.pdf`** – Detailed vibrational meanings of numbers 0-10

## How This Folder Contributes to the System

The patterns documented in `architecture/` are not just decorative or symbolic – they are **actively used by the BSR algorithm** when processing angel messages.

When the BSR system:
- **Detects a portal** → It may transform a number according to portal rules
- **Identifies a ladder** → It may apply bonus points to candidates forming ladder patterns
- **Recognizes a sequence** → It may prioritize those numbers as convergence candidates
- **Finds mirrors** → It may link related numbers or validate choices through symmetry

Without the patterns defined in this folder, the BSR system would be reduced to pure frequency counting. The architecture documents provide the **semantic layer** that gives numbers meaning beyond their raw appearance count.

### Example: How Architecture Influences Selection

Imagine the system processes these angel messages for a day:
```
555, 777, 888, 567, 678
```

**Without architecture knowledge:**
- The system would just count: 5 appears 4 times, 7 appears 5 times, 8 appears 5 times
- It might select 7 and 8 as high-frequency numbers

**With architecture knowledge:**
- The system recognizes 567 and 678 as **ladder patterns**
- The ladder pattern receives bonus points in the scoring system
- It might prioritize 5-6-7-8 as a constellation because of the structural pattern
- The portal connections between certain numbers may transform candidates
- Vibrational meanings help break ties between equally frequent numbers

This is why `architecture/` exists as a separate folder – these patterns are foundational but conceptually distinct from the algorithmic rules in `method/`.

## Relationship to `method/`

There is some intentional overlap between `architecture/` and `method/`:

- The file **`🏛️ ARQUITECTURA 🔑 LLAVES DE ARQUITECTURA - Guía Completa.pdf`** appears in both folders
- Architecture patterns are **referenced** in `method/bsr_code_ready_spec.md` (the BSR 6.0 specification)

This is by design:
- **`architecture/`** focuses on **what patterns exist and what they mean**
- **`method/`** focuses on **how to detect patterns and how they affect scoring**

When in doubt:
- For pattern definitions and meanings → Consult `architecture/`
- For pattern detection algorithms and scoring rules → Consult `method/`

## Design Philosophy: Small and Focused

This folder is **intentionally kept small**.

Unlike `method/`, which may grow as the system evolves (new phases, databases, master logs), the `architecture/` folder documents foundational patterns that are relatively stable. New pattern types may be discovered occasionally, but the core relationships (portals, ladders, mirrors, sequences, vibrations) form a stable base.

If you're adding a document to this repository, ask:
- Is this about **what a pattern means**? → `architecture/`
- Is this about **how to apply or score a pattern**? → `method/`
- Is this about **raw input data (messages received)**? → `daily-logs/`
- Is this about **external interpretation resources**? → `references/`

## Adding Documents to This Folder

When adding new documents to `architecture/`, ensure they:

1. **Focus on patterns and relationships** – Not algorithms or step-by-step procedures
2. **Provide meanings and interpretations** – What does this pattern represent? Why is it significant?
3. **Remain conceptually clear** – These documents should be understandable without deep technical knowledge
4. **Avoid duplication** – If a pattern is already covered elsewhere, consider updating the existing document rather than creating a new one

### Naming Conventions

Observed patterns (not strict rules):
- Use descriptive names that clearly indicate the pattern type: `NÚMEROS Mixtos DE ÁNGEL`, `Secuencias Angelicales`, `VIBRACIONES de los NÚMEROS`
- Emoji prefixes are optional but semantically meaningful: 🏛️ for architecture/structure
- Preserve Spanish names when appropriate (many concepts originate in Spanish-language materials)

## For Newcomers

If you're new to the BSR system and want to understand the patterns:

1. **Start with vibrational meanings:** Read `VIBRACIONES de los NÚMEROS del 0 al 10.pdf` to understand how individual numbers carry energy and meaning
2. **Learn the architecture keys:** Read `🏛️ ARQUITECTURA 🔑 LLAVES DE ARQUITECTURA - Guía Completa.pdf` for a comprehensive overview of all pattern types
3. **Study sequences:** Read `Secuencias Angelicales Angel..pdf` to see how numbers form meaningful ordered patterns
4. **Explore mixed numbers:** Read `NÚMEROS Mixtos DE ÁNGEL` to understand compound meanings
5. **See the spiritual map:** Review `Conversores de Palabras en Numeros` to understand the broader symbolic framework

You don't need to memorize every pattern – even experienced practitioners refer to these documents regularly. The goal is to develop familiarity with the types of relationships that exist, so you can recognize them when they appear in daily messages.

## Usage in Automation

When automating the BSR system:

- **Pattern detection** will need to be coded based on these documents
- **Portal operations** will need clear mathematical definitions (work in progress in `bsr_code_ready_spec.md`)
- **Ladder detection** requires defining what constitutes a valid ladder (e.g., 5-6-7-8 vs. 5-7-9)
- **Vibrational meanings** may be stored in lookup tables for scoring or tiebreaking

The documents in this folder are primarily in PDF format and written for human interpretation. Converting these concepts into code will require:
1. Extracting explicit rules from the PDFs
2. Defining edge cases and ambiguities
3. Creating deterministic algorithms for pattern detection
4. Adding these algorithms to `method/bsr_code_ready_spec.md`

This work is part of the roadmap for full BSR system automation.

## Status: Foundational Patterns Documented

The documents in this folder provide a **solid foundation** for understanding BSR architecture patterns. However:
- Some pattern rules are described qualitatively, not quantitatively
- Not all edge cases are explicitly defined
- Translation from symbolic/spiritual language to deterministic code is ongoing

These gaps are expected and being addressed through the `method/bsr_code_ready_spec.md` implementation assumptions.

---

**Questions about patterns?** Consult the documents here. For questions about how patterns affect the algorithm, see `method/`. For questions about repository organization, see the root `README.md` or `CLAUDE.md`.

**Last updated:** 2025-11-21
