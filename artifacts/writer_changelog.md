# Writer Changelog — (A)-type Editorial Revisions

**Date:** 2026-09-08
**Source of truth:** `artifacts/revision_plan.md` (Revision Coach synthesis)
**Scope:** Only (A)-type editorial fixes applied. (B)-type PI-owned items left untouched.
**Validation:** `main_v2.tex` compiles (pdflatex exit 0); no undefined citation keys; no new LaTeX errors.

---

## Applied Fixes

### R1 — Duplicate section label (P0, editorial)
- File: `main_v2.tex`
- Change: The second `\newsection{F}` (before `\input{sections/synergy}`) is now `\newsection{G}`. The Project Summary section keeps `F`. Section letters are now unique.

### R4 — Embodiment count consistency (P1, editorial)
- Files: `01_v2.tex`, `02_v2.tex`
- Change: Replaced "six robots, six embodiments" with an explicit, table-consistent statement: six robot embodiments (Franka, Google Robot, Spot, Hello Stretch, UR5, Xarm7) plus human demonstration data. This reconciles the prose with the 7 codes in `tab:multi_dataset` (F,G,S,H,U,M,X) by distinguishing the six robot platforms from the human ("M") data source.

### R5 — Dataset count clarity (P1, editorial)
- Files: `02_v2.tex`, `01_v2.tex`
- Change: Replaced the ambiguous "15 (=14+OXE)" phrasing with an explicit count: 15 dataset sources = 14 named robotics datasets (Table 1, including our own Xarm7 data) plus the Open X-Embodiment (OXE) repository, which itself aggregates 60 further robotic datasets. Mirrored the same clarification in `01_v2.tex`.

### R6 — De-escalate novelty overclaims (P1, editorial)
- File: `01_v2.tex` (three sites)
- Changes:
  - "uncharted threat landscape" -> "systematically investigate the threat landscape".
  - "presents the first comprehensive framework unifying..." -> "presents a systematic, unified framework spanning...".
  - "three main pioneering contributions ... the first comprehensive taxonomy and framework ... reveal previously unexplored vulnerabilities" -> "three main contributions ... a systematic taxonomy and unified framework ... surface under-studied vulnerabilities".
- Contribution preserved; primacy claims removed to match the already-hedged Project Summary and Research Plan, consistent with the concurrent 2025–26 work cited in the proposal.

### R7 — Real-time-vs-cloud reconciliation (P1, editorial)
- File: `02_v2.tex`
- Change: Uncommented and condensed the "Adoption and Constraints" block. The visible text now states the 3–10 Hz control-loop budget, keeps small models (ACT, Octo, RT-1) under the white-box model locally, and ties cloud-hosted large models (OpenVLA, RT-2) to the black-box threat model. Adds one sentence bounding TACD inference overhead against the same 3–10 Hz budget.

### R8 — Relationship to Concurrent Work (P1, editorial)
- File: `02_v2.tex`
- Change: Added a "Relationship to Concurrent Work" paragraph after the threat-model discussion. It positions BadVLA (`badvla`), AdvVLA (`advvla`), AttackVLA (`li2025attackvla`), and DRIFT (`tae2026drift`) as isolated single-model/component attacks, then differentiates this proposal on three axes: kinematic/Jacobian constraints, physical-consequence metrics across six embodiments, and a unified benchmark (VLA-SecBench) with a single multi-task detector (TACD). Only existing citation keys used; no new keys invented.

### R14 — Dual-use vs. open-source reconciliation (P2, editorial)
- Files: `01_v2.tex`, `sections/datamanagement_v2.tex`
- Change: Both sites now state a staged/controlled release: defenses, benchmarks, and datasets released openly; offensive attack tooling released under controlled, gated access (data-use agreements + responsible-disclosure review). Removes the conflict between "gated appropriately" and "open source under permissive licenses".

### R16 — Remove leftover editorial comments (P2, cleanup)
- Files: `01_v2.tex`, `sections/0_project_summary_v2.tex`
- Change: Removed the two `%TODO: add more deliverables.` markers (after T1 and T2 in `01_v2.tex`) and the `% VERIFY first keyword against NSF 25-515 controlled list` marker in the Project Summary. Only dead TODO/VERIFY markers removed; meaningful commented content (e.g., alternate dataset lists) left intact.

---

## Intentionally Left for the PI (not fabricated)

- **R2 (Co-PI identity/robotics credentials):** `[Co-PI: TBD]` in `01_v2.tex` left untouched. No Co-PI named, no robotics credentials fabricated.
- **R3 (Budget placeholder + totals):** `$[PLACEHOLDER]` and totals in `sections/budgetjustification_v2.tex` untouched. No budget numbers invented or recomputed.
- **R10 (Preliminary defense evidence):** No TACD/AGAT defense results or BadVLA/AdvVLA comparisons added. Requires real experiments.
- **R11 (Scope vs. staffing):** Committed scope not narrowed; coupled to the PI's R2 decision.
- **R9 (M0/ACCESS compute plan), R12 (go/no-go thresholds), R13 (threat-model trust wording), R15 (T3-2 rater protocol):** Not modified in this pass. Each would require a specific number (allocation size, acceptance threshold, rater count/agreement metric) not already present in the proposal; adding qualitative-only framing risked either fabricating figures or duplicating existing text, so these were deferred to the PI per the no-fabrication constraint.

---

## Self-Check

- pdflatex on `main_v2.tex`: exit 0, no errors.
- New citation keys (`badvla`, `advvla`, `li2025attackvla`, `tae2026drift`) all resolve in `main_v2.bbl`; no "Citation undefined" warnings.
- Section labels A–G now unique.
- Research design (aims, T0–T3, ABBP/TTDA/TACD/AGAT, VLA-SecBench) unchanged.
