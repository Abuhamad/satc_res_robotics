# Adversarial Feasibility & Methodological Audit
## NSF SaTC 2.0: RES: Toward Secure and Robust Generalist Robotic Models

**Auditor:** Auditor Agent
**Date:** 2026-09-08
**Scope:** Full compiled proposal — [main_v2.tex](../main_v2.tex) → [01_v2.tex](../01_v2.tex) (Overview, Intellectual Merit, Background), [02_v2.tex](../02_v2.tex) (Research Plan T0–T3, threat model, preliminary studies, dataset table, workplan/timeline), [sections/impact.tex](../sections/impact.tex), [sections/prior_support.tex](../sections/prior_support.tex), [sections/budgetjustification_v2.tex](../sections/budgetjustification_v2.tex), [sections/datamanagement_v2.tex](../sections/datamanagement_v2.tex), [sections/mentoring_v2.tex](../sections/mentoring_v2.tex), [sections/summary_v2.tex](../sections/summary_v2.tex), [sections/synergy.tex](../sections/synergy.tex), [sections/facilities.tex](../sections/facilities.tex), [sections/0_project_summary_v2.tex](../sections/0_project_summary_v2.tex), and the results figure source [figures/results/tr.tex](../figures/results/tr.tex). Cross-checked against prior planning artifacts [artifacts/research_plan_timeline.md](../artifacts/research_plan_timeline.md) and [artifacts/timeline_update.md](../artifacts/timeline_update.md), which are **stale planning inputs**, not part of the submitted document — several issues they previously flagged (Q3/Q4 swap, FiLM misattribution, TACD per-task model proliferation, missing LoRA spec for AGAT) have already been fixed in the current `_v2` proposal text. This audit evaluates the proposal **as it now stands**, not the earlier draft.

---

## 1. Executive Audit Summary

The proposal is **conceptually coherent and technically well-motivated** at the level of its four novel contributions (ABBP, TTDA, TACD, AGAT) and its staged MVP → scale-up structure. Compared to the version audited previously, the team has already closed several prior gaps: the workplan calendar is now internally consistent (Q1–Q4 run in chronological order and align with the budget's personnel span), TACD uses a single multi-task model, AGAT specifies LoRA rank-16 to stay compute-feasible, and the FiLM/OpenVLA architecture misattribution in the multimodal-attack description has been corrected.

However, the audit surfaces **new, submission-blocking defects** that a prior planning-stage review could not have seen because they only exist in the current text:

1. **A literal unresolved placeholder is present in the Intellectual Merit narrative itself** — "a Co-PI [Co-PI: TBD] contributing robot-learning and real-robot experimentation expertise" ([01_v2.tex](../01_v2.tex#L214)) — while the Budget Justification *does* name a Co-PI (George K. Thiruvathukal) whose stated contribution is "concurrent, parallel, and distributed modeling and analysis," not robotics. This is not a cosmetic issue: the document asserts robotics/hardware expertise that is nowhere substantiated for the actual named collaborator.
2. **A dollar-amount placeholder is left inside the Budget Justification**: "`\$[PLACEHOLDER]`" for Years 3–4 cloud/API compute ([sections/budgetjustification_v2.tex](../sections/budgetjustification_v2.tex#L59)), meaning the submitted budget total is not actually final.
3. **A factual self-contradiction in the core scope claim**: the narrative twice states "six robots, six embodiments" ([01_v2.tex](../01_v2.tex#L100), [02_v2.tex](../02_v2.tex#L37)), but the dataset table it references enumerates **seven** distinct embodiment codes (F, G, S, H, U, M, X) in its own caption and rows ([02_v2.tex](../02_v2.tex#L11-L27)).
4. The real-time-inference-vs-cloud-hosted-large-model tension — which the user explicitly asked this audit to check — **was written but then commented out** of the visible document ([02_v2.tex](../02_v2.tex#L262-L270), lines prefixed with `%`), leaving no discussion in the actual submitted text of how TACD's inference-time overhead or RT-2/OpenVLA's cloud/API dependence interacts with the 3–10 Hz real-time control constraint stated earlier in Background.
5. The compute-feasibility mitigation (NSF ACCESS allocation) appears **only as an orphaned milestone label** ("M0 compute/NSF ACCESS allocation secured") in the workplan figure caption ([02_v2.tex](../02_v2.tex#L740)) with no supporting body text, budget line, or contingency plan if the allocation is denied.

None of these defects invalidate the underlying research idea. All are correctable in a revision pass. But as currently written, the document would read to an NSF panel as **incompletely proofread and internally inconsistent on exactly the two questions (team composition, resource plan) reviewers weight most heavily for feasibility**. This drives the Feasibility score below the Technical-Merit score.

**Verdict: Major Revision Required** (see §15).

---

## 2. Problem Validation

**Strengths:**
- The problem (security/trustworthiness of VLA/generalist robotic foundation models) is real and under-addressed; the proposal correctly cites concrete precedent vulnerabilities (jailbreaking of LLM-controlled robots, adversarial attacks on quadrupedal locomotion) as existence proofs rather than speculation ([01_v2.tex](../01_v2.tex#L44-L47)).
- The motivation distinguishes this work from mature VLM/LLM adversarial-ML literature by identifying structurally distinct properties of robotic action spaces (discretized action bins, temporal action chunks) — a legitimate and underexplored gap, correctly scoped as "isolated vulnerabilities" in prior work rather than a systematic study ([01_v2.tex](../01_v2.tex#L58)).

**Weaknesses:**
- The "millions of industrial and service robots" framing in the Overview ([01_v2.tex](../01_v2.tex#L11)) is a generic industry-scale motivator rather than evidence tied to the specific generalist/VLA models this proposal studies (RT-1/RT-2/OpenVLA/Octo/ACT/RoboCat are research-stage models, not yet the deployed industrial base cited). This is a common but noticeable rhetorical overreach that a technical reviewer may discount.

**Risks:**
- If a reviewer perceives the deployed-robot framing as disconnected from the actual (research-prototype-stage) systems studied, it can weaken the "urgency" argument without weakening the technical contribution itself.

---

## 3. Logic Audit

Tracing Problem → Research Questions → Methodology → Evaluation → Outcomes:

**Strengths:**
- The three tasks (T1 vulnerability analysis, T2 modality-inherited vulnerabilities, T3 benchmarks) map cleanly onto the three stated Intellectual Merit contributions and onto the four proposed artifacts (ABBP, TTDA, TACD, AGAT) plus VLA-SecBench.
- Each attack/defense subsection explicitly separates "baseline" (PGD/FGSM/CW, existing VLM defenses) from "proposed contribution," and repeatedly uses hedged framing ("we frame this as research to be conducted," "contingent on model availability") rather than presenting unproven claims as settled results ([02_v2.tex](../02_v2.tex#L419), [02_v2.tex](../02_v2.tex#L520)). This is good academic discipline and reduces integrity risk.

**Missing Links:**
- The Evaluation Plan for T1/T2 promises a "full model × model × attack transferability matrix across the model families and embodiments in our scope" ([02_v2.tex](../02_v2.tex#L540)), but no text specifies which specific model×embodiment pairs are in scope for the *MVP* (Years 1–2) versus reserved for scale-up (Years 3–4), beyond the Staged Scope paragraph naming "two embodiments (Xarm7 and the Google robot)" ([02_v2.tex](../02_v2.tex#L665)). A reviewer cannot verify Objective-level success criteria from the visible text alone; the concrete ≥N×≥M sizing exists only in the internal planner artifact ([artifacts/research_plan_timeline.md](../artifacts/research_plan_timeline.md)), not in the proposal itself.
- T3-2 (Interpretability) promises "human-in-the-loop evaluations" ([02_v2.tex](../02_v2.tex#L654)) with no defined protocol (number of raters, agreement/reliability metric, task design). This is a logic gap between the claimed rigor of T1/T2 (Welch's t-test, ≥10 runs, mean±std) and the qualitative, unspecified rigor of T3-2.

---

## 4. Methodology Audit

**Attacks (ABBP, TTDA):**
- ABBP's core claim — that uniform 256-bin action discretization creates an exploitable "semantic continuity" allowing lower perturbation budget than equivalent language-token disruption — is explicitly and appropriately **hedged as unresolved**: "The claimed perturbation-budget advantage over these baselines is not assumed: our formal analysis will compare the required $L_\infty$ budget after normalizing to physical consequence" ([02_v2.tex](../02_v2.tex#L419)). This is honest framing, but it means the central novelty claim of ABBP is, by the proposal's own admission, unverified at submission time. This is acceptable for a research proposal but should be weighed as real technical risk, not treated as a settled contribution.
- TTDA is methodologically the stronger of the two: Octo's action-chunking creates a genuine, architecturally distinct attack surface absent in single-output VLMs, and the per-step-vs-sequence detection-evasion argument is internally consistent. The pi-0/flow-matching extension is correctly hedged as "contingent on model availability" ([02_v2.tex](../02_v2.tex#L521)) and correctly deferred to Years 3–4.

**Defenses (TACD, AGAT):**
- TACD's single multi-task trajectory-forecasting model (avoiding per-task model proliferation) is a sound fix from the earlier draft. The false-positive risk on real robots (legitimate task variability resembling anomalous sequences) is not explicitly discussed in the visible T1-4 text, though the M4a/M4 milestone split in the workplan figure caption implicitly acknowledges it.
- AGAT's LoRA rank-16 specification makes the defense computationally credible on the stated hardware budget. However, the robustness-accuracy tradeoff (AGAT may reduce clean TSR) is not given any explicit acceptance threshold in the visible text (no "if clean TSR drops by more than X%, pivot to Y" language), unlike the internal planner draft which had numeric go/no-go criteria. As submitted, a reviewer has no way to judge when this line of work would be considered to have failed.

**Multimodal attack (T2):**
- The vision-language coupling target list is now architecturally correct (FiLM for RT-1, projection MLP for OpenVLA, cross-attention for Octo — [02_v2.tex](../02_v2.tex#L577)), which fixes the error flagged in the prior audit round. This is a heterogeneous set of coupling mechanisms across models that differ by orders of magnitude in parameter count (RT-1 at 35M vs. OpenVLA at 7B); the proposal does not address whether a "tightly-coupled co-perturbation objective" formulated per-mechanism will support the claimed general conclusion ("coupling increases cross-embodiment transferability") or will instead produce three disconnected, non-comparable case studies. This is a moderate methodological risk to the T2 narrative's generalizability claim.

**Threat model formalism:**
- The formal notation ($\mathcal{M}$, $\mathcal{P}(\cdot)$, targeted/untargeted, white/gray/black-box) is clear, internally consistent, and correctly used to classify all subsequent attacks in Table `attacks_models`. This is one of the strongest sections of the proposal methodologically.
- The white-box threat model is justified narrowly and correctly: "This assumption is realistic since these robotic models typically incorporate open-source pre-trained visual encoders, making their architecture and parameters readily available" ([02_v2.tex](../02_v2.tex#L397)). This properly scopes white-box access to the encoder, not the full 7B model — which is the right fix for the black-box-vs-white-box tension the user asked about. **However, this scoping is stated only for the preliminary-experiment description, not restated as a standing constraint in the formal T1-1 White-box Attacks subsection**, so a careful reviewer could still ask whether ABBP's "gradient-based ... driving predicted action tokens across bin boundaries" ([02_v2.tex](../02_v2.tex#L419)) requires gradients through the action decoder (which sits downstream of the visual encoder and would need full-model access for OpenVLA/RT-2-scale models) — this is not resolved anywhere in the visible text.

---

## 5. Evaluation Audit

**Strengths:**
- Primary metric (task success rate under attack) plus secondary metrics (30% action-token deviation proxy, Attack Success Rate, Contain, Exactmatch, transferability, imperceptibility, end-effector displacement, safety-zone/force-threshold violation rate) is a genuinely comprehensive, physically-grounded metric suite ([02_v2.tex](../02_v2.tex#L538-L545)).
- Statistical rigor is explicit and appropriate: "mean ± std over at least ten runs with multiple seeds," Welch's t-test for significance ([02_v2.tex](../02_v2.tex#L544)).
- At least three named baseline defenses (input smoothing, VLM-ported adversarial training, ensemble voting) are specified for TACD/AGAT comparison ([02_v2.tex](../02_v2.tex#L520)) — this satisfies a common reviewer objection ("strawman defense") preemptively.
- The metric-consistency issue flagged in the prior audit round (preliminary results using the 30% threshold vs. the evaluation plan promising TSR) has been explicitly patched with a bridging sentence ([02_v2.tex](../02_v2.tex#L404-L406)). This fix is good.

**Missing Evidence / Weaknesses:**
- No explicit train/validation/held-out-test split protocol is described for any of T1–T3; "25 episodes over five runs" in the preliminary study ([02_v2.tex](../02_v2.tex#L247)) is a small per-condition sample, and the full evaluation plan does not commit to a larger N per task for the main study (only "≥10 runs" for statistical reporting, which is a run count, not an episode/task count).
- T3-2 interpretability evaluation ("human-in-the-loop... reviewing and interpreting the results" — [02_v2.tex](../02_v2.tex#L654)) has no defined inter-rater agreement metric, number of evaluators, or scoring rubric — this is qualitatively weaker than the rest of the evaluation plan and will likely draw a Methodology Reviewer objection.
- No ablation plan is stated for ABBP's Jacobian/kinematic-consistency constraint (i.e., what happens to attack success rate if the constraint is removed) — this ablation is exactly the evidence needed to support the "coordinated, kinematically-consistent" claim as the source of ABBP's advantage, and its absence weakens the evaluation's ability to attribute effect to mechanism.

---

## 6. Feasibility Audit

### 6.1 Scope Realism vs. Budget and Team

The project is **4 years** in duration (per the workplan figure caption, "Year 1 = May 2027–Apr 2028 ... Year 4 = May 2030–Apr 2031," [02_v2.tex](../02_v2.tex#L738)) and the budget's graduate-student span ("Summer 2027 through Spring 2031," [sections/budgetjustification_v2.tex](../sections/budgetjustification_v2.tex#L20)) is now internally consistent with that calendar — this is a material improvement over the version reviewed previously, where these two dates disagreed by 15 months.

Personnel: PI (1 summer month/year) + Co-PI (1 summer month/year) + 1 graduate student (continuously replaced on graduation) + 1 undergraduate (10 hr/week). This is standard staffing for a ~$555K single-cycle award, but it is thin relative to the described scope: six robot embodiments' worth of data, six model families (RT-1, RT-2, OpenVLA, RoboCat, Octo, ACT) each requiring implementation/fine-tuning/evaluation, four novel attack/defense methods, a public benchmark release, plus mentoring and curriculum/outreach deliverables — all across two research "tracks" (security/ML and robotics/real-robot). With one graduate student total (not per-track), the two-track parallelism described in Intellectual Merit ("enabling parallel progress on the security and robotics tracks," [01_v2.tex](../01_v2.tex#L214)) is not resourced: there is no second graduate student assigned to a robotics-specific track, and the budget confirms only one student line item.

### 6.2 Co-PI Identity, Expertise, and the TBD Placeholder — **CRITICAL**

- [01_v2.tex](../01_v2.tex#L214) (Intellectual Merit): "a Co-PI **[Co-PI: TBD]** contributing robot-learning and real-robot experimentation expertise."
- [sections/budgetjustification_v2.tex](../sections/budgetjustification_v2.tex#L15) (Budget): "George K. Thiruvathukal, Co-Principal Investigator ... will assist the PI in all aspects of the project ... and will also contribute to **concurrent, parallel, and distributed modeling and analysis efforts**."

These two passages describe two different people doing two different things. Nowhere in the document is Thiruvathukal's robotics or real-robot-hardware background established, and nowhere is the "[Co-PI: TBD]" bracket resolved. A reviewer reading straight through the document will notice the placeholder text on first pass — this is the single most damaging, easily fixed defect in the proposal, because it visibly signals the document was submitted without a final consistency pass. Substantively, it also means the plan's real-robot execution capacity (Xarm7 preliminary work notwithstanding — see §6.3) rests on an unconfirmed or mismatched collaborator.

### 6.3 Real-Robot Hardware Access

Preliminary experiments already used a physical Xarm7 for three tasks (Stack Cubes, Duck in Bowl, Sweep — [02_v2.tex](../02_v2.tex#L245-L249)), which is good evidence the team already has working real-robot access today, independent of the Co-PI question. However, [sections/facilities.tex](../sections/facilities.tex) only vaguely states that the co-hosted "Software and Systems Laboratory (SSL) ... has additional workstations, desks, and robotic equipment" ([sections/facilities.tex](../sections/facilities.tex#L11)) with no inventory of what "robotic equipment" means, no confirmation that it includes the Xarm7 used in preliminary work, and no mention of Franka/Spot/other embodiments named for Years 3–4 scale-up. This is a facilities-section gap independent of the Co-PI issue.

### 6.4 Compute Resources

- Budgeted equipment: a single "$12,500" GPU-equipped computer, purchased Year 1 ([sections/budgetjustification_v2.tex](../sections/budgetjustification_v2.tex#L53)), plus department-shared infrastructure ("+8 GPUs, +2TB RAM, +200 CPU cores," [sections/facilities.tex](../sections/facilities.tex#L18)) and an aging (2018) HPC cluster.
- The proposal's own compute-risk mitigations are real and reasonable (LoRA rank-16 for AGAT reduces trainable parameters to ~25M; white-box scope is implicitly limited to open visual encoders) but the **NSF ACCESS allocation**, which the workplan figure lists as gating milestone **M0** ("compute/NSF ACCESS allocation secured," [02_v2.tex](../02_v2.tex#L740)), is never mentioned in any body paragraph, budget line, or contingency statement. An externally-gated milestone with no supporting narrative is a red flag: a reviewer cannot evaluate a mitigation plan that exists only as a milestone label.
- Cloud/API cost for RT-2/proprietary-VLA black-box evaluation (Years 3–4) is an explicit unresolved placeholder: "`\$[PLACEHOLDER]`" ([sections/budgetjustification_v2.tex](../sections/budgetjustification_v2.tex#L59)). Total Direct/Indirect Costs ($408,435 / $146,736 / $555,171 total) are stated as final numbers despite this placeholder still being open, meaning the stated totals are not actually reconciled with the budget narrative above them.

### 6.5 Timeline / Milestone Realism

The workplan Gantt figure ([02_v2.tex](../02_v2.tex#L682-L747)) is now internally consistent: quarters run in chronological calendar order (Q1 May–Jul, Q2 Aug–Oct, Q3 Nov–Jan, Q4 Feb–Apr), and the graduate-student budget span aligns with the stated Year 1–4 calendar. Eight milestones (M0–M7) are distributed across the timeline with a sensible early-to-late progression (compute confirmation → formal attack spec → model zoo operational → attack-vs-baseline comparison → defense FP check → benchmark v0.5 + pi-0 availability check → multimodal coupling → benchmark v1.0 release). This is a legitimate improvement over the previous draft, which had a swapped quarter sequence and an off-by-15-months budget mismatch — both appear resolved.

Remaining timeline concerns:
- M0 (compute) and M5 (pi-0 availability) are both **externally gated, go/no-go-critical milestones with no stated fallback consequence** in the visible text (the fallback plans exist only in the internal planner artifact, not the proposal). A reviewer sees a diamond on a Gantt chart but no sentence explaining what happens on NO-GO.
- The Phase 2 (Years 3–4) scope — pi-0/flow-matching extension, multimodal coupling, certified-robustness defenses, full transferability matrix, VLA-SecBench v1.0 public release — remains a large simultaneous set of deliverables for one continuously-replaced graduate student plus an undergraduate, consistent with the staffing concern in §6.1.

### 6.6 Risk Register (Constructed by This Audit — Not Present as a Standalone Section in the Proposal)

| Risk | Category | Likelihood | Severity | Mitigation |
|---|---|---|---|---|
| Co-PI identity/expertise unresolved before submission | Execution / Funding | High (currently true) | **High** | Resolve "[Co-PI: TBD]" before submission; either substantiate Thiruvathukal's role with concrete robotics-adjacent contribution (e.g., distributed training infra, benchmark software engineering) or add a second collaborator with real-robot expertise |
| Budget placeholder (`$[PLACEHOLDER]`) unresolved | Funding | High (currently true) | **High** | Fill in cloud/API cost estimate and recompute indirect costs before submission |
| Compute gap for 7B-parameter white-box/AGAT work | Technical | Medium | High | State the ACCESS application plan in body text (not only the figure caption); define explicit fallback (encoder-only scope) if ACCESS is denied |
| ABBP normalization argument may fail to show claimed advantage | Technical | Medium | Medium | Proposal already hedges this appropriately; ensure go/no-go framing is visible to reviewers, not only claimed as "future work" |
| Six vs. seven embodiments inconsistency | Integrity / Consistency | High (currently true) | Low–Medium | Recount table rows and correct prose to match, or vice versa |
| Real-time inference vs. cloud-hosted large-model tension unaddressed | Methodological | Medium | Medium | Reinstate (edited) discussion of TACD inference latency and RT-2/OpenVLA cloud dependence under the 3–10 Hz constraint |
| Single graduate student across two tracks (security + robotics) | Execution | Medium–High | Medium | Either scope down to what one student can realistically execute per track-year, or clarify Co-PI's own students/lab contribute additional labor |
| T3-2 interpretability evaluation protocol underspecified | Evaluation | Medium | Low–Medium | Define rater count, task set, and an agreement metric (e.g., Cohen's κ) |
| Year 3–4 deliverable load (pi-0 extension, multimodal, certified robustness, benchmark v1.0) | Execution | Medium | Medium | Explicitly mark 1–2 Year-4 deliverables as "preprint/contingent" rather than committed |

---

## 7. Assumption Audit

```yaml
Assumption: "Adjacent action-bin perturbations require lower L_inf budget than equivalent language-token disruption (ABBP's core premise)"
Evidence: "Not yet demonstrated; proposal explicitly commits to a normalization study rather than assuming this holds"
Risk: "If normalization shows no advantage, ABBP reduces to a variant of PGD with extra constraints"
Impact: "Weakens, but does not eliminate, Aim 1 — TTDA remains the stronger fallback contribution"

Assumption: "Open-source visual encoders (DINOv2, SigLIP, EfficientNet, ResNet) are a realistic white-box attack surface because they are publicly released"
Evidence: "Reasonable and stated explicitly in the preliminary-study text"
Risk: "Low — this is a well-supported assumption in the adversarial-ML literature"
Impact: "Low; strengthens T1-1 threat-model realism"

Assumption: "The Co-PI brings robot-learning and real-robot experimentation expertise"
Evidence: "None provided for the named Co-PI (Thiruvathukal); budget describes his role as parallel/distributed computing"
Risk: "High — unverified expertise claim in Intellectual Merit"
Impact: "Directly undermines credibility of the robotics/hardware execution track"

Assumption: "A single $12,500 workstation plus department HPC resources plus a not-yet-secured NSF ACCESS allocation is sufficient for training/attacking 6 model families including a 7B-parameter VLA"
Evidence: "Partially mitigated via LoRA and encoder-only white-box scoping, but ACCESS plan is not described in body text"
Risk: "Medium-High if ACCESS is denied or delayed"
Impact: "Would force late-stage descoping of white-box and AGAT work on OpenVLA-scale models"

Assumption: "TACD's single multi-task forecasting model generalizes false-positive control across ≥10 tasks and ≥2 embodiments without per-task retraining"
Evidence: "Asserted design choice, not yet validated; per-task threshold calibration is stated but FP rate across heterogeneous tasks is unmeasured"
Risk: "Medium"
Impact: "Could require reverting to per-task models, reintroducing the overhead this design was meant to avoid"

Assumption: "Six robots / six embodiments accurately describes the data mixture"
Evidence: "Contradicted by the dataset table's own seven embodiment codes (F, G, S, H, U, M, X)"
Risk: "Low technical risk, but a checkable factual error"
Impact: "Reviewer confidence in the document's care/precision"
```

---

## 8. Funding Alignment Audit

**Strengths:**
- Strong fit to NSF SaTC's core mission (secure and trustworthy computing) applied to an emerging, underexplored system class (generalist robotic foundation models). The taxonomy-building, threat-modeling, and open-benchmark deliverables map directly onto SaTC's community-infrastructure goals.
- Broader Impacts ([sections/impact.tex](../sections/impact.tex), [sections/0_project_summary_v2.tex](../sections/0_project_summary_v2.tex)) correctly emphasize open-source release, cross-domain transfer of methods (to "adjacent domains" beyond robotics), and education/outreach — consistent with SaTC's broadening-participation and community-benefit expectations.
- Prior NSF support ([sections/prior_support.tex](../sections/prior_support.tex)) — an EAGER on AI-security training and a large CyberCorps SFS award — is directly relevant and demonstrates a track record of delivering security-education outcomes, which strengthens confidence in the mentoring/curriculum deliverables specifically (separate from the technical robotics deliverables, which have no comparable track-record evidence for either PI or Co-PI).

**Weaknesses:**
- Responsible-disclosure and dual-use handling for the attack tooling is addressed in a single sentence — "released attack tooling will be gated appropriately to prevent misuse" ([01_v2.tex](../01_v2.tex#L219)) — with no specifics (embargo period, controlled-release mechanism, review board, or DUA terms), despite the Data Management Plan committing to fully open-source release "under permissive licenses" ([sections/datamanagement_v2.tex](../sections/datamanagement_v2.tex#L20)). These two statements are in mild tension: "gated appropriately" vs. "open source under permissive licenses" is not reconciled.

**Risks:**
- A Program Officer/reviewer focused on responsible dual-use practices for offensive security research may ask for a concrete gating mechanism; as written, the commitment is aspirational rather than procedural.

---

## 9. Execution Risk Audit

```yaml
Risk: "Co-PI role/identity unresolved at submission"
Likelihood: "High (present in current text)"
Severity: "High"
Mitigation: "Resolve before submission; single highest-priority fix in this audit"

Risk: "Compute allocation (NSF ACCESS or equivalent) not secured by Year 1"
Likelihood: "Medium"
Severity: "High"
Mitigation: "State the application plan and timeline in body text; define explicit descope fallback"

Risk: "pi-0 (or equivalent open flow-matching model) unavailable for Years 3-4 TTDA/T2 extension"
Likelihood: "Medium"
Severity: "Medium"
Mitigation: "Already partially hedged via 'contingent on model availability' language; no named substitute model is given in the visible text"

Risk: "Single graduate student cannot sustain parallel security-ML and real-robot tracks across 4 years"
Likelihood: "Medium-High"
Severity: "Medium"
Mitigation: "Clarify Co-PI-side student/lab contributions, or reduce claimed track parallelism"

Risk: "Benchmark release (VLA-SecBench v1.0) dual-use review adds unplanned schedule risk in Year 4"
Likelihood: "Medium"
Severity: "Medium"
Mitigation: "Define the dual-use/gating review process now, budget time for it explicitly in Year 4"

Risk: "ABBP found to offer no measurable advantage over PGD after normalization"
Likelihood: "Medium"
Severity: "Medium (not fatal — TTDA/TACD/AGAT stand independently)"
Mitigation: "Already correctly gated as a go/no-go check per the internal plan; make this explicit in the proposal text itself, not only internally"
```

---

## 10. Contradiction Analysis

```yaml
Contradictions:
  - Issue: "Co-PI identity and expertise"
    Evidence: "01_v2.tex line 214 says '[Co-PI: TBD] ... robot-learning and real-robot experimentation expertise'; budgetjustification_v2.tex line 15 names George K. Thiruvathukal with 'concurrent, parallel, and distributed modeling and analysis' expertise"
    Severity: "Critical"

  - Issue: "Embodiment count"
    Evidence: "01_v2.tex line 100 and 02_v2.tex line 37 both state 'six robots, six embodiments'; Table multi_dataset (02_v2.tex lines 11-27) caption and rows show seven distinct embodiment codes (F, G, S, H, U, M, X)"
    Severity: "Minor-Moderate (factual, easily fixed, but checkable by any careful reviewer)"

  - Issue: "Open-source release commitment vs. dual-use gating commitment"
    Evidence: "01_v2.tex line 219 ('gated appropriately to prevent misuse') vs. datamanagement_v2.tex line 20 ('open source under permissive licenses')"
    Severity: "Minor-Moderate"

  - Issue: "Real-time inference constraint raised in Background but not connected to the evaluation/defense plan"
    Evidence: "01_v2.tex / 02_v2.tex Background states 3-5Hz / 3-10Hz real-time constraints as a core challenge; the paragraph that would have connected this constraint to TACD inference overhead and cloud-hosted large-model (RT-2/OpenVLA) deployment is commented out in 02_v2.tex (lines ~262-270, prefixed with %)"
    Severity: "Moderate — a requested audit item with no visible resolution"

  - Issue: "Compute mitigation milestone (M0/NSF ACCESS) has no supporting body text or budget line"
    Evidence: "02_v2.tex line 740 (figure caption) references M0 'compute/NSF ACCESS allocation secured'; no other occurrence of 'ACCESS' anywhere in 01_v2.tex or 02_v2.tex body text"
    Severity: "Moderate"

  - Issue: "Budget total finality vs. open placeholder"
    Evidence: "budgetjustification_v2.tex states final Total Direct ($408,435), Indirect ($146,736), and Total ($555,171) costs while an unresolved '\$[PLACEHOLDER]' cloud-compute line remains open above it (line 59)"
    Severity: "Moderate-High (internal arithmetic cannot be verified as final)"
```

---

## 11. Reviewer Objections (Simulated)

```yaml
Reviewer Objections:
  Reviewer A (Technical Reviewer): >
    "ABBP's central claim — that action-bin discretization offers a perturbation-budget
    advantage over continuous language-token attacks — is explicitly unproven at
    submission time, and the proposal does not explain how gradients will be obtained
    through the LLM action decoder for 7B-parameter models given the stated $12,500
    single-workstation budget. The white-box threat model is only clearly justified for
    the visual encoder in the preliminary-study text, not restated as a scope limit in
    the formal T1-1 subsection. I would want a concrete compute plan, not a milestone
    label referencing an unsecured ACCESS allocation."

  Reviewer B (Methodology Reviewer): >
    "The T1/T2 evaluation protocol (TSR, ≥10 runs, Welch's t-test, physically-grounded
    secondary metrics) is genuinely solid. But T3-2's interpretability evaluation is
    qualitative with no stated rater count or agreement metric, which is inconsistent
    with the rigor shown elsewhere. I also could not find an ablation isolating the
    claimed benefit of ABBP's kinematic-consistency constraint from a plain multi-DOF
    PGD variant."

  Reviewer C (Program Reviewer): >
    "The Intellectual Merit section states the project is 'led by a two-investigator
    team' with the Co-PI providing 'robot-learning and real-robot experimentation
    expertise,' but the Co-PI is literally listed as '[Co-PI: TBD]' in the same sentence,
    while the Budget Justification names a different collaborator whose background,
    as described, is parallel and distributed computing rather than robotics. I cannot
    assess feasibility of the real-robot execution track without knowing who is actually
    doing this work. There is also an unresolved dollar-amount placeholder in the
    budget. These should have been resolved before submission."
```

---

## 12. Failure Mode Analysis

```yaml
Failure Modes:
  - Issue: "Panel perceives document as not submission-ready due to visible placeholder text and budget gap"
    Likelihood: "High if submitted as-is"
    Severity: "High — can trigger administrative return or a strongly negative first impression independent of technical merit"

  - Issue: "Co-PI robotics expertise challenged, undermining confidence in real-robot deliverables (T0 data collection, Xarm7 scale-up, Years 3-4 new embodiments)"
    Likelihood: "Medium-High"
    Severity: "High"

  - Issue: "ABBP's core novelty claim does not survive the promised normalization analysis"
    Likelihood: "Medium"
    Severity: "Medium (mitigated by TTDA/TACD/AGAT as independent contributions)"

  - Issue: "Compute insufficient for planned white-box/AGAT experiments on OpenVLA-scale models if ACCESS allocation is delayed or denied"
    Likelihood: "Medium"
    Severity: "Medium-High"

  - Issue: "Overambitious Year 3-4 deliverable set (pi-0 extension, multimodal coupling, certified robustness, VLA-SecBench v1.0) for the staffing level described"
    Likelihood: "Medium"
    Severity: "Medium"

  - Issue: "Weak broader-impacts specificity on dual-use/responsible-disclosure practice for released attack tooling"
    Likelihood: "Low-Medium"
    Severity: "Low-Medium"
```

---

## 13. Repair Recommendations (Priority-Ordered)

### Critical Priority

**C1 — Resolve the Co-PI identity/expertise contradiction before submission**
- Issue: [01_v2.tex](../01_v2.tex#L214) contains literal placeholder text "[Co-PI: TBD]" describing robot-learning/real-robot expertise, while [sections/budgetjustification_v2.tex](../sections/budgetjustification_v2.tex#L15) names a different collaborator with parallel/distributed-computing expertise.
- Recommendation: Either (a) confirm Thiruvathukal's actual planned contribution and rewrite the Intellectual Merit sentence to match it truthfully (e.g., contributing to scaled training/benchmark infrastructure rather than "real-robot experimentation"), or (b) add/confirm a collaborator with genuine robotics/hardware background and update both documents consistently.
- Expected Benefit: Removes the single most visible and damaging inconsistency in the proposal.
- Priority: Critical.

**C2 — Fill in the budget placeholder and recompute totals**
- Issue: "`\$[PLACEHOLDER]`" cloud/API cost line ([sections/budgetjustification_v2.tex](../sections/budgetjustification_v2.tex#L59)) while Total Direct/Indirect/Overall costs are presented as final.
- Recommendation: Insert the estimated $3–5K/year figure (or actual computed value), recompute indirect costs and totals, and remove the placeholder before submission.
- Priority: Critical.

### High Priority

**H1 — Fix the six-vs-seven embodiment inconsistency**
- Issue: Prose claims "six robots, six embodiments" ([01_v2.tex](../01_v2.tex#L100), [02_v2.tex](../02_v2.tex#L37)) contradicting the dataset table's seven embodiment codes ([02_v2.tex](../02_v2.tex#L11-L27)).
- Recommendation: Recount the table and correct the prose (or table) to a single consistent number.

**H2 — State the compute-mitigation plan in body text, not only as a milestone label**
- Issue: M0 ("NSF ACCESS allocation secured") appears only in the workplan figure caption with no supporting narrative anywhere in [02_v2.tex](../02_v2.tex).
- Recommendation: Add 2–3 sentences to T1-1 or the Work Plan section stating the ACCESS application plan, expected allocation size, timing, and the explicit fallback (e.g., encoder-only white-box scope) if the allocation is denied.

**H3 — Reinstate (in edited form) the real-time-inference-vs-cloud-hosted-model discussion**
- Issue: The relevant paragraph is commented out in [02_v2.tex](../02_v2.tex#L262-L270), leaving the real-time (3–10 Hz) constraint raised in Background unconnected to the evaluation/defense plan.
- Recommendation: Add a short paragraph in T1-4 or the Evaluation Plan noting that TACD's inference-time overhead must remain within the robot's control-loop budget, and that RT-2/OpenVLA-scale models evaluated via cloud API are treated under the black-box threat model for exactly this reason (tying the architecture-scale split directly to the threat-model split already present in the text).

### Medium Priority

**M1 — Add explicit go/no-go acceptance thresholds into the visible proposal text**
- Issue: Numeric go/no-go criteria (e.g., ABBP vs. PGD improvement threshold, TACD false-positive ceiling, AGAT clean-TSR degradation ceiling) exist only in the internal planning artifact, not in the submitted document.
- Recommendation: State at least one quantitative threshold per major contribution directly in the T1/T1-4 text so reviewers can evaluate falsifiability.

**M2 — Define the T3-2 human-in-the-loop evaluation protocol**
- Issue: No rater count, task set, or agreement metric specified ([02_v2.tex](../02_v2.tex#L654)).
- Recommendation: Add a sentence specifying number of evaluators, evaluation task sample size, and an inter-rater agreement statistic.

**M3 — Reconcile the "gated" vs. "fully open-source" dual-use language**
- Issue: [01_v2.tex](../01_v2.tex#L219) vs. [sections/datamanagement_v2.tex](../sections/datamanagement_v2.tex#L20).
- Recommendation: State a concrete release mechanism (e.g., staged release, DUA-gated attack code with openly released defenses/benchmarks) that reconciles both commitments.

**M4 — Clarify per-track staffing**
- Issue: Intellectual Merit claims "parallel progress on the security and robotics tracks" ([01_v2.tex](../01_v2.tex#L214)) with only one graduate student in the budget.
- Recommendation: Either state that the Co-PI's own lab/students contribute additional labor to the robotics track, or reduce the parallelism claim to match actual staffing.

### Low Priority

**L1 — Remove leftover editorial TODO comments** ("`% VERIFY first keyword against NSF 25-515 controlled list`" in [sections/0_project_summary_v2.tex](../sections/0_project_summary_v2.tex), "`%TODO: add more deliverables`" in [01_v2.tex](../01_v2.tex#L184,192)). These are invisible in the compiled PDF but indicate unfinished internal review passes; verify before final compile.

**L2 — Clarify the travel budget line** ("2 trips × $2,500 = $5,000 for years 2 to 4," [sections/budgetjustification_v2.tex](../sections/budgetjustification_v2.tex#L38)) — ambiguous whether this is a per-year or one-time total across three years.

---

## 14. Risk Scorecard

```yaml
Risk Scorecard:
  Problem Clarity:            8/10
  Methodological Soundness:   7/10
  Evaluation Strength:        7/10
  Feasibility:                5/10
  Alignment:                  8/10
  Risk Exposure:              5/10
  Reviewer Readiness:         4/10
```

**Numeric summary scores requested by the audit brief:**

```yaml
Feasibility Score:      5 / 10
Technical-Merit Score:  7 / 10
```

Feasibility is held down primarily by the Co-PI identity/expertise contradiction, the unresolved budget placeholder, and the unnarrated compute-mitigation plan — all fixable, none reflecting a flaw in the underlying research design. Technical Merit is held at a solid but not excellent level by the appropriately-hedged-but-still-unproven ABBP novelty claim, the underspecified T3-2 evaluation protocol, and the excised real-time/cloud-hosted-model discussion.

---

## 15. Advancement Decision

```yaml
Decision: Major Revision Required
Rationale: >
  No Critical score (Methodological Soundness, Feasibility, Evaluation Strength,
  Alignment) falls below 5, so a full Reframe is not warranted — the research
  direction itself is sound and several issues flagged in a prior audit round
  (calendar consistency, FiLM misattribution, TACD proliferation, AGAT compute
  infeasibility) have already been correctly fixed in this version. However,
  Feasibility (5/10) falls below the 7 threshold required for "Ready With
  Revisions," driven by two submission-blocking, easily-fixed defects (the
  literal "[Co-PI: TBD]" placeholder contradicting the named Budget Co-PI, and
  the unresolved "$[PLACEHOLDER]" budget line) plus one real, only-partially-
  mitigated resource risk (compute for 7B-parameter white-box/AGAT work gated on
  an unsecured, unnarrated NSF ACCESS allocation). These must be resolved before
  the proposal is submission-ready. Recommend a focused revision pass addressing
  §13's Critical and High priority items before advancing to Planning.
```

---

*Feasibility and methodological audit produced by Auditor Agent, 2026-09-08. All findings are grounded in direct citation of the source files listed in the header. No research results are fabricated; findings are limited to what is verifiable from the provided documents. Priority labels (Critical/High/Medium/Low) reflect risk to proposal fundability and submission-readiness, not scientific interest.*
