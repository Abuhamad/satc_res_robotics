---
name: proposal-review-boost
description: 'Interactive prompt-refinement workflow for requests to review, critique, audit, or check the NSF/DARPA/NIH proposal in this repo. Interrogates scope (whole proposal vs. section), which reviewer lens to apply (Academic Reviewer, Auditor, Integrity Reviewer, Novelty-Detector), sponsor/review criteria, depth, and desired output before any review agent is dispatched. Use when the user gives a multi-step or ambiguous review/feedback request (e.g. "review my proposal", "check this for problems", "is this ready to submit") instead of a single clear one-step instruction. Never performs the review itself; only produces a refined task brief for the Orchestrator to execute.'
---

# Proposal Review Prompt Booster

You help the user turn a vague "review my proposal" style request into a precise task brief the Orchestrator can dispatch to the right subagent(s) — **before** any review work starts. DO NOT review, critique, or edit proposal content yourself in this skill. DO NOT invoke subagents yourself; your only output is a refined brief.

## When to Use This Skill

- The user asks to review, check, critique, audit, grade, or give feedback on the proposal (or a section) without specifying scope, lens, or output format.
- The request is multi-step (e.g. implies both critique and revision, or spans multiple sections/agents) rather than a single unambiguous action.
- Skip this skill if the user's request is already fully specified (exact section, exact reviewer, exact output format) — just proceed directly in that case.

## Interrogation Checklist

Ask only the questions not already answered by the user's original message. Batch them into one round using `vscode_askQuestions` where possible; do not ask one at a time.

1. **Scope** — Whole proposal (`main_v2.tex`) or specific section(s)/file(s) (e.g. [sections/impact.tex](sections/impact.tex), [01_v2.tex](01_v2.tex))?
2. **Reviewer lens** — Which of the system's review agents should apply:
   - Academic Reviewer (peer-review simulation: significance, clarity, positioning)
   - Auditor (feasibility, methodological/assumption weaknesses, risk)
   - Integrity Reviewer (cross-section consistency, logic, citation/evidence check)
   - Novelty-Detector (originality vs. prior work)
   - Or "all" for a full Stage 6+ review pass per the Orchestrator pipeline
3. **Sponsor/criteria** — NSF, DARPA, NIH, or other — review criteria and tone differ (check [artifacts/context_report.md](artifacts/context_report.md) if unsure).
4. **Depth** — Quick pass/spot-check vs. thorough line-by-line critique.
5. **Output** — Structured findings report only (e.g. append to [artifacts/academic_review.md](artifacts/academic_review.md)), or findings + a prioritized revision plan (hands off to Revision Coach)?
6. **Convergence** — One-shot review, or should this feed the Orchestrator's Revision Mode loop until thresholds are met?

## Process

1. Read the user's initial request and the relevant artifacts/sections needed to understand current state (use read-only tools: `read_file`, `grep_search`, `list_dir` — do not edit anything).
2. Identify which checklist items are already answered; ask only the remaining ones in a single batched question set.
3. Draft a refined task brief in markdown with these fields: **Scope**, **Reviewer(s) to dispatch**, **Sponsor/criteria**, **Depth**, **Expected output artifact(s)**, **Follow-up loop (yes/no)**.
4. Present the brief to the user and ask for confirmation or changes. Iterate until approved.
5. Once approved, copy the final brief to the clipboard and hand it back so the user (or the Orchestrator) can dispatch it — do not execute the review yourself.

```clojure
(require '["vscode" :as vscode])
(vscode/env.clipboard.writeText "your-markdown-brief-here")
```

## Gotchas

- **Never** skip straight to calling Academic Reviewer/Auditor/etc. subagents from within this skill — that is the Orchestrator's job, not this booster's.
- A request mentioning only one section and one clear reviewer (e.g. "have the Auditor check [sections/impact.tex](sections/impact.tex) for feasibility gaps") is already a one-step request — proceed directly without interrogation.
- If the user's answers reveal they actually want a revision, not just a review, note that in the brief's "Follow-up loop" field rather than silently expanding scope.
