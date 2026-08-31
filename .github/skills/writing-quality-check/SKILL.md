---
name: writing-quality-check
description: 'Writing quality rules for clear, precise academic prose. Use when: reviewing drafts for common AI-text patterns (flagged terms, punctuation overuse, throat-clearing, structural tics, monotonous rhythm); self-editing research papers, proposals, or articles; improving sentence-level clarity and variation; ensuring consistent terminology and natural paragraph rhythm. Includes term warnings, punctuation guidelines, structure pattern detection, and burstiness checks.'
---

# Writing Quality Check

## Purpose

A set of writing quality rules extracted from common patterns in AI-generated text. **These are good writing rules that apply regardless of source — human or AI-generated.** The goal is clear, precise, varied academic prose.

> **Design boundary**: This checklist improves writing quality. It is NOT a humanizer. We do not aim to fool AI detectors. We aim to produce rigorous, readable academic work.

---

## When to Use This Skill

- You're reviewing a draft for common patterns that weaken prose clarity
- You notice repetitive structures, flagged terms, or punctuation tics
- You want to vary sentence rhythm and paragraph structure
- You're doing final self-review before submitting an article, proposal, or report
- You're editing another agent's output for academic polish

---

## Core Principles

### 1. Precision Over Default Vocabulary

When you encounter a flagged term, ask: **"Is this really the most precise word here?"** Many default terms (delve, landscape, robust, navigate) are not wrong — but often a more specific alternative exists in context.

### 2. Variation Is a Virtue

Natural academic writing has rhythm created by varied sentence length, paragraph structure, and punctuation patterns. Monotony signals template-generated text.

### 3. Structure Follows Content

Different sections serve different purposes. Methods can be procedural with uniform structure. Discussion should be exploratory with varied rhythm. Let form follow function, not templates.

### 4. Clarity Over Cliché

Throat-clearing phrases and meta-commentary add no information. Cut them. If an idea is important, the evidence speaks for itself.

---

## Quick Reference: Five Problem Areas

| Problem Area | What to Check | Reference |
|--------------|---------------|-----------|
| **Flagged Terms** | Are you using overused default terms when a more precise alternative exists? | [high-frequency-terms.md](./references/high-frequency-terms.md) |
| **Punctuation Patterns** | Em dash overuse (>3 per paper), semicolon chaining, colon-list monotony? | [punctuation-patterns.md](./references/punctuation-patterns.md) |
| **Throat-Clearing** | Opening sentences that describe the writing instead of doing the writing? | [throat-clearing.md](./references/throat-clearing.md) |
| **Structure Tics** | Rule-of-three compulsion, uniform paragraphs, synonym cycling, binary contrasts? | [structure-patterns.md](./references/structure-patterns.md) |
| **Burstiness** | Monotonous sentence length variation; lack of rhythm? | [burstiness.md](./references/burstiness.md) |

---

## Review Workflow

### During Drafting (Recommended)

Apply this checklist **while writing each section** in a self-review pass. Catch issues before they propagate.

**Steps:**
1. Write the section
2. Read aloud for rhythm (feel for monotony)
3. Scan for flagged terms → replace if a more precise word fits
4. Check punctuation pattern counts (em dashes, semicolons, colon lists)
5. Cut any throat-clearing openers
6. Verify section structure is **fit to content**, not templated
7. Check sentence-length burstiness in the final paragraph

### During Final Review (Fallback)

If not applied during drafting, run a full-paper sweep before handoff to the next stage.

**Speed version (15 minutes per 5K words):**
1. Scan for flagged terms in topic sentences and conclusions (highest-impact locations)
2. Count em dashes, semicolons, colon lists (stop at first paragraph if ≤ limits)
3. Delete any opening throat-clearer phrases
4. Read the Discussion section aloud for rhythm
5. Spot-check paragraph length variation in introduction and body

---

## Key Definitions

**Flagged term**: A default word that often masks less-precise alternatives. Using it doesn't mean changing it — it means asking "Is this the most specific word here?"

**Throat-clearing**: Meta-commentary that describes the writing instead of doing it. Adds no information. Cut without replacement.

**Structural tic**: A repetitive pattern (e.g., all sections have 3 subsections, all paragraphs ~150 words) that creates a template feel.

**Burstiness**: Variation in sentence length. Natural prose has high burstiness (short + long + medium sentences). Template prose has low burstiness (all sentences 20-25 words).

---

## Detailed Guidance

Read each reference file as needed for your current task:

- **[high-frequency-terms.md](./references/high-frequency-terms.md)** — Complete table of 25+ flagged terms with why they're overused and better alternatives. Includes exception rule for discipline-standard terminology.

- **[punctuation-patterns.md](./references/punctuation-patterns.md)** — Em dash, semicolon, and colon-list rules. Specific limits (≤3 em dashes per paper, ≤2 per 1000 words semicolons) and fixes.

- **[throat-clearing.md](./references/throat-clearing.md)** — 12+ opening phrases to delete and meta-commentary patterns to eliminate. Includes roadmap sentence exception.

- **[structure-patterns.md](./references/structure-patterns.md)** — Five structural tics: rule-of-three compulsion, uniform paragraphs, synonym cycling, binary contrasts, mirror structure. Includes why each weakens prose and how to fix.

- **[burstiness.md](./references/burstiness.md)** — Sentence length variation detection and targets by section type (Abstract: moderate, Introduction: high, Methods: low acceptable, Discussion: highest).

---

## Gotchas

- **"This looks fine to me" ≠ Ready to submit.** Read your draft aloud. Rhythm problems are audio problems — you'll hear them before you see them. Template prose sounds metronomic.

- **Flagged terms are not banned.** They're flags for re-examination. If "robust" is the discipline-standard term for your field (statistics, systems research), keep it. The exception rule applies.

- **Colon-list syndrome spreads quietly.** If one section has "Here are three points:" + list, and the next section mirrors it, you've created a template structure. Integrate at least one list into prose to break the pattern.

- **Semicolons chain more easily than you think.** Every time you write "; " to connect two clauses, ask: "Should this be a period instead?" Often yes.

- **Short, punchy sentences can also monotonize.** If every sentence is ≤10 words, you've flipped the burstiness problem. Natural writing needs long sentences too.

- **Paragraph length uniformity is harder to spot than you'd think.** Open your draft to a random page and measure paragraph length in sentences. If they're all 5-7 sentences, mark that section for restructuring.

---

## Quality Scoring (Internal, Not Reported)

For self-monitoring, track violations by category:
- **0 violations**: Clean
- **1–3 violations**: Minor — fix in next review pass
- **4+ violations**: Pattern issue — review your approach to that section

Do NOT report scores to the user. Just fix issues silently during drafting or final review.

---

## Remember

**Good writing is:** Precise, varied, clear, disciplined about structure.  
**Template writing is:** Default terms, monotonous rhythm, meta-commentary, structural repetition.

This checklist helps you move from the second toward the first — regardless of whether you or an AI wrote the draft.
