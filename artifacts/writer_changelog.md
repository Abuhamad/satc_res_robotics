# Writer Change Log: CAREER to SaTC 2.0 RES (4-year) + Method Modernization

Current date: 2026-08-31. No original (non-`_v2`) file was edited. All source-of-truth
originals (`main.tex`, `01.tex`, `02.tex`, `refs.bib`, and every `sections/*.tex` without a
`_v2` suffix) are untouched. Dollar figures were not recomputed or invented; duration-dependent
figures carry an inline `% PI: recompute for 4-year duration` comment.

## Files created

1. `sections/budgetjustification_v2.tex` (copy of `sections/budgetjustification.tex`)
2. `sections/mentoring_v2.tex` (copy of `sections/mentoring.tex`)
3. `sections/summary_v2.tex` (copy of `sections/summary.tex`)
4. `sections/datamanagement_v2.tex` (copy of `sections/datamanagement.tex`)
5. `sections/0_project_summary_v2.tex` (copy of `sections/0_project_summary.tex`)
6. `artifacts/writer_changelog.md` (this file)

## Files edited

7. `main_v2.tex` (input rewiring only)
8. `02_v2.tex` (hedged SOTA method citations)
9. `refs_v2_additions.bib` (12 new candidate entries appended; existing 7 kept)

---

## Part A: CAREER to SaTC 2.0 RES, four-year

### `sections/budgetjustification_v2.tex`
- Senior Personnel: `outlined in the CAREER proposal` to `outlined in this SaTC 2.0 RES project`.
- Graduate support span: `Summer 2026 through Spring 2031` to `Summer 2026 through Spring 2030`.
- Fringe Benefits: `over five years` to `over four years`; appended `% PI: recompute for 4-year duration`. Number unchanged ($96,927).
- Travel: `for years 2 to 5` to `for years 2 to 4`.
- Travel: added a SaTC Principal Investigators' meeting line (one trip per year over four years) with the dollar amount as a marked placeholder `\$[PLACEHOLDER: PI to insert per-trip cost]` and an inline `% PI:` recompute comment.
- Total Direct Costs: `over five years` to `over four years`; appended recompute comment. Number unchanged ($408,435).
- Indirect Costs: `over five years` to `over four years`; appended recompute comment. Number unchanged ($146,736).
- Total Direct and Indirect Costs: `over five years` to `over four years`; appended recompute comment. Number unchanged ($555,171).
- Deleted stale commented five-year totals: `% \$413,585 over five years.` and `% \$4,266,251 over five years.`.
- One-time GPU workstation ($12,500) left unchanged.

### `sections/mentoring_v2.tex`
- L8: `involved in this CAREER project` to `involved in this SaTC 2.0 RES project`.
- Lowercase job-sense "career" words left unchanged.

### `sections/summary_v2.tex`
- `The educational components of this CAREER proposal integrate` to `... of this project integrate`.

### `sections/datamanagement_v2.tex`
- Header retitled `Data Management Plan` to `Data Management and Sharing Plan (DMSP)`.
- Added an open-source release commitment sentence (source code, benchmarks, attack and defense tools) in the Access to Data section.
- Data-retention "after five years" left unchanged (retention period, not project duration).

### `sections/0_project_summary_v2.tex`
- Title line replaced with `SaTC 2.0: RES: Toward Secure and Robust Generalist Robotic Models`.
- Overview / Intellectual Merit / Broader Impacts body replaced with content adapted from `sections/summary_v2.tex` so the standalone Project Summary matches the funded VLA-security project (the prior body described a different privacy/federated/human-in-the-loop project). The undefined `\xot` macro (defined only in `settings.tex`) was expanded to plain text "Cross-embodiment" since this file is standalone.
- Appended a Keywords line at the end of the Overview: `trustworthy AI/ML security; robotic foundation models; vision-language-action models; adversarial robustness; multimodal security; safety benchmarking` with `% VERIFY first keyword against NSF 25-515 controlled list`.
- PI/affiliation line left unchanged.

### `main_v2.tex`
- `\input{sections/budgetjustification}` to `\input{sections/budgetjustification_v2}`.
- `\input{sections/datamanagement}` to `\input{sections/datamanagement_v2}`.
- `\input{sections/mentoring}` to `\input{sections/mentoring_v2}`.
- `\input{sections/summary}` to `\input{sections/summary_v2}`.
- All other inputs unchanged.

---

## Part B: `02_v2.tex` method modernization (hedged, existing citations kept)

- T1-1 white-box: added a hedged clause on trajectory-level redirection and flow-matching-specific attacks. Cites `puthumanaillam2026trajectory,tae2026drift`.
- T1-1 poisoning/backdoor: added a hedged clause on objective-decoupled backdoors. Cites `zhou2025badvla`.
- T1-3 black-box transfer: added a hedged clause on universal transferable patch attacks. Cites `lu2026whenrobots`.
- T1-4 defenses: added a hedged sentence on VLA-specific defenses (structure-aware robust fine-tuning, randomized smoothing / certified robustness, backdoor token reconstruction), complementing the existing action-space anomaly detector paragraph. Cites `zhang2026structure,seferis2025randomized,li2026whenattention`.
- T1-4 evaluation plan: added a physically-grounded evaluation-protocol sentence. Cites `sun2026maniparena`.
- T2 multimodal: added a hedged sentence on physical attention-hijacking / patch attacks. Cites `zhang2026structure,yin2026vlaguard`.
- T2 evaluation plan: added a physically-grounded evaluation-protocol sentence. Cites `sun2026maniparena`.
- T3-1 safety benchmarks: added a hedged sentence on dedicated VLA security benchmarks and physically-grounded evaluation suites. Cites `li2025attackvla,sun2026maniparena`.
- T3-2 interpretability: added a hedged sentence on spatial-grounding attribution and neuro-symbolic spatial reasoning. Cites `schofield2026chain,jahangard2025multimodal`.

---

## Part C: `refs_v2_additions.bib`

Appended 12 new candidate entries after the existing 7 (header and prior entries kept):
`puthumanaillam2026trajectory`, `zhang2026structure`, `yin2026vlaguard`, `tae2026drift`,
`lu2026whenrobots`, `zhou2025badvla`, `seferis2025randomized`, `li2026whenattention`,
`li2025attackvla`, `sun2026maniparena`, `schofield2026chain`, `jahangard2025multimodal`.

- Titles and years taken from `artifacts/researcher_report.md`. `@inproceedings` used for reported
  venues (IROS/CVPR/EMNLP/ICRA 2025-2026), `@misc` with `howpublished = {arXiv preprint}` otherwise.
- `author = {NEEDS VERIFICATION}` for every entry; reported first-author surname placed in the
  `note` field only.
- Each entry carries a `VERIFY: ... confirm title, authors, venue, and arXiv id before submission` note.
- No arXiv identifiers were fabricated.

---

## Verification sweep

- No uppercase `CAREER` remains in the `_v2` section files.
- No `over five years`, `2031`, `years 2 to 5`, `413,585`, or `4,266,251` remain in the `_v2` files.
- Intentional leave-alones confirmed present: data-retention "after five years" in
  `datamanagement_v2.tex`; lowercase job-sense "career" in `mentoring_v2.tex`; experiment seed count
  "five random seeds" in `02_v2.tex`.

## Follow-ups for the PI (not done here)
- Recompute every duration-dependent dollar figure for the 4-year budget and insert the SaTC PI-meeting travel cost.
- Verify the Project Summary first keyword against the NSF 25-515 controlled vocabulary.
- Verify all 12 new bibliography entries (title, authors, venue, arXiv id) before submission.
- Build with `\bibliography{refs,refs_v2_additions}` so the new keys resolve.

---

## Part D: Integrate approved 4-year, two-investigator plan (with Auditor fixes)

Sources: `artifacts/research_plan_timeline.md` (plan) and `artifacts/auditor_feasibility.md`
(feasibility fixes). Only `_v2` files edited. No dollar totals changed; no arXiv IDs, author
lists, or budget amounts invented.

### `01_v2.tex`
- Intellectual Merit: named the concrete proposed contributions as hedged proposed research
  (ABBP and TTDA attack primitives; TACD and AGAT defenses; open VLA-SecBench with a
  cross-model transferability matrix and a spatial-action interpretability tool). Existing
  citations kept; framed as "research to be validated rather than completed results."
- Added one sentence introducing the two-investigator team (PI in AI/ML security, Co-PI in
  robot learning) with a `[Co-PI: TBD]` placeholder. No budget committed.

### `02_v2.tex`
- Preliminary study: added the Auditor 2.3 reconciliation sentence right after the
  30%-threshold figures, stating TSR replaces the proxy in the full protocol.
- T1-1: added an ABBP paragraph (gradient-based, 256-bin boundary crossing, kinematically
  consistent Jacobian constraint); PGD/FGSM/C&W framed as baselines; per Auditor 4.1 the
  L-infinity comparison is normalized to physical consequence and not overclaimed.
- T1-3: added a TTDA paragraph (gray/black-box, slow drift within per-step limits, absent in
  single-output VLMs); per Auditor 4.2 the pi-0/flow-matching extension is hedged as a
  Years 3-4 scale-up objective contingent on model availability.
- T1-4: added a TACD + AGAT paragraph. TACD = single multi-task trajectory-forecasting model
  conditioned on a task embedding with per-task thresholds on held-out benign episodes
  (Auditor 4.3). AGAT = kinematically-constrained adversarial fine-tuning via LoRA rank-16
  (Auditor 3.1/4.4). Evaluated against >=3 baseline defenses.
- T2: fixed the FiLM attribution (Auditor 4.5) to model-specific coupling targets (FiLM in
  RT-1, projection MLP in OpenVLA, cross-attention in Octo); removed ACT from the multimodal
  scope and added OpenVLA-OFT / language-conditioned Octo; presented T2 as a Years 3-4 track.
- Evaluation plans (T1 and T2): made TSR the primary metric, retained 30% action deviation as
  a secondary proxy, added the model x model x attack transferability matrix, >=3 baseline
  defenses, physical metrics, and mean +/- std over >=10 runs with Welch's t-test.
- New subsection "Work Plan, Timeline, and Team": staged MVP (Y1-2) vs scale-up (Y3-4)
  paragraph; a compact `tabular` Gantt table (`tab:workplan_timeline`) on the corrected
  calendar (Year 1 = Sep 2026-Aug 2027 ... Year 4 = Sep 2029-Aug 2030; Q1 Sep-Nov, Q2
  Dec-Feb, Q3 Mar-May, Q4 Jun-Aug per Auditor 1.1); a milestones list with the added gates
  M0 (compute), pre-submission Co-PI confirmation, pi-0 availability at Y2Q4, split TACD gate
  (M4a Y2Q2 + M4 Y2Q3), and interpretability validation moved to Y3Q4 (Auditor 1.3/1.4/5);
  a PI vs Co-PI division-of-labor table (`tab:division_labor`) with `[Co-PI: TBD]`; and a
  one-line compute plan (encoder-only ABBP, LoRA rank-16 AGAT, ACCESS Explore in Y1Q1).

### `sections/budgetjustification_v2.tex`
- Added a commented flag plus one visible sentence: budget must be recomputed to add the
  Co-PI; if combined direct costs exceed $600K a Collaboration Plan supplement is required;
  keep total under the $1.2M RES cap.
- Added an "Other Direct Costs -- Cloud Compute" placeholder line for RT-2/proprietary-VLA
  black-box API queries in Years 3-4, marked `% PI: confirm, ~$3-5K/yr`.
- No existing dollar totals changed; existing `% PI: recompute` flags left in place.

### Not done here (PI decisions)
- Confirm Co-PI identity, recompute the two-investigator budget, and prepare the Collaboration
  Plan if the $600K threshold is crossed.
- Build with LaTeX to verify the new tables render within the 15-page limit.
