# Revision Plan — NSF SaTC 2.0 RES: "Toward Secure and Robust Generalist Robotic Models"

**Revision Coach synthesis of four completed reviews**
**Date:** 2026-09-08
**Inputs:** `artifacts/academic_review.md`, `artifacts/auditor_feasibility.md`, `artifacts/integrity_review.md`, `artifacts/novelty_assessment.md`
**Fix sites verified in:** `main_v2.tex`, `01_v2.tex`, `02_v2.tex`, `sections/budgetjustification_v2.tex`, `sections/0_project_summary_v2.tex`
**Constraint:** Preserve validated research design (aims, T0–T3 structure, ABBP/TTDA/TACD/AGAT, VLA-SecBench). No .tex files edited by this plan.

---

## 1. Executive Revision Summary

The four reviews converge on a consistent conclusion: the **underlying research design is sound**, but the submitted document carries a small set of **visible, high-impact defects** (a literal Co-PI placeholder, a budget placeholder, a duplicate section label, count inconsistencies, and un-hedged novelty language) plus a few **substantive gaps** (Co-PI robotics credentials, real budget numbers, preliminary defense evidence, scope-vs-staffing) that require PI decisions and cannot be fabricated.

Every fix below is classified as either:

- **(A) EDITORIAL** — Writer can apply now without changing research design (consistency, hedging, uncommenting, label fixes, repositioning, reconciliation).
- **(B) SUBSTANTIVE** — requires PI decision or new research; listed as PI action items and **not to be fabricated**.

**Headline:** 11 (A)-type editorial fixes are ready to apply now (2 P0, 6 P1, 3 P2 leading + 1 P2 cleanup). 4 (B)-type items require PI input, of which **2 are P0 submission blockers** (Co-PI identity/credentials; budget placeholder + total recomputation). The proposal cannot be submitted until the two P0 (B) items are resolved by the PI, but all editorial work can proceed in parallel.

---

## 2. Issue Aggregation (deduplicated, cross-referenced)

Reviewer key: **AC** = Academic, **AU** = Auditor, **IN** = Integrity, **NO** = Novelty.

| ID | Issue (deduplicated) | Flagged by | Severity | Class |
|----|----------------------|-----------|----------|-------|
| R1 | Duplicate `\newsection{F}` label | IN (C-1) | P0 | A |
| R2 | `[Co-PI: TBD]` placeholder vs. named Co-PI (Thiruvathukal) whose stated expertise is distributed computing, not robotics | AC (Atk2), AU (C1/§6.2), IN (C-2), NO (§10) | P0 | **B** |
| R3 | `$[PLACEHOLDER]` in budget (Yr 3–4 cloud/API) while totals stated as final | AC (Atk8), AU (C2/§6.4) | P0 | **B** |
| R4 | "six robots, six embodiments" vs. 7 embodiment codes (F,G,S,H,U,M,X) in table | AU (H1/§7), IN (M-1) | P1 | A |
| R5 | Dataset count ambiguity "15 (=14+OXE)" | IN (C-3), AU (§3) | P1 | A |
| R6 | Novelty overclaim: "first comprehensive," "uncharted," "pioneering" contradicted by own cited 2025–26 work | NO (primary), AC (Atk7), AU (§2) | P1 | A |
| R7 | Commented-out real-time-inference-vs-cloud reconciliation leaves feasibility contradiction | AU (H3/§10) | P1 | A |
| R8 | No explicit "Relationship to Concurrent Work" differentiation (BadVLA/AdvVLA/AttackVLA/DRIFT/Trajectory-Redirection/Structure-Aware-FT) | NO (§14), AC (§6) | P1 | A |
| R9 | Orphaned M0 "NSF ACCESS allocation" milestone with no narrative/budget/fallback | AU (H2/§6.4) | P1 | A (+PI confirm) |
| R10 | Weak preliminary evaluation: no TACD/AGAT defense results, no BadVLA/AdvVLA comparison | AC (Atk3/§4), AU (§5), NO | P1 | **B** |
| R11 | Scope exceeds feasibility (6 embodiments × 15 datasets × 6 models for ~1.3 FTE) | AC (Atk6/§7), AU (§6.1), NO | P1 | **B** |
| R12 | Go/no-go numeric acceptance thresholds exist only in internal planner, not visible text | AU (M1) | P2 | A (+PI confirm) |
| R13 | Threat model / "trust" definition circular; threat actors not prioritized | AC (Atk10), AU (§4) | P2 | A |
| R14 | "gated appropriately" vs. "open-source under permissive licenses" dual-use tension | AU (M3/§8) | P2 | A |
| R15 | T3-2 human-in-the-loop protocol underspecified (raters, N, agreement metric) | AU (M2/§5), AC (§4) | P2 | A |
| R16 | Leftover `%TODO` / `% VERIFY` editorial comments | AU (L1) | P2 | A |

---

## 3. Issue-to-Section Mapping

```yaml
R1:  Section: Document structure       File: main_v2.tex:57
R2:  Section: Intellectual Merit / Budget  File: 01_v2.tex:214 ; sections/budgetjustification_v2.tex:15
R3:  Section: Budget Justification     File: sections/budgetjustification_v2.tex:59
R4:  Section: Overview / Research Plan  File: 01_v2.tex:151 ; 02_v2.tex:39
R5:  Section: Research Plan (T0 data)   File: 02_v2.tex:39 ; 01_v2.tex:151
R6:  Section: Overview / Intellectual Merit  File: 01_v2.tex:105, 112, 212
R7:  Section: Research Plan (prelim/eval)  File: 02_v2.tex:252-260 (commented block)
R8:  Section: Research Plan (after threat model)  File: 02_v2.tex (new paragraph)
R9:  Section: Work Plan / T0-T1-1        File: 02_v2.tex:740 (caption) → body text
R10: Section: Preliminary Studies / Eval Plan  File: 02_v2.tex (new results, PI)
R11: Section: Staged Scope / Feasibility  File: 01_v2.tex:214 ; 02_v2.tex staged-scope
R12: Section: T1 / T1-4                   File: 02_v2.tex
R13: Section: Threat Model               File: 01_v2.tex / 02_v2.tex threat-model
R14: Section: Intellectual Merit / DMP    File: 01_v2.tex:217 ; sections/datamanagement_v2.tex:20
R15: Section: T3-2 Interpretability       File: 02_v2.tex:654
R16: Section: multiple                    File: 01_v2.tex:184,192 ; sections/0_project_summary_v2.tex:87
```

---

## 4. Prescribed Fixes (ordered: P0 (A) first, then P0 (B), then P1 (A), P1 (B), P2)

> Not yet applied — this plan does not edit .tex sources. Each item gives the exact site, the concrete change, and its (A)/(B) classification.

### P0 — Blockers

**R1 — (A) EDITORIAL — Duplicate section label**
- File/loc: `main_v2.tex:57`
- Change: `\newpage\newsection{F}` (the second one, before `\input{sections/synergy}`) → `\newpage\newsection{G}`. Line 54 (Project Summary) stays `F`.
- Fix type: Consistency (structural).

**R2 — (B) SUBSTANTIVE — Co-PI identity and robotics credentials** *(PI action)*
- File/loc: `01_v2.tex:214` (`a Co-PI [Co-PI: TBD] contributing robot-learning and real-robot experimentation expertise`) vs. `sections/budgetjustification_v2.tex:15` (George K. Thiruvathukal — "concurrent, parallel, and distributed modeling and analysis").
- Required PI decision (do NOT fabricate): (a) confirm whether Thiruvathukal is the Co-PI and, if so, **rewrite the Intellectual Merit sentence to match his actual contribution** (e.g., scaled/distributed training + benchmark infrastructure) rather than asserting real-robot experimentation; OR (b) add/confirm a collaborator with genuine robot-learning credentials and update both the narrative and budget consistently.
- Editorial sub-fix (blocked until PI decides): once resolved, remove the literal `[Co-PI: TBD]` bracket so no placeholder remains, and ensure `01_v2.tex` and `budgetjustification_v2.tex` describe the same person doing the same work.
- Fix type: Consistency + Evidence (feasibility credibility).

**R3 — (B) SUBSTANTIVE — Budget placeholder + total recomputation** *(PI action)*
- File/loc: `sections/budgetjustification_v2.tex:59` (`\$[PLACEHOLDER]`, Yr 3–4 cloud/API; existing comment suggests ~$3–5K/yr).
- Required PI decision (do NOT fabricate): insert the actual cloud/API cost, add it to Other Direct Costs, **recompute indirect costs and the $408,435 / $146,736 / $555,171 totals**, and delete the placeholder. Totals currently presented as final are not reconciled while this line is open.
- Fix type: Evidence (budget integrity).

### P1 — Major

**R4 — (A) EDITORIAL — Embodiment count consistency**
- File/loc: `01_v2.tex:151`, `02_v2.tex:39` ("six robots, six embodiments").
- Change: recount against `\autoref{tab:multi_dataset}` (7 codes: F,G,S,H,U,M,X). Align prose to the table — either state **"seven robot types / embodiments"**, or if six is intended, write **"six primary embodiments (Franka, Google Robot, Spot, Stretch, UR5, Xarm7), plus human/other demonstration data"** so prose and table agree on one number.
- Fix type: Consistency. (Which count is authoritative is a minor Writer judgment against the table — no new research.)

**R5 — (A) EDITORIAL — Dataset count clarity**
- File/loc: `02_v2.tex:39` (and `01_v2.tex:151`).
- Change: replace ambiguous "15 (=14+OXE)" with explicit phrasing, e.g. *"a mixture of 15 dataset sources: 14 explicitly named robotics datasets (Table 1) plus the Open X-Embodiment (OXE) repository, which itself aggregates additional robotic datasets."* Remove the arithmetic ambiguity.
- Fix type: Clarification.

**R6 — (A) EDITORIAL — De-escalate novelty overclaims**
- File/loc: `01_v2.tex:105` ("uncharted threat landscape"), `01_v2.tex:112` ("the first comprehensive framework unifying..."), `01_v2.tex:212` ("pioneering contributions... the first comprehensive taxonomy and framework").
- Change: soften "first comprehensive / uncharted / previously unexplored / pioneering" to claims the citation record supports — **systematic cross-embodiment coverage, physical-consequence grounding, and integration/rigor at scale**. Note: `sections/0_project_summary_v2.tex:91` is **already** softened ("developing a taxonomy and framework"); bring `01_v2.tex` into line with it so the framing sections match the (already-hedged) Research Plan.
- Fix type: Reframing (no scope change).

**R7 — (A) EDITORIAL — Reinstate real-time-vs-cloud reconciliation**
- File/loc: `02_v2.tex:252-260` (the `%`-commented "Adoption and Constraints" block).
- Change: uncomment and lightly edit into 2–4 sentences in T1-4/Evaluation stating that (i) TACD inference overhead must stay within the robot's 3–10 Hz control-loop budget, and (ii) RT-2/OpenVLA-scale models queried via cloud API are treated under the **black-box** threat model for exactly this reason — tying the architecture-scale split to the already-present threat-model split.
- Fix type: Consistency (resolves a live feasibility contradiction).

**R8 — (A) EDITORIAL — Add "Relationship to Concurrent Work" differentiation**
- File/loc: `02_v2.tex` (new paragraph/table after the threat-model / before or within the Research Plan).
- Change: add an explicit comparison of ABBP/TTDA/TACD/AGAT/VLA-SecBench against **BadVLA, AdvVLA, AttackVLA, DRIFT, Trajectory-Level Redirection, Structure-Aware Robust Fine-Tuning, Randomized Smoothing** — stating what is shared and what differs (kinematic/Jacobian constraint, physical-consequence metrics, cross-embodiment scale, single multi-task TACD). Converts implicit citations into a load-bearing positioning argument. **No new research** — repositioning of existing citations only.
- Fix type: Reframing / positioning.

**R9 — (A) EDITORIAL (+PI confirm) — Narrate the M0/ACCESS compute plan**
- File/loc: `02_v2.tex:740` (milestone caption) → add body text in T0/T1-1 or Work Plan.
- Change: add 2–3 sentences stating the NSF ACCESS application plan, approximate allocation, timing, and an explicit **fallback** (e.g., encoder-only white-box scope + LoRA if the allocation is denied/delayed). The narrative and fallback are editorial; the **specific allocation size/timing should be confirmed by the PI** before final compile.
- Fix type: Evidence Enhancement (feasibility).

**R10 — (B) SUBSTANTIVE — Strengthen preliminary evaluation** *(PI / new research)*
- File/loc: `02_v2.tex` Preliminary Studies / Evaluation Plan.
- Required (do NOT fabricate): add real preliminary **defense** results (TACD detection rate + false-positive rate; AGAT clean-vs-robust TSR) and at least one **direct comparison to BadVLA/AdvVLA** on the existing toy tasks, with ≥10 runs and significance testing. If new results cannot be produced pre-submission, reposition affected defense claims as "to be validated" consistent with the existing hedged framing.
- Fix type: Evidence (cannot be editorial-only).

**R11 — (B) SUBSTANTIVE — Scope vs. staffing** *(PI decision)*
- File/loc: `01_v2.tex:214` (two-track parallelism claim) + `02_v2.tex` staged-scope paragraph.
- Required (do NOT fabricate): either (a) narrow the committed MVP to what one graduate student can execute per track-year (e.g., 2 embodiments / 3 models, as the reviews suggest), or (b) document that the Co-PI's lab/students contribute additional robotics-track labor. This is coupled to R2. **Preserve the validated aims**; adjust only committed scope, not the research design.
- Fix type: Reframing / scope reconciliation (PI-gated).

### P2 — Minor

**R12 — (A) EDITORIAL (+PI confirm) — Surface go/no-go thresholds**
- File/loc: `02_v2.tex` T1 / T1-4.
- Change: state at least one quantitative acceptance threshold per major contribution (ABBP-vs-PGD normalized-budget improvement; TACD false-positive ceiling; AGAT max clean-TSR drop) directly in the visible text. Numbers should be confirmed by the PI from the internal planner artifact.
- Fix type: Clarification (falsifiability).

**R13 — (A) EDITORIAL — Tighten threat model / trust definition**
- File/loc: `01_v2.tex` / `02_v2.tex` threat-model text.
- Change: replace the circular "trust = safe, intended actions" with an operational statement, and name/prioritize the threat actors already implied (insider white-box on open encoders; external black-box via API; supply-chain poisoning). No new methodology — clarification of existing scope.
- Fix type: Clarification.

**R14 — (A) EDITORIAL — Reconcile dual-use vs. open-source language**
- File/loc: `01_v2.tex:217` ("gated appropriately") vs. `sections/datamanagement_v2.tex:20` ("open source under permissive licenses").
- Change: state a concrete mechanism reconciling both — e.g., staged/DUA-gated release of offensive attack code with openly released defenses, benchmarks, and datasets.
- Fix type: Consistency.

**R15 — (A) EDITORIAL — Specify T3-2 human-in-the-loop protocol**
- File/loc: `02_v2.tex:654`.
- Change: add one sentence giving number of evaluators, evaluation-task sample size, and an inter-rater agreement metric (e.g., Cohen's κ), to match the rigor of the T1/T2 plan.
- Fix type: Evidence Enhancement.

**R16 — (A) EDITORIAL — Remove leftover editorial comments**
- File/loc: `01_v2.tex:184,192` (`%TODO: add more deliverables`); `sections/0_project_summary_v2.tex:87` (`% VERIFY first keyword against NSF 25-515 controlled list`).
- Change: resolve/remove the TODO and verify the keyword against the NSF 25-515 controlled list, then delete the comments. (Invisible in PDF but indicate an unfinished pass.)
- Fix type: Cleanup.

---

## 5. Section-Level Revisions (summary by section)

- **Document structure (`main_v2.tex`):** R1 relabel second `F`→`G`.
- **Overview / Intellectual Merit (`01_v2.tex`):** R6 hedge novelty; R2 Co-PI sentence (PI-gated); R4 embodiment count; R13 threat/trust wording; R14 dual-use wording; R16 remove TODOs.
- **Research Plan (`02_v2.tex`):** R5 dataset count; R7 reinstate real-time/cloud paragraph; R8 concurrent-work differentiation; R9 ACCESS narrative + fallback; R10 defense/BadVLA evidence (PI); R11 staged-scope (PI); R12 go/no-go thresholds; R15 T3-2 protocol.
- **Budget (`sections/budgetjustification_v2.tex`):** R3 fill placeholder + recompute (PI); R2 Co-PI role alignment (PI).
- **Project Summary (`sections/0_project_summary_v2.tex`):** R16 verify keyword; already-softened language is the target register for R6.
- **Data Management (`sections/datamanagement_v2.tex`):** R14 reconcile with Intellectual Merit.

---

## 6. Consistency Reconciliation

- **Co-PI (R2):** the single most-cited defect — flagged by **all four** reviewers. `01_v2.tex:214` and `budgetjustification_v2.tex:15` must describe the same person and the same work. Resolution is PI-gated; until then the proposal is internally contradictory on team composition.
- **Counts (R4/R5):** prose ("six/15=14+OXE") must match `tab:multi_dataset` (7 codes; 14 named datasets + OXE). Pick one authoritative count and propagate to both `01_v2.tex` and `02_v2.tex`.
- **Novelty framing (R6):** `01_v2.tex` framing sections must be brought down to the register already used in the (hedged) Research Plan and Project Summary — removes the self-contradiction the Novelty reviewer names as the top risk.
- **Real-time/threat-model (R7):** reinstating the commented paragraph closes the gap between the Background 3–10 Hz constraint and the black-box treatment of cloud-hosted models.
- **Budget totals (R3):** totals cannot be asserted "final" while a placeholder line is open — arithmetic must be reconciled.
- **Dual-use (R14):** "gated" vs. "permissive open-source" must be reconciled across `01_v2.tex` and the DMP.

---

## 7. Revision Traceability Map

```yaml
- Original Issue: Duplicate section label
  Fix Applied: main_v2.tex:57 F -> G
  Location: Document structure
  Expected Improvement: Structural integrity; correct cross-refs/index

- Original Issue: Co-PI placeholder + robotics-credential mismatch
  Fix Applied: PI confirms Co-PI + rewrite 01_v2:214 to match budget:15 (or add roboticist)
  Location: Intellectual Merit + Budget
  Expected Improvement: Removes top feasibility blocker; team credibility

- Original Issue: Budget $[PLACEHOLDER] + unreconciled totals
  Fix Applied: PI inserts real cost, recomputes indirect + totals, removes placeholder
  Location: Budget Justification
  Expected Improvement: Budget integrity; submission-readiness

- Original Issue: 6 vs 7 embodiments
  Fix Applied: Align prose to table (single count)
  Location: Overview / Research Plan
  Expected Improvement: Factual precision; reviewer confidence

- Original Issue: "15 (=14+OXE)" ambiguity
  Fix Applied: Explicit dataset-source phrasing
  Location: Research Plan T0
  Expected Improvement: Clarity; removes checkable ambiguity

- Original Issue: Novelty overclaim
  Fix Applied: Hedge 01_v2:105/112/212 to scale/rigor framing
  Location: Overview / Intellectual Merit
  Expected Improvement: Removes self-contradiction vs own citations; perceived novelty honesty

- Original Issue: Commented real-time/cloud reconciliation
  Fix Applied: Reinstate edited paragraph tying cloud models to black-box model
  Location: Research Plan / Eval
  Expected Improvement: Resolves feasibility contradiction

- Original Issue: No concurrent-work differentiation
  Fix Applied: Add explicit comparison paragraph/table
  Location: Research Plan
  Expected Improvement: Load-bearing novelty positioning; pre-empts Reviewer A/B

- Original Issue: Orphaned M0/ACCESS milestone
  Fix Applied: Narrative + fallback in body text (allocation confirmed by PI)
  Location: Work Plan / T0-T1-1
  Expected Improvement: Perceived feasibility of compute plan

- Original Issue: Weak preliminary evaluation
  Fix Applied: PI adds defense + BadVLA/AdvVLA results, or repositions as to-be-validated
  Location: Preliminary Studies / Eval
  Expected Improvement: Reduces execution risk; evaluation strength

- Original Issue: Scope vs staffing
  Fix Applied: PI narrows committed MVP or documents added robotics labor
  Location: Staged Scope
  Expected Improvement: Perceived feasibility

- Original Issue: Hidden go/no-go thresholds
  Fix Applied: Surface numeric thresholds (PI-confirmed) into text
  Location: T1 / T1-4
  Expected Improvement: Falsifiability; methodological rigor

- Original Issue: Circular trust definition
  Fix Applied: Operationalize trust + name threat actors
  Location: Threat Model
  Expected Improvement: Threat-model clarity

- Original Issue: Dual-use vs open-source tension
  Fix Applied: Concrete staged/DUA release mechanism
  Location: Intellectual Merit + DMP
  Expected Improvement: Responsible-disclosure credibility

- Original Issue: T3-2 protocol underspecified
  Fix Applied: Add raters/N/agreement metric
  Location: T3-2
  Expected Improvement: Evaluation consistency

- Original Issue: Leftover TODO/VERIFY comments
  Fix Applied: Resolve + remove
  Location: 01_v2 / project summary
  Expected Improvement: Signals completed review pass
```

---

## 8. Revision Impact Assessment

```yaml
Revision Impact:
  Clarity Improvement: High — R4/R5/R6/R7/R13 remove the most reviewer-visible ambiguities and self-contradictions.
  Feasibility Improvement: High but PI-gated — R2, R3, R9, R10, R11 drive the Feasibility/Reviewer-Readiness scores (Auditor 5/10, Reviewer-Readiness 4/10); the two P0 (B) items are the binding constraints.
  Reviewer Score Improvement: Moderate — editorial fixes lift Integrity to PASS and remove the Novelty self-contradiction; Novelty (4/10) improves only modestly without R8 + (ideally) R10, since core mechanisms remain incremental by design.
  Alignment Improvement: Moderate — R14 (dual-use) and R13 (threat model) tighten SaTC responsible-disclosure and trustworthiness alignment.
```

---

## 9. Remaining Weaknesses (after editorial pass, if (B) items unresolved)

- **Core novelty remains incremental** by design (ABBP/TTDA/TACD/AGAT are constrained variants of known families). Editorial reframing (R6/R8) mitigates but does not eliminate this; only R10-type evidence would.
- **Feasibility stays capped** until R2 (Co-PI credentials), R3 (budget), and R11 (scope) are resolved by the PI.
- **Preliminary defense evidence (R10)** is absent; without it, defense contributions remain "to be validated."

These are **outside Revision Coach authority** (they need PI decisions / new research) and must not be fabricated.

---

## 10. Final Readiness Assessment

**Status: Requires Another Revision Cycle** — gated on PI inputs.

- All **11 (A)-type editorial fixes can be applied now** by the Writer and will move Integrity to PASS and materially improve clarity, consistency, and positioning.
- **2 P0 (B) blockers (R2 Co-PI, R3 budget)** must be resolved by the PI before the proposal is submission-ready; **2 P1 (B) items (R10, R11)** should be resolved for competitiveness.
- After the Writer applies the (A) fixes and the PI supplies the (B) inputs, re-validate:

```text
RE-ENTER REVIEW LOOP
```

→ Integrity Reviewer (re-check R1/R2/R4/R5/R14) → Academic Reviewer (re-score novelty/feasibility after R6/R8/R9/R10/R11) → Revision Coach convergence check.

---

### Routing
- **To Writer:** apply all (A) items (R1, R4, R5, R6, R7, R8, R9, R12, R13, R14, R15, R16). Do not touch aims, T0–T3, or method definitions.
- **To PI:** resolve (B) items (R2, R3, R10, R11) — do not fabricate; provide real Co-PI/credentials, real budget numbers, preliminary defense evidence, and a staffing/scope decision.
- **To Orchestrator:** hold submission until R2 and R3 are closed; then trigger re-review loop.
