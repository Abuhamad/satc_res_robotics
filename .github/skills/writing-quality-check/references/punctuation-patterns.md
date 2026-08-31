# Punctuation Pattern Control

Three specific punctuation patterns that weaken academic prose. Apply these limits consistently.

---

## Em Dash (—)

### Limit
- **≤ 3 per paper total** (recommended 0–1)

### Why It's Flagged
AI text overuses em dashes for parenthetical asides. Academic writing typically uses commas, parentheses, or separate sentences instead.

### How to Fix
Replace with:
- **Commas** (for brief asides): "The protocol, which uses gossip, reduces latency."
- **Parentheses** (for slightly longer asides): "The protocol (see Section 3.2) reduces latency."
- **New sentence** (for stronger emphasis): "The protocol reduces latency. This is achieved through gossip-based updates."

### Exception
Direct quotes from sources retain their original punctuation.

---

## Semicolons

### Limit
- **≤ 2 per 1000 words**

### Why It's Flagged
AI text chains independent clauses with semicolons where a period would be clearer. Semicolons signal a close relationship between clauses, but overuse creates a chained, breathless effect.

### When to Use
Reserve semicolons for closely related parallel structures:
- "The protocol achieves O(n log n) complexity; the baseline requires O(n²)."
- "Results show 40% latency reduction; throughput remains constant."

### How to Fix
Replace with a period. New sentences are often clearer:
- ❌ "The protocol uses gossip; this reduces message overhead."
- ✅ "The protocol uses gossip. This reduces message overhead."

---

## Colon-List Sequences

### Rule
Avoid 2+ consecutive paragraphs that each open with a colon followed by a list.

### Why It's Flagged
Creates a monotonous enumerate-everything pattern that signals templated writing.

### Example of the Problem

```
## Approach
We employ three strategies:
- Strategy 1
- Strategy 2
- Strategy 3

## Evaluation
We measure three metrics:
- Metric 1
- Metric 2
- Metric 3
```

### How to Fix
Integrate at least one list into prose:

```
## Approach
We employ three strategies: strategy 1 accelerates local decisions, strategy 2 reduces global synchronization, and strategy 3 leverages network locality. 

## Evaluation
We measure three key metrics:
- Metric 1
- Metric 2
- Metric 3
```

---

## How to Check

1. **Em dashes**: Use Find to count "—" (em dash, not hyphen). If >3, trim.
2. **Semicolons**: Use Find to count ";". If >2 per 1000 words, replace with periods.
3. **Colon lists**: Scan for paragraphs starting with "Here are", "We use", "This includes", followed by bullet lists. If 2+ appear consecutively, integrate one into prose.

**Remember:** These are guidelines, not laws. But they flag patterns worth examining.
