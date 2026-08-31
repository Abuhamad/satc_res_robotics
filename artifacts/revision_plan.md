# Revision Plan — NSF SaTC 2.0 RES Proposal (Cycle 2)

**Proposal:** "SaTC 2.0: RES: Toward Secure and Robust Generalist Robotic Models" (PI: Abuhamad, Loyola University Chicago)
**Date:** 2026-08-31
**Inputs used:** `artifacts/academic_review.md` (panel: GOOD 3/5, Borderline), `artifacts/integrity_review.md` (PASS w/ pre-submission actions), `artifacts/context_report.md`, `artifacts/researcher_report.md`, and current `01_v2.tex` / `02_v2.tex` / `sections/*_v2.tex` for grounding.
**Note:** `artifacts/auditor_report.md` was requested but does **not** exist in `artifacts/`. Auditor-type findings were recovered from the session record and folded into Category B where relevant, but no auditor file was read.

**Scope of this document:** planning only. **No `.tex` or `.bib` files were edited.** Every dollar figure and reference remains the PI's to compute/verify; nothing is fabricated here.

---

## 1. Executive Revision Summary

The panel rates the proposal **GOOD (3/5), Borderline / not competitive as-is**. The integrity gate is **PASS** but lists concrete pre-submission blockers. The gap between the two is instructive: the package is *structurally sound and internally consistent*, but its *research narrative* is judged incremental. Repairs therefore split cleanly into three tracks:

- **(A) Mechanical / Compliance** — text-level fixes that are safe to apply now and do not touch the science. These close every integrity blocker except numbers/refs.
- **(B) Research-substance** — the four issues that actually move the score (attack novelty, defense evidence, evaluation rigor, scope). These require **PI decisions and/or real data** and **must not be fabricated**. This plan proposes *options and framing*, not invented results.
- **(C) Verification** — references, the Project-Summary controlled keyword token, and the 4-year budget recomputation. Facts the PI must confirm against primary sources.

**Headline judgment:** the compliance track can be finished quickly and is auto-applyable; the score ceiling is set by Category B, which cannot be closed by editing alone. Realistically, lifting GOOD → VERY GOOD requires at least one genuine VLA-specific attack result and a preliminary anomaly-detector evaluation (detection/false-positive numbers) — both PI-executed.

---

## 2. Issue Aggregation (by severity)

**Critical**
- C1. Attack methods read as ports of VLM/LLM attacks (PGD/FGSM/C&W, prompt injection, token deletion); no VLA-specific algorithmic novelty. *(academic §1.2 W1, §5 W1)*
- C2. Action-space anomaly-detection defense has **zero preliminary evidence** (no detection rate, no false-positive rate, no baselines). *(academic §1.2 W2, §5 W2)*
- C3. Evaluation is narrow: 3 sim + 3 real basic manipulation tasks, no baseline defenses, no transferability data, arbitrary 30% deviation threshold, single-seed/5-run stats. *(academic §1.2 W3, §3.4, §5 W3)*

**Major**
- M1. Scope exceeds single-PI/4-year feasibility (T0–T3; six robots/six embodiments/15 datasets; 5+ model families; real-robot logistics). *(academic §1.2 W4, §3.6 "Poor", §5 W4)*
- M2. Threat model and trust definition under-specified / circular; no explicit threat actors; trust reduced to adversarial robustness only. *(academic §1.2 W5, §3.1, §3.2, §5 W5)*
- M3. Missing required appendices in `main_v2.tex`: Mentoring Plan and Synergistic Activities not `\input`. *(integrity §7, Priority-1)*
- M4. Budget still computed "over five years" in the v1 source and carries flagged placeholders; must be recomputed for 4 years. *(integrity §3, context §3)*
- M5. 19 candidate references all flagged NEEDS VERIFICATION (no verified authors/venues/IDs). *(integrity §4)*

**Minor**
- m1. Project-Summary keyword line present but first token is not the NSF 25-515 controlled class token. *(context §2, integrity notes)*
- m2. Dual-use / tool-gating governance thin; no explicit release-gating policy. *(academic §2, §3.5)*
- m3. Reproducibility commitment not pinned (no OSF pre-registration, no "reproducible on OpenVLA/Octo by Year 2" pledge). *(academic §3.4)*
- m4. Generalizability-beyond-robotics claim asserted without support. *(academic §2)*
- m5. DMSP terminology alignment + explicit open-source release commitment. *(context §2.4)*
- m6. Cosmetic: stray backtick in `facilities.tex`; stale commented budget totals. *(context §2)*

---

## 3. Issue-to-Section Mapping

| ID | Section / File | Severity |
|----|----------------|----------|
| C1 | `02_v2.tex` T1-1/T1-3, `01_v2.tex` novelty framing | Critical |
| C2 | `02_v2.tex` (defense subsection incl. L546 anomaly detector) | Critical |
| C3 | `02_v2.tex` T3 / evaluation (L263 tasks, L179 metrics) | Critical |
| M1 | `01_v2.tex` L150–151, `02_v2.tex` L39; timeline/task table | Major |
| M2 | `01_v2.tex` Overview (trust def), `02_v2.tex` T1 intro | Major |
| M3 | `main_v2.tex` (appendix wiring) | Major |
| M4 | `sections/budgetjustification_v2.tex` (L47 + all totals) | Major |
| M5 | `refs_v2_additions.bib` (19 keys) | Major |
| m1 | `sections/0_project_summary_v2.tex` L87 | Minor |
| m2 | `01_v2.tex` responsible-computing close; `sections/impact.tex` | Minor |
| m3 | `02_v2.tex` eval plan; `sections/datamanagement_v2.tex` | Minor |
| m4 | `sections/impact.tex` | Minor |
| m5 | `sections/datamanagement_v2.tex` | Minor |
| m6 | `sections/facilities.tex`, `budgetjustification_v2.tex` comments | Minor |

---

## 4. Category A — MECHANICAL / COMPLIANCE (safe to auto-apply now)

These are text-only, do not change the research design, and close integrity blockers. All are **safe to auto-apply** unless noted. (This plan does not apply them — user requested no `.tex` edits.)

| # | Action | File(s) | Priority | Effort | Auto-apply? |
|---|--------|---------|----------|--------|-------------|
| A1 | Add missing appendices: after `\input{sections/datamanagement_v2}` insert `\newpage\newsection{E}\input{sections/mentoring_v2}` and `\newpage\newsection{F}\input{sections/synergy}`; recompile. Resolves M3. | `main_v2.tex` | HIGH | 5 min | **Yes** — but PI must confirm whether Mentoring/Synergy go inline vs. as separate Research.gov supplements |
| A2 | Delete stale commented budget totals (context §2: L74 MTDC comment, L90 `%…$4,266,251 over five years`); flip residual "over five years"→"over four years" wording (numbers handled in C-track). Resolves M4 wording, m6. | `budgetjustification_v2.tex` | MEDIUM | 5 min | **Yes** (wording only; do not touch figures) |
| A3 | Remove cosmetic stray backtick artifact after "…2 PB of disk space and growing." | `facilities.tex` | LOW | 2 min | **Yes** |
| A4 | DMSP alignment: retitle "Data Management Plan"→"Data Management and Sharing Plan (DMSP)" and add explicit open-source/open-science release sentence (code, benchmarks, attack/defense tools) already promised elsewhere. Resolves m5. | `datamanagement_v2.tex` | MEDIUM | 15 min | **Yes** (do NOT change the "after five years" retention clause) |
| A5 | Add an explicit tool-gating / dual-use governance sentence (e.g., attack code released under institutional-affiliation DUA, delayed public release post-publication) to strengthen responsible-computing framing. Resolves m2. | `01_v2.tex` (IM close) and/or `sections/impact.tex` | MEDIUM | 20 min | **Yes** (framing only; PI should confirm the actual gating policy wording) |
| A6 | Add a one-line reproducibility pledge ("all experiments reproducible on OpenVLA + Octo on the Simpler benchmark by end of Year 2; protocol pre-registered on OSF"). Resolves m3. | `02_v2.tex` eval plan | LOW | 10 min | **Yes** (PI confirms OSF intent) |
| A7 | Soften/qualify the "extends beyond robotics" generalizability claim or cut it, per academic §2. Resolves m4. | `sections/impact.tex` | LOW | 10 min | **Yes** |

**Category A net effect:** clears M3, m2, m4, m5, m6 and the wording half of M4. None affect the score-driving Category B.

---

## 5. Category B — RESEARCH-SUBSTANCE (PI decisions / data required — DO NOT FABRICATE)

These four items set the funding ceiling. **None can be auto-applied**: they need real PI decisions, real experiments, or design commitments. This plan supplies *framing scaffolds and options only* — no invented success rates, detection numbers, or results.

| # | Issue | Concrete action (PI-owned) | File(s) | Priority | Effort | Auto-apply? |
|---|-------|----------------------------|---------|----------|--------|-------------|
| B1 | **C1 — Attack novelty.** | PI must design + justify ≥1 genuinely VLA-specific attack that exploits structure absent in VLMs: action-token adjacency / discretization-bin vulnerability, temporal action-consistency, or kinematic-coordination coupling. Add a formal argument for *why action quantization differs from language tokenization*. Frame current PGD/FGSM/C&W ports explicitly as **baselines**, not contributions. Candidate literature to position against (VERIFY): `puthumanaillam2026trajectory`, `tae2026drift`, `lu2026whenrobots`, `zhou2025badvla`. Target metric (reviewer): ≥20–25% improvement over naive ports. | `02_v2.tex` T1-1/T1-3, `01_v2.tex` contribution list (L212) | HIGH | Weeks (design + a preliminary run) | **No — PI input + data** |
| B2 | **C2 — Defense evidence.** | Run a preliminary adversarial-robustness eval of the action-space anomaly detector: generate white-box adversarial examples *constrained to the valid action space*, report **detection rate + false-positive rate** and threshold Pareto curve; compare to ≥2 baselines (input smoothing, adversarial training, ensemble). Reviewer bar: ≥70% detection at ≤5% FP on ≥2 models × ≥2 embodiments. Reframe detector honestly as *layered safety+security filter*, not sole defense, and note it does not cover poisoning/privacy. **Report only real measured numbers.** | `02_v2.tex` defense subsection (~L546) | HIGH | Weeks (experiments) | **No — data required** |
| B3 | **C3 — Evaluation rigor.** | PI decisions: (a) make **task-success-rate under attack** the primary metric and justify/derive the 30% deviation threshold from a physical consequence (or drop it); (b) add a **transferability matrix** (attack trained on M_i, tested on M_j) — even a small real one; (c) add ≥2–3 **baseline defenses**; (d) report **mean ± std over ≥10 runs / multiple seeds** with a significance test. Expand task set toward the reviewer's target only as far as data allows. Position with `li2025attackvla`, `sun2026maniparena` (VERIFY). | `02_v2.tex` T3 / eval (L179, L263, L264) | HIGH | Weeks–months | **No — data + PI design** |
| B4 | **M1 — Scope narrowing.** | Adopt an explicit staged plan (see §5.1 Option) — a minimum viable core in Years 1–2, remainder deferred to Years 3–4 — OR document co-PI/partnership access for real robots. This is a **design choice**; the plan below is presented as an OPTION, not a unilateral rewrite. | `01_v2.tex` L150–151, `02_v2.tex` L39, timeline/task table | HIGH | Days (rewrite) once PI decides | **No — PI decision** (once decided, rewrite is safe) |
| B5 | **M2 — Threat model / trust.** | Add explicit threat-actor profiles (white-box insider, black-box API, supply-chain/training-data, physical/sensor) × goals (task failure / specific harmful action / data extraction / trajectory corruption); replace the circular trust definition with an operational vector (robustness, interpretability, recovery time, safety margin). Map each defense to the threat(s) it addresses. Optionally align to NIST AI RMF. Content is largely a **writing** task but needs PI sign-off on which scenarios are in-scope. | `01_v2.tex` Overview trust def; `02_v2.tex` T1 intro | HIGH | Days | **Partial** — draft safely, PI confirms in/out-of-scope |

### 5.1 Scope-Narrowing Recommendation (OPTION for the PI — not applied)

Presented as a decision aid. The research design is **not** rewritten here; the PI chooses whether to adopt, and with which platforms.

**Minimum Viable Core — Years 1–2 (depth over breadth):**
- **Models:** 2 open, reproducible — **OpenVLA + Octo** (both public; avoids RT-2 55B / proprietary-access reproducibility risk flagged in academic §3.4, §1.2 W3.5).
- **Embodiments:** 2 — **Xarm7 (real)** + **Google robot (Simpler sim)**, matching the existing preliminary setup at `02_v2.tex` L263 (minimal new infra).
- **Tasks (T1 core):** the existing 3 sim + 3 real, plus enough additions to support a small transferability matrix.
- **Attacks:** white-box (PGD/C&W) + black-box token attacks **as baselines**, plus **the one novel VLA-specific attack (B1)**.
- **Defense:** action-space anomaly detector **with the preliminary eval (B2)** and ≥2 baselines.
- **Deliverable target:** one methods paper (novel attack) + one defense-evaluation result — directly answers academic §7 items 1–2.

**Staged to Years 3–4 (breadth, once the core lands):**
- **+Models:** RT-2 (cloud API only, no local reproduction) and/or ACT / RoboCat.
- **+Embodiments:** Franka and/or Spot (adds bi-manual / quadruped coverage).
- **T2 multimodal cross-modal attack propagation** — the reviewer's suggested deferral target (academic §5 W4).
- **T3 full safety-benchmark suite + interpretability** (`schofield2026chain`, `jahangard2025multimodal` — VERIFY) and the **full transferability matrix + certified defenses** (randomized smoothing, `seferis2025randomized` — VERIFY).
- Bound real-robot time (reviewer suggestion: ≤20–30 hrs/yr per embodiment).

**Trade-off note for the PI:** This preserves all aims and methods (nothing is cut, only *sequenced*), converting the "2–3 person / 6-year" perception (academic §1.2 W4) into a defensible single-PI/4-year plan. If the PI prefers to keep full breadth in Years 1–2, the alternative is to secure documented co-PI/partner platform access (Google Robotics / CMU / UC Berkeley per academic §3.6) and fund explicit PhD/postdoc effort rather than REU-only.

---

## 6. Category C — VERIFICATION (facts the PI must confirm; do not invent)

| # | Item | Action | File(s) | Priority | Effort | Auto-apply? |
|---|------|--------|---------|----------|--------|-------------|
| C-1 | **Budget recomputation (4-year).** | Recompute every duration-dependent figure for 4 years: PI summer salary (4 mo), grad support (Summer 2026–Spring 2030), undergrad wages, fringe (was $96,927/5yr), conference travel (years 2–4), Total Direct (was $408,435), MTDC, Indirect @45.5% (was $146,736), Total (was $555,171). Keep one-time GPU $12,500. Confirm single-PI, <$600K, under $1.2M RES cap. | `budgetjustification_v2.tex` | HIGH | 30–60 min | **No — PI computes** |
| C-2 | **SaTC PI-meeting travel placeholder.** | Replace `\$[PLACEHOLDER]` at L47 (1 trip/yr × 4 yrs × per-trip cost) with real per-trip cost; propagate into totals in C-1. | `budgetjustification_v2.tex` L47 | HIGH | 10 min | **No — PI value** |
| C-3 | **19 candidate references.** | For each key in `refs_v2_additions.bib` (7 cycle-1 models + 12 cycle-2 methods), verify real author list, venue, year, and arXiv ID/DOI; replace all "NEEDS VERIFICATION" markers; **drop any that do not resolve** (several are dated 2026 and may not yet exist). Do not invent IDs/authors. | `refs_v2_additions.bib` | HIGH | 1–2 hrs | **No — PI verifies** |
| C-4 | **Project-Summary controlled keyword token.** | The keyword line (`0_project_summary_v2.tex` L87) currently starts "trustworthy AI/ML security; …". Prepend the **exact NSF 25-515 controlled class token** (the RES/program-designated first keyword) per the solicitation's Project-Summary instructions. Topical terms may stay. | `0_project_summary_v2.tex` L87 | HIGH | 15 min (after checking 25-515) | **No — verify token, then safe** |
| C-5 | **Cycle-1 model availability.** | Confirm `gr00tn1`, `geminirobotics2025`, `pi05_2025`, `rdt1b`, `openvla_oft` are released/accessible as of submission; if not, reframe as "anticipated." | `01_v2.tex` emerging-models list; `refs_v2_additions.bib` | MEDIUM | 30 min | **No — PI verifies** |
| C-6 | **Internal-timeline ↔ budget duration.** | Spot-check the year-by-task figure/table in `02_v2.tex` reads 4 years to match the budget. | `02_v2.tex` | LOW | 10 min | **Yes** (once confirmed) |

---

## 7. Consistency Reconciliation

- **No new contradictions introduced.** Category A edits are wording/wiring; Category B reframes existing claims (ports→baselines; detector→layered filter) without changing aims or methods; Category C fixes numbers/refs.
- **Cross-section checks after edits:** (1) if B4 staging is adopted, update embodiment/model counts consistently in `01_v2.tex` L150–151, `02_v2.tex` L39, and the timeline table; (2) after C-1/C-2, re-verify Total Direct → MTDC → Indirect → Total chain and the mentoring/budget student-count alignment (integrity Priority-3 #5); (3) ensure the Project-Summary keyword token (C-4) and cover title stay consistent.
- **Integrity blockers status after plan:** M3 (appendices) → A1; M4 wording → A2, figures → C-1/C-2; M5 → C-3; keyword → C-4. All integrity Priority-1/2 items are covered.

---

## 8. Revision Traceability Map

```yaml
- original_issue: C1 attack novelty (ported methods)
  fix_applied: B1 (novel VLA-specific attack + baseline reframing)
  location: 02_v2.tex T1-1/T1-3; 01_v2.tex L212
  expected_improvement: raises perceived algorithmic novelty; addresses academic §7.1
- original_issue: C2 anomaly detector unvalidated
  fix_applied: B2 (preliminary detection/FP eval + baselines + honest reframing)
  location: 02_v2.tex ~L546
  expected_improvement: converts "strawman defense" into evidenced contribution (§7.2)
- original_issue: C3 evaluation gaps
  fix_applied: B3 (task-success metric, transferability, baselines, stats)
  location: 02_v2.tex L179/L263/L264
  expected_improvement: meets rigor/reproducibility bar (§3.4, §7.3)
- original_issue: M1 over-scope
  fix_applied: B4 + §5.1 staged option
  location: 01_v2.tex L150-151; 02_v2.tex L39; timeline table
  expected_improvement: single-PI/4-year feasibility perception (§3.6)
- original_issue: M2 threat/trust ambiguity
  fix_applied: B5 (actor profiles + operational trust vector)
  location: 01_v2.tex Overview; 02_v2.tex T1 intro
  expected_improvement: testable threat model; SaTC clarity (§3.1-3.2)
- original_issue: M3 missing appendices
  fix_applied: A1
  location: main_v2.tex
  expected_improvement: submission-complete (integrity §7)
- original_issue: M4 budget duration/placeholder
  fix_applied: A2 (wording) + C-1/C-2 (figures)
  location: budgetjustification_v2.tex
  expected_improvement: internal budget consistency, RES compliance
- original_issue: M5 unverified references
  fix_applied: C-3
  location: refs_v2_additions.bib
  expected_improvement: citation integrity for submission
- original_issue: m1 keyword token
  fix_applied: C-4
  location: 0_project_summary_v2.tex L87
  expected_improvement: NSF 25-515 Project-Summary compliance
- original_issue: m2/m3/m4/m5/m6 minor
  fix_applied: A5/A6/A7/A4/A3
  location: impact.tex, 02_v2.tex, datamanagement_v2.tex, facilities.tex
  expected_improvement: broader-impacts, reproducibility, DMSP, cosmetics
```

---

## 9. Revision Impact Assessment

```yaml
Revision Impact:
  Clarity Improvement:      HIGH   # B5 threat model + A-track wording remove circularity/ambiguity
  Feasibility Improvement:  HIGH   # B4/§5.1 staging directly answers the "Poor" scope-vs-investment score
  Reviewer Score Improvement: CONDITIONAL
    # Category A + C alone: keeps GOOD (3/5) — compliant but still "incremental" narrative
    # + B1 + B2 with real data: plausible GOOD -> VERY GOOD (4/5), matching academic §7 upgrade path
  Alignment Improvement:    MEDIUM-HIGH  # DMSP, keyword token, responsible-computing gating, RES budget
```

**Bottom line:** the mechanical and verification tracks make the proposal *submittable and compliant*; only the Category B experiments make it *competitive*.

---

## 10. Remaining Weaknesses (after this plan, if B-track deferred)

- If B1/B2 are not executed before submission, the "limited novelty" and "unvalidated defense" critiques persist and the score stays at Borderline GOOD.
- Real-robot feasibility remains a reviewer concern unless B4 staging is adopted or partnership/co-PI access is documented.
- 2026-dated references (C-3) carry residual risk: if they cannot be verified, positioning claims that lean on them must be softened.

---

## 11. Final Readiness Assessment

**Requires Another Revision Cycle.**

- **Compliance readiness:** achievable now via Category A + C (no science needed) — closes all integrity blockers.
- **Competitiveness readiness:** **blocked on PI-owned Category B data/decisions** (novel attack B1, detector evaluation B2, evaluation rigor B3, scope B4). These cannot be auto-applied or fabricated.

**Recommended order of operations:** A1–A7 and C-1…C-6 first (fast, safe, submission-critical) → PI decision on B4 scope option (§5.1) → B5 threat-model rewrite → B1/B2/B3 experiments as data allows.

```text
RE-ENTER REVIEW LOOP
```
Trigger after B-track data lands: Integrity Reviewer → Academic Reviewer → Revision Coach, to re-validate the novelty/evaluation claims against real results.
