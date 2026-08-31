# Burstiness: Sentence Length Variation

"Burstiness" is the technical term for variation in sentence length. Natural prose has **high burstiness** (short + long + medium sentences). Template prose has **low burstiness** (all sentences 20–25 words).

---

## Quick Detection

Count the words in 5 consecutive sentences in a paragraph. If they're all within a narrow range (e.g., all 18–24 words), flag for revision.

**Good example:**
- Sentence 1: 8 words. (Short)
- Sentence 2: 34 words. (Long)
- Sentence 3: 15 words. (Medium)
- Sentence 4: 42 words. (Long)
- Sentence 5: 6 words. (Short)

**Template example:**
- Sentence 1: 22 words.
- Sentence 2: 19 words.
- Sentence 3: 21 words.
- Sentence 4: 18 words.
- Sentence 5: 23 words.

---

## How to Fix

### If Sentences Are All Short (≤10 words):
Combine two related sentences into one:
- ❌ "The protocol is fast. It uses gossip. This reduces overhead."
- ✅ "The protocol is fast because it uses gossip-based communication, which reduces overhead."

### If Sentences Are All Long (≥30 words):
Break one sentence into two:
- ❌ "The protocol, which uses gossip-based communication to reduce message overhead while maintaining Byzantine fault tolerance under realistic network assumptions, achieves O(n log n) complexity."
- ✅ "The protocol uses gossip-based communication. This reduces message overhead while maintaining Byzantine fault tolerance, achieving O(n log n) complexity."

### If Sentences Are Uniform (20–25 words):
Insert one very short sentence (≤8 words) per paragraph for rhythm:
- "Results confirmed our hypothesis." or "This matters." or "Not all systems scale."

---

## Burstiness Targets by Section

### Abstract
**Target:** Moderate variation  
**Why:** Abstracts are factual and steady-paced. Readers expect a measured tone.

### Introduction
**Target:** High variation  
**Why:** Hook with short sentences, build excitement. Then develop complex ideas in longer sentences. Rhythm draws readers in.

### Literature Review
**Target:** Moderate variation  
**Why:** Analytical sections need steady pace. Occasional short synthesis sentences (e.g., "This gap is our opportunity.") for emphasis.

### Methods
**Target:** Low variation acceptable  
**Why:** Procedural sections naturally have uniform sentence length. This is OK. But try to insert one short summary sentence per subsection anyway.

### Results
**Target:** Moderate variation  
**Why:** Short sentences for key findings ("Latency improved 40%."). Longer sentences for detailed descriptions.

### Discussion
**Target:** Highest variation  
**Why:** You're interpreting, not just reporting. Use short sentences for emphasis. Long sentences for nuanced interpretation. Very short sentences for conclusions.

---

## How to Check

1. **Select a paragraph** (any section).
2. **Count words in each sentence.**
3. **Check the range:** Is the spread >10 words (e.g., shortest is 8, longest is 35)? Good.
4. **If the range is <10 words,** the paragraph likely has low burstiness. Revise.

---

## Remember

**Burstiness is about rhythm.** Read your paragraph aloud. If it sounds metronomic (same pace throughout), it has low burstiness. Natural prose has peaks and valleys — short bursts of emphasis, longer stretches of development.

This is one of the hardest problems to spot visually but easiest to hear. **Read aloud.**
