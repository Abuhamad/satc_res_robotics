# Feasibility Audit — NSF SaTC 2.0 RES Proposal
## 4-Year, Two-Investigator Plan: Secure and Trustworthy VLA Robotic Foundation Models

**Auditor:** Auditor Agent  
**Date:** 2026-08-31  
**Sources audited:**  
- `artifacts/research_plan_timeline.md` (Planner Agent, 2026-08-31)  
- `01_v2.tex` (Overview and background)  
- `02_v2.tex` (Research plan, tasks T0–T3, preliminary experiments)  
- `sections/budgetjustification_v2.tex` (Budget, personnel, direct/indirect costs)

---

## Executive Feasibility Summary

The research plan is **scientifically coherent and well-structured** at the level of aims and work packages. The staged MVP / scale-up architecture is the plan's strongest feature and directly addresses the prior panel's scope concern. However, **five HIGH-severity structural problems must be resolved before the Writer integrates this plan into the proposal**. Three are fatal in isolation: (1) the plan's Year-1 start (~Sep 2027) is ~12–15 months later than the budget's personnel span (Summer 2026–Spring 2030), creating a 4-year calendar that maps onto nothing the budget actually funds; (2) the budget has no Co-PI — the plan's entire two-investigator structure is funded by a $555K single-PI award that nowhere mentions a Co-PI, yet the plan assigns ~40% of all deliverables to that unconfirmed Co-PI; (3) the Year-1 Quarter labels Q3 (Jul–Aug) and Q4 (Mar–May) are chronologically swapped, which will produce an incoherent timeline figure in the proposal. Additional HIGH issues concern compute inadequacy (a $12,500 single-GPU node cannot run OpenVLA 7B white-box attacks or AGAT adversarial fine-tuning) and a Year-4 deliverable overload. All five HIGH issues have concrete, minimal fixes listed below.

---

## 1. TIMELINE FEASIBILITY

### 1.1 Year-Quarter Calendar Labels — **HIGH**

**Problem:**  
In Part 11 (Timeline), Year 1 quarters are labeled in non-chronological order:  
- Q1: Sep–Nov (fall) ✓  
- Q2: Dec–Feb (winter) ✓  
- Q3: Jul–Aug ← labeled "US academic calendar — summer" **but listed as the third period, after Dec–Feb**  
- Q4: Mar–May ← labeled "academic spring" **but listed last, after Jul–Aug**  

A year that runs Q1 Sep→Q2 Dec→Q3 Jul→Q4 Mar is not a valid sequence. Q3 and Q4 are swapped relative to calendar order. Every task timeline keyed to "Y1Q3" or "Y1Q4" will be misread. For example, WP1-T2 (ABBP implementation) is labeled "Y1Q3," which the mislabeled calendar makes appear to be a summer activity, but the work logically belongs in spring (Mar–May), after the Q2 formalization.

**Concrete fix for Writer:**  
Relabel Year 1 (and all subsequent years) uniformly:  
- Q1: Sep–Nov (fall)  
- Q2: Dec–Feb (winter)  
- Q3: Mar–May (spring)  
- Q4: Jun–Aug (summer)  

Then verify all task timelines (WP0 through WP6) against the corrected mapping. No tasks need to move; only the quarter labels and their narrative descriptions change.

---

### 1.2 Year-1 Start Date vs. Budget Personnel Span — **HIGH** (see also §6)

**Problem:**  
The plan states "Year 1: ~Sep 2027 – Aug 2028 ... Year 4: ~Sep 2030 – Aug 2031." The budget justification states the graduate student is "supported from **Summer 2026** through **Spring 2030**." These spans are mutually exclusive: the budget's 4-year period runs approximately Jun 2026 – May 2030, ending 17 months before the plan's Year 4 closes. Under the plan's calendar, the graduate student who provides most experimental execution (WP0–WP2) would leave the project midway through Year 3.

**Concrete fix for Writer:**  
Replace the plan's header date range with the budget-consistent window:  
- Year 1: ~Sep 2026 – Aug 2027  
- Year 2: ~Sep 2027 – Aug 2028  
- Year 3: ~Sep 2028 – Aug 2029  
- Year 4: ~Sep 2029 – Aug 2030  

Propagate this change to all section headers, milestone dates (M1 → Y1Q2 = Dec 2026–Feb 2027, etc.), and any figures. This is a find-and-replace operation requiring no science changes.

---

### 1.3 Critical Path: WP0→WP1→WP2→WP5 — **MEDIUM**

**Assessment:**  
The critical path (WP0-T1 → WP1-T2 → WP1-T6 → WP2-T5 → WP5-T1) traverses 6 dependent tasks across 7 quarters, ending at WP5-T1 in Y2Q4. This is feasible in principle if each task delivers on time. Specific pressure points:

- **WP0-T1 (fine-tune OpenVLA + Octo)** must complete Y1Q1–Q2. OpenVLA 7B fine-tuning is computationally intensive (see §3 below); if compute is not confirmed in Q1, this gate slips and delays every downstream WP.
- **WP1-T6 (ABBP vs. PGD comparative evaluation)** depends on WP1-T2 (ABBP code), WP1-T5 (baselines), and WP3-T1 (metric framework). All three have a Y1Q2–Q3 earliest start and are assigned partially to the PI. With the corrected calendar (WP1-T6 = Y2Q1, Jan–Mar), only 1–2 quarters separate baseline completion from full comparative evaluation. This is tight but not unrealistic.
- **WP2-T5 (defense comparison paper)** depends on four predecessors (WP2-T2, WP2-T3, WP2-T4, WP3-T1). All must complete by Y2Q2 (Dec–Feb), leaving one quarter (Y2Q3, Mar–May) for comparative evaluation runs. This is the tightest squeeze on the critical path; a 4–6 week slip in any one predecessor delays the defense paper submission.

**Flag:** WP2-T5 and Milestone M4 are both scheduled at Y2Q3. The go/no-go check (M4: TACD detection characterization) and the comparative evaluation that produces the defense paper are the same task. If M4 triggers a NO-GO (FP >15%), there is no buffer to recover before the defense paper deadline. Recommend splitting M4 into a preliminary check at Y2Q2 (before evaluation runs are complete) with a formal gate at Y2Q3.

---

### 1.4 Year-4 Deliverable Overload — **HIGH**

**Problem:**  
Year 4 requires completing and releasing all of the following:  
- WP5-T2: Full transferability matrix (3+ models × 2+ embodiments × 4+ attack types) — computationally expensive  
- WP5-T3: Interpretability tool final validation  
- WP5-T4: VLA-SecBench v1.0 public release (documentation, dual-use review, GitHub/HuggingFace hosting)  
- WP5-T5: Benchmark paper submission (venue: ICRA/CoRL/USENIX)  
- D4.2: Transferability matrix paper  
- D4.4: Open-source toolkit (consolidated, with DUA)  
- D4.5: Final curriculum materials  
- Grant closeout and NSF final report  

This is 7–8 simultaneous output streams in a single year, alongside final robot experiments (Co-PI) and community workshops. For a team of PI + 1 grad + 1 undergrad (actual budget), Year 4 is over-committed by approximately 1–2 full person-years of effort.

**Concrete fix for Writer:**  
Move WP5-T3 (interpretability tool) final validation from Y4Q1 to **Y3Q4** and advance WP5-T5 to Y4Q2, freeing Y4Q3 for only toolkit release and paper revision. Explicitly note that D4.2 (transferability matrix paper) and D4.3 (T3 benchmark paper) are separate submissions; both cannot realistically be submitted in Y4Q3 by one PI. Mark one as primary and one as "submitted for review or preprint by grant close."

---

### 1.5 Quarter Assignment Review — Selected Tasks

| Task | Stated Timeline | Assessment |
|------|----------------|------------|
| WP0-T3 (compute setup) | Y1Q1 | FEASIBLE — must complete before WP0-T1 can run |
| WP0-T1 (fine-tune OpenVLA + Octo) | Y1Q1–Q2 | CONDITIONAL — depends on compute (see §3) |
| WP1-T1 (ABBP formalization) | Y1Q2 | FEASIBLE — PI-only theoretical work |
| WP1-T3 (TTDA on Octo) | Y1Q3–Q4 | FEASIBLE — Co-PI-led, parallel to ABBP |
| WP2-T3 (AGAT design) | Y1Q4–Y2Q1 | CONDITIONAL — AGAT implementation requires confirmed compute |
| WP5-T2 (full transferability matrix) | Y3Q4–Y4Q2 | TIGHT — 3 quarters for ≥3×2×4 experimental matrix + analysis |
| WP5-T4 (benchmark v1.0 release) | Y4Q2–Q3 | AT-RISK if WP5-T2 slips |
| WP5-T5 (T3 paper submission) | Y4Q3 | OVER-COMPRESSED with WP5-T4 in same quarter |

---

## 2. SCOPE FEASIBILITY

### 2.1 MVP (Years 1–2) — FEASIBLE WITH CONFIRMED COMPUTE AND CO-PI

The MVP scope (OpenVLA + Octo, Xarm7 + Simpler, 10+ tasks, ABBP + TTDA + 3 baselines, TACD + AGAT) is well-calibrated for two investigators over two years. The scope is **not over-engineered** at the MVP level. Concerns are primarily execution-gated (compute, Co-PI identity) rather than conceptual.

**Assessment:** Achievable if (a) compute is confirmed in Y1Q1–Q2 and (b) Co-PI is real and brings Xarm7 access. If either condition fails, the MVP collapses to a sim-only, single-PI effort, which is feasible but weakens the real-robot transferability claims central to the proposal.

---

### 2.2 Scale-Up (Years 3–4) — OVER-SCOPED WITHOUT CONFIRMED CO-PI AND HARDWARE — **HIGH**

**Problem:**  
Years 3–4 add:  
- pi-0 or equivalent flow-matching VLA (public availability not confirmed as of Aug 2026)  
- ACT (vision-only; no language — does not test multimodal coupling, weakening T2's core claim)  
- RT-2 via cloud API (requires API budget not in the current budget justification)  
- Franka or Spot (requires Co-PI institutional hardware — not confirmed)  
- Locomotion and navigation tasks (entirely new embodiment class requiring new data collection)  
- Tightly-coupled multimodal attacks (new research track, not piloted in Y1–2)  
- Physical adversarial patches on real robots  
- Randomized smoothing certified robustness  
- Full VLA-SecBench v1.0 + transferability matrix + interpretability tool  

On a single-PI + 1-grad budget with an unconfirmed Co-PI, Years 3–4 would require parallel execution of WP4 (new attack), WP5 (benchmark completion), WP2-T6 (extended defense), and WP6 (education) simultaneously. The plan itself estimates this was previously a "2–3 person, 6-year effort" — the Years 3–4 scope still resembles that.

**Concrete fix for Writer:**  
(a) Designate pi-0 availability as a **named contingency**: "If pi-0 or equivalent open flow-matching VLA is not available by Y3Q1, TTDA scale-up evaluates Octo-large (93M) and a fine-tuned diffusion-head variant as the third architectural family." (b) Remove ACT from the T2 multimodal coupling scope — ACT is vision-only and cannot be used to test visual-language coupling attacks. Replace ACT in the T2 scope with OpenVLA-OFT or a fine-tuned Octo variant with language conditioning. (c) Add explicit RT-2 API cost line to the budget.

---

### 2.3 Preliminary Experiment Metric Inconsistency — **MEDIUM**

**Problem:**  
`02_v2.tex` describes preliminary experiments (white-box and black-box attacks) using a 30%-action-deviation threshold as the attack success criterion. The research plan explicitly states this metric should be **replaced** by Task Success Rate (TSR) as the primary metric, with the 30%-deviation threshold retained only as a secondary physical-consequence proxy. However, the preliminary results figures (`fig:visual_white_box`, `fig:visual_black_box`) are labeled with the 30%-threshold metric. The proposal document will contain both a preliminary result section using the old metric and an evaluation section promising to replace it — reviewers will notice and question metric consistency.

**Concrete fix for Writer:**  
Add a single sentence in T1's evaluation plan (after the 30%-threshold figures) explaining: "In our preliminary experiments we operationalized attack success as a 30% action-token deviation proxy; in the full evaluation protocol (Part 4), we replace this with task success rate (TSR) as the primary metric and retain action deviation as a secondary physical-consequence proxy, for which we provide empirical justification in WP3-T1."

---

## 3. COMPUTE AND RESOURCE FEASIBILITY

### 3.1 GPU Budget vs. OpenVLA 7B White-Box Attacks — **HIGH**

**Problem:**  
The budget justification allocates **$12,500** for a single "GPU-equipped computer" as the sole hardware investment. This is consistent with a single high-end workstation (e.g., 2× RTX 4090 with 24 GB VRAM each, 48 GB total).

Running gradient-based white-box attacks (ABBP) on OpenVLA (7B parameters, LLaMA-2 backbone + dual ViT) requires:  
- Minimum memory for full-model inference + gradient storage: ~80–120 GB VRAM for a single forward-backward pass at batch size ≥ 1  
- PGD with K=10 steps requires K × that memory per perturbation step (or gradient checkpointing with ~3× time overhead)  
- AGAT adversarial fine-tuning: repeated PGD loops during training = 10–50× compute multiplier over standard fine-tuning  

A 2× RTX 4090 workstation cannot run end-to-end backprop through the full 7B model. The plan's own Risk Register (R1) acknowledges this and proposes NSF ACCESS allocation as a mitigation, but:  
- ACCESS allocations are not guaranteed and must be applied for competitively  
- The proposal does not budget time or funds for the ACCESS application  
- The fallback (white-box attacks on the visual encoder only, ~300–600M parameters) is viable but significantly narrows the ABBP claim: if gradient does not flow through the LLM action decoder, the "action-bin boundary" attack cannot directly optimize against the discrete bin assignment step

**Concrete fix for Writer:**  
State the compute plan explicitly in the proposal body (T1 subsection or a resource paragraph): "ABBP gradient-based evaluation targets the visual encoder components of OpenVLA (DINOv2 + SigLIP encoders, ~300M total parameters collectively) — a realistic threat model since these encoders are publicly released. Full-model backpropagation for AGAT uses LoRA-rank-16 fine-tuning (~25M trainable parameters), reducing per-step memory to ~20–30 GB and making AGAT compatible with a 2× A100 node on NSF ACCESS. We will apply for an ACCESS Explore allocation (standard application, no additional funding required) in Year 1, Quarter 1 as the first infrastructure milestone." Also add AGAT LoRA explicitly to the WP2-T3 task description.

---

### 3.2 RT-2 / Large-Model API Cost Not Budgeted — **MEDIUM**

**Problem:**  
RT-2 access requires cloud API calls (Google Cloud or third-party endpoint). The plan designates RT-2 for black-box evaluation in Years 3–4 with "cloud API budget for RT-2 / large model black-box queries (Year 3-4)" but no dollar amount appears in the budget justification. With ≥10 runs × ≥4 attack types × ≥4 tasks × query budgets of 500 per run, API costs could run $2,000–$10,000 or more.

**Concrete fix for Writer:**  
Add an "Other Direct Costs — Cloud Compute" line item to the budget justification for Year 3 and Year 4, estimated at $3,000–$5,000/year, with the notation "for black-box API evaluation of RT-2 and other proprietary VLAs." Adjust indirect cost calculation accordingly.

---

### 3.3 Simpler Benchmark Dependency — LOW RISK

The plan correctly identifies Simpler as the primary simulation platform. Simpler is open-source, actively maintained, and already used in preliminary experiments. No feasibility concern here.

---

## 4. TECHNICAL FEASIBILITY OF NOVEL CLAIMS

### 4.1 ABBP (Action-Bin Boundary Perturbation) — **MEDIUM RISK**

**Claim:** Adjacent action bins represent physically close but discretely different control signals; cross-bin perturbation requires less L∞ budget than equivalent disruption in language token spaces.

**Concern:**  
The underlying assumption — that uniform 256-bin discretization of a bounded action range creates an exploitable "semantic continuity" — is plausible but not obvious. Action bins are uniformly spaced within physical limits (e.g., Δpos_x ∈ [−0.05, 0.05] m mapped to 256 bins of ~0.4 mm resolution). A perturbation that crosses one bin boundary changes the predicted action by one bin width (~0.4 mm for the position dimension). Whether this is "lower L∞ budget than equivalent language token disruption" depends on the normalization: a language token change moves from one 32k-vocabulary token to another — an entirely different semantic unit — while a one-bin action shift is a tiny physical delta. The budget comparison is not apples-to-apples unless carefully normalized. Reviewers with adversarial ML expertise will press on this.

Additionally, the Jacobian constraint argument (simultaneous cross-bin perturbation across all 7 DOF for kinematic consistency) is novel but adds complexity to implementation (WP1-T1 requires formalizing this).

**Assessment:** ABBP is technically feasible to implement, but the claimed structural advantage over PGD is not obviously large. The plan appropriately gates this at M1 (formal analysis) and M3 (empirical test). The fallback (TTDA as primary novelty) is sound.

**No fix required at proposal-writing stage** beyond the M1 go/no-go language already in the plan. Ensure the formal analysis in WP1-T1 addresses the "L∞ budget comparison normalized to physical consequence" question explicitly.

---

### 4.2 TTDA (Temporal Trajectory Drift Attack) — **FEASIBLE, WITH CAVEAT**

**Claim:** Crafting slowly-accumulating perturbations across an action chunk that individually satisfy kinematic limits but collectively redirect the trajectory.

**Assessment:** This is technically sound. Octo's action chunking (predicting a sequence of K future actions jointly) creates genuine attack surface absent in single-output VLMs. The sufficient conditions for per-step detection bypass are characterizable via the trajectory prediction covariance (a per-step detector checks individual steps against learned thresholds; a drift attacker can stay within per-step bounds while the trajectory integral diverges).

**Caveat — pi-0 TTDA extension:**  
The plan extends TTDA to flow-matching models (pi-0) in Year 3. Flow-matching inference involves iterative denoising steps that are qualitatively different from autoregressive chunk prediction. The "denoising trajectory depth" framing is novel but requires separate theoretical treatment. Feasibility depends on pi-0 being available (see §2.2). The TTDA claim on Octo alone is solid; the pi-0 extension should be presented as exploratory in the proposal.

**Concrete fix for Writer:**  
In T1-1/T1-2 text, hedge the pi-0 TTDA extension: "We will extend TTDA to flow-matching policies (e.g., pi-0) in Years 3–4, where the denoising trajectory provides an analogous sequence structure; this extension is contingent on model availability and treated as a scale-up objective."

---

### 4.3 TACD (Temporal Action Consistency Detector) — **FEASIBLE, FP RISK IS REAL**

**Claim:** Sequence-level anomaly detection over full action chunks catches TTDA-style drift that per-step kinematic detectors miss.

**Assessment:** The conceptual distinction (step-level vs. sequence-level anomaly) is scientifically clean and novel. The main feasibility risk is the false-positive rate on real robots: legitimate task variability (grasp retries, near-miss trajectories, disturbance recovery) can produce sequences that look anomalous to a forecasting model trained on nominal demonstrations. The risk register correctly flags this as R4 (MEDIUM likelihood, MEDIUM impact).

**Concern not addressed in the plan:** The TACD trajectory forecasting model needs to be trained on per-task benign demonstrations. With ≥10 tasks and ≥2 embodiments, TACD requires separate forecasting models (or a multi-task shared model) for each task-embodiment pair. Training 20+ forecasting models adds significant infrastructure overhead to WP2-T1/T2 that is not explicitly scoped.

**Concrete fix for Writer:**  
Add to WP2-T1 task description: "TACD training uses a single multi-task trajectory forecasting model conditioned on task embedding, trained on all ≥10 tasks simultaneously to avoid per-task model proliferation. A per-task threshold is calibrated on held-out benign validation episodes."

---

### 4.4 AGAT (Action-Grounded Adversarial Fine-Tuning) — **FEASIBLE IF LORA IS USED**

**Assessment:** Standard PGD-based adversarial fine-tuning of a 7B model is computationally infeasible at the budget level. With LoRA (as recommended in §3.1 fix), AGAT becomes feasible. The conceptual novelty (kinematically-constrained perturbations as augmentation data) is sound and clearly distinct from standard adversarial training. Main risk is the robustness-accuracy tradeoff on downstream tasks — AGAT may reduce clean TSR more than expected. This is an empirical risk, not a theoretical one, and is appropriately handled by the M4 go/no-go framework.

---

### 4.5 Multimodal Tightly-Coupled Attack (T2) — **MEDIUM-HIGH RISK, Y3 START**

**Claim:** Visual and language perturbations co-reinforcing at the vision-language grounding layer achieve higher cross-embodiment transfer than independent attacks.

**Assessment:** The hypothesis is testable and the coupling mechanism (FiLM layers in OpenVLA/RT-1, Q-Former in other VLMs) is well-identified. However:

1. OpenVLA uses DINOv2 + SigLIP encoders with a projection head — the architecture is not FiLM-based. The plan incorrectly lists FiLM as one of the coupling targets for OpenVLA; FiLM is used in RT-1, not OpenVLA. The architectural analysis in WP4-T1 must be specific to the actual coupling mechanism in each model.
2. Octo and pi-0 have different grounding mechanisms (transformer cross-attention) than RT-1 (FiLM). A single "tightly-coupled" formulation may not generalize cleanly across the model zoo.
3. The T2 work is entirely in Year 3 (Y3Q1–Q4), which means it starts before Year-2 results from T1-T2 attacks have been published and peer-reviewed. Reviewers may ask why T2 coupling benefit is claimed before T1 baseline is established.

**Concrete fix for Writer:**  
In the T2 description, correct the FiLM attribution: "We target the vision-language coupling layer in each model (FiLM in RT-1, projection MLP in OpenVLA, cross-attention in Octo) and formulate a model-specific co-perturbation objective at each mechanism." Remove the generic "FiLM / Q-Former / dual ViT encoders" list from the multimodal attack description and replace with model-specific coupling targets.

---

## 5. GO/NO-GO GATES ASSESSMENT

### Existing Gates

| Milestone | Placement | Assessment |
|-----------|-----------|------------|
| M1 (Y1Q2): ABBP formal spec | Good — before major experimental investment | ADEQUATE |
| M2 (Y1Q3): MVP model zoo operational | Good — confirms reproducibility early | ADEQUATE |
| M3 (Y2Q1): ABBP vs. PGD results | Good — before paper writing begins | ADEQUATE; consider ≥15% threshold (current 10% is marginal) |
| M4 (Y2Q3): TACD detection/FP | Concurrent with WP2-T5 evaluation — too late | PROBLEM: split into preliminary check Y2Q2 |
| M5 (Y2Q4): VLA-SecBench v0.5 | Good — gates Year-3 scale-up | ADEQUATE |
| M6 (Y3Q2): Multimodal coupling benefit | Good — early in T2 work | ADEQUATE |
| M7 (Y4Q2): Benchmark ready for release | Good — includes dual-use review | ADEQUATE |

### Missing Gates — **HIGH/MEDIUM**

**Missing M0 — Compute Allocation (HIGH):**  
No milestone checks whether NSF ACCESS (or equivalent) allocation is secured. This is a prerequisite for WP0-T1 (OpenVLA fine-tuning) and all white-box evaluations. Without it, the entire attack pipeline degrades to encoder-only evaluation.  
**Add:** M0 at Y1Q1: "NSF ACCESS Explore allocation submitted and institutional GPU node operational. GO if either confirms ≥ 4 × A100 equivalent node access by end of Y1Q1; NO-GO: pivot to encoder-only white-box scope (explicitly stated in proposal) and submit ACCESS application immediately."

**Missing gate — Co-PI Confirmation (HIGH):**  
The plan explicitly marks the Co-PI as an assumption. There is no milestone checking Co-PI institutional confirmation before Year-1 real-robot work is assigned.  
**Add:** Pre-submission blocker (not a year milestone): "Co-PI confirmed with signed collaboration letter, institutional affiliation verified, and Xarm7 access documented before proposal submission."

**Missing gate — pi-0 Availability (MEDIUM):**  
Y3Q1 assumes pi-0 is available. No gate.  
**Add:** M at Y2Q4: "pi-0 or equivalent open flow-matching VLA confirmed available for research use. NO-GO: substitute Octo-large diffusion variant or distilled flow model; document substitution in progress report."

---

## 6. CONSISTENCY: BUDGET vs. PLAN

### 6.1 Year-1 Start Date Mismatch — **HIGH**

| Document | 4-Year Span |
|----------|-------------|
| `research_plan_timeline.md` | Sep 2027 – Aug 2031 |
| `budgetjustification_v2.tex` (grad student span) | Summer 2026 – Spring 2030 |
| **Gap** | **~15 months** |

The budget is internally consistent with an award starting ~June 2026 (standard NSF SaTC timeline for a proposal submitted in early 2026). The plan was generated with a Sep 2027 start that is almost certainly wrong. **The plan's dates must be corrected to match the budget** — not the reverse.

**Concrete fix for Writer:**  
Replace all Year 1–4 date labels in the plan and in any timeline figure with the corrected window (Sep 2026 – Aug 2030 or Jun 2026 – May 2030, whichever matches the intended submission date). All milestone quarters (M1 = Y1Q2 = Dec 2026–Feb 2027, etc.) shift accordingly.

---

### 6.2 Single-PI Budget vs. Two-Investigator Plan — **HIGH**

**Problem:**  
The budget justification lists:  
- Senior Personnel: PI (Mohammed Abuhamad) — 1 summer month/year  
- Graduate student: 1 student, Summer 2026–Spring 2030  
- Undergraduate: 1 student, 10 hr/week  
- **No Co-PI appears anywhere in the budget**  
- Total direct costs: $408,435. Total with indirect: $555,171

The plan is built around a two-investigator team (PI + Co-PI), with the Co-PI leading WP0 robot hardware, real-robot TTDA implementation, TACD testing, physical patch experiments, and scale-up embodiment integration. Approximately 35–40% of all deliverables are assigned as Co-PI primary leads.

At $555,171 total (single PI), the budget does not trigger the $600K Collaboration Plan requirement — consistent with having no Co-PI. If a Co-PI is added:  
- Total budget likely rises to $750K–$1.1M (depending on Co-PI salary, fringe, indirect rate)  
- The $600K threshold is exceeded; a **Collaboration Plan becomes required**  
- The total must remain under the RES cap ($1.2M total costs)

**The plan correctly flags this (§7 Collaboration Plan trigger and Pre-Submission Blockers)** but the Writer must not integrate the two-investigator structure into the proposal until the Co-PI identity, budget impact, and Collaboration Plan are resolved.

**Concrete fix for Writer:**  
Do not write "Co-PI" language into the proposal body until the PI has (a) identified the Co-PI, (b) recomputed the budget, and (c) confirmed whether the $600K threshold is crossed. In the interim, draft the research plan sections with "the research team" language, with placeholder [Co-PI: TBD] markers in the Division of Labor table. The timeline table should show parallel PI/Co-PI tracks but note the Co-PI as "to be confirmed."

---

### 6.3 Graduate Student Count Mismatch — **MEDIUM**

The budget has **1 graduate student**. The plan's Resource Requirements list **≥2 PhD students** ("1 led by PI [adversarial ML], 1 led by Co-PI [robotics]"). A single graduate student cannot execute both the ML-security track and the real-robot track in parallel. The scale-up scope in Years 3–4 is particularly at risk: WP5-T2 (full transferability matrix requiring simultaneous multi-embodiment runs) requires at minimum two concurrent experimental setups.

**Concrete fix for Writer:**  
If the budget remains single-PI, revise the Resource Requirements to state "1 PhD graduate student and 1 undergraduate RA." Acknowledge that the robotic infrastructure track relies on the Co-PI's own students. Mark the second-student resource requirement as Co-PI-institutional.

---

## 7. RISK SCORECARD

```yaml
Risk Scorecard:
  Timeline Feasibility:       6/10  # Q3/Q4 swap, year-start error, Y4 overload
  Scope Feasibility (MVP):    8/10  # Well-scoped; compute and Co-PI are external gates
  Scope Feasibility (Y3-4):   5/10  # pi-0 availability, ACT mismatch, overloaded final year
  Compute / Resource:         5/10  # Single $12.5K GPU incompatible with 7B white-box + AGAT
  ABBP Technical Soundness:   7/10  # Plausible; normalization argument needs hardening
  TTDA Technical Soundness:   8/10  # Structurally solid; pi-0 extension is speculative
  TACD Technical Soundness:   7/10  # Conceptually clean; FP risk acknowledged; multi-task overhead missing
  AGAT Technical Soundness:   6/10  # Infeasible without LoRA; LoRA not currently in the plan
  Multimodal Attack (T2):     6/10  # FiLM attribution error; model-specific coupling needed
  Go/No-Go Gate Coverage:     7/10  # 7 gates adequate; 3 critical gates missing
  Budget Consistency:         3/10  # No Co-PI in budget; year-start 15 months off; grad count mismatch
  Alignment (NSF SaTC 2.0):   8/10  # Strong program fit; staged scope directly addresses feasibility concern
```

---

## 8. REPAIR RECOMMENDATIONS (Priority-Ordered)

### HIGH Priority

**H1 — Fix calendar year-start and quarter labels before any proposal integration**  
- Issue: Plan year-start (Sep 2027) contradicts budget (Summer 2026). Q3/Q4 labels swapped.  
- Fix: Set Year 1 = Sep 2026–Aug 2027; relabel Q3 = Mar–May, Q4 = Jun–Aug throughout all 17 parts of the plan.  
- Impact: Every milestone date, deliverable year, and timeline figure becomes coherent.  
- Expected Benefit: Prevents a timeline figure that contradicts the budget period.

**H2 — Resolve Co-PI identity before writing the research plan section**  
- Issue: Budget has no Co-PI; plan assigns ~40% of effort to an unconfirmed Co-PI.  
- Fix: PI must identify Co-PI, add to budget, recompute to confirm $600K threshold status, and prepare Collaboration Plan if needed. Writer should use "research team" placeholders until resolved.  
- Impact: Determines whether Collaboration Plan is required; determines whether Year-3 robot scale-up is feasible.

**H3 — State explicit compute plan in the proposal (LoRA + ACCESS)**  
- Issue: $12,500 GPU budget cannot run OpenVLA 7B white-box attacks or AGAT fine-tuning.  
- Fix: Add to proposal: (a) ABBP targets ViT encoders only (realistic threat model); (b) AGAT uses LoRA rank-16 fine-tuning (~25M parameters); (c) NSF ACCESS Explore allocation submitted Y1Q1.  
- Impact: Makes compute plan credible to technical reviewers; avoids reviewer objection on resource realism.

**H4 — Add Missing Go/No-Go Gate M0 (Compute Confirmation)**  
- Issue: No milestone checks whether compute is available before WP0-T1 (fine-tune OpenVLA 7B).  
- Fix: Insert M0 at Y1Q1: "Compute allocation confirmed (ACCESS or local). NO-GO: scope white-box evaluation to encoder-only; document explicitly."  
- Impact: Protects entire critical path from silent failure.

**H5 — Reduce Year-4 simultaneous deliverable count**  
- Issue: 7–8 output streams in Year 4 for a team of PI + 1 grad.  
- Fix: Move WP5-T3 (interpretability tool) to Y3Q4; de-prioritize D4.2 vs. D4.3 (mark one as "preprint by grant close"); advance WP5-T5 to Y4Q2.  
- Impact: Makes Year 4 feasible without dropping any science.

---

### MEDIUM Priority

**M1 — Fix FiLM/coupling layer attribution in T2 multimodal attack description**  
- Issue: Plan lists FiLM as a coupling target for OpenVLA, which uses projection MLP, not FiLM.  
- Fix: Replace generic "FiLM/Q-Former/dual ViT" list with model-specific coupling targets: FiLM (RT-1), projection MLP (OpenVLA), cross-attention (Octo).  
- Impact: Prevents reviewer correction on architectural knowledge.

**M2 — Add LoRA specification to AGAT task (WP2-T3)**  
- Issue: AGAT as stated requires full-model backprop on 7B — infeasible at budget.  
- Fix: Add "AGAT implements LoRA-based adversarial fine-tuning (rank 16, targeting query/value matrices in LLM backbone)" to WP2-T3 deliverable description.  
- Impact: Makes AGAT technically credible without requiring hardware upgrade.

**M3 — Split M4 into preliminary check (Y2Q2) and formal gate (Y2Q3)**  
- Issue: TACD go/no-go and defense paper evaluation run are scheduled simultaneously.  
- Fix: Add preliminary TACD FP characterization milestone at Y2Q2: if FP >20%, redesign threshold strategy before full WP2-T5 evaluation runs begin.  
- Impact: Creates recovery buffer before defense paper deadline.

**M4 — Add metric consistency note bridging preliminary 30%-threshold and TSR**  
- Issue: 02_v2.tex uses 30%-deviation threshold in preliminary results; plan replaces it with TSR.  
- Fix: Add one bridging sentence in T1's evaluation plan section of the proposal.  
- Impact: Prevents reviewer confusion about metric discontinuity.

**M5 — Add explicit RT-2 API cost line to budget**  
- Issue: Cloud API evaluation costs not budgeted.  
- Fix: Add $3,000–$5,000/year in Other Direct Costs for Years 3–4.  
- Impact: Prevents an NSF budget question post-award.

**M6 — Remove ACT from T2 multimodal coupling scope; substitute language-conditioned model**  
- Issue: ACT is vision-only — cannot test visual-language coupling.  
- Fix: Replace ACT in T2 scope with OpenVLA-OFT or language-conditioned Octo variant.  
- Impact: T2 claim becomes internally consistent.

---

### LOW Priority

**L1 — Hedge pi-0 TTDA extension as exploratory**  
- Fix: Add "contingent on model availability; treated as scale-up objective" to T1-3 pi-0 language.

**L2 — Add multi-task TACD training specification to WP2-T1**  
- Fix: Specify single multi-task trajectory forecasting model with per-task threshold calibration.

**L3 — Clarify M3 go/no-go threshold (consider ≥15% over PGD instead of ≥10%)**  
- Fix: A marginal 11% improvement would pass M3 but produce a weak contribution framing; raise threshold.

---

## 9. Advancement Decision

```yaml
Decision: FEASIBLE-WITH-FIXES

Rationale: >
  The science is credible and the staged MVP/scale-up structure is a genuine improvement
  over the original panel-rejected scope. However, three structural inconsistencies
  (budget year-start mismatch, no Co-PI in budget, calendar quarter swap) must be
  corrected before any prose is written from this plan — they are not science problems
  but document-integration bombs that will produce internal contradictions in the proposal.
  The compute plan gap (7B model on $12.5K GPU) and the Year-4 overload are solvable
  with minimal scope adjustment (LoRA + ACCESS + 1 deliverable re-ordering). None of the
  novel technical claims (ABBP, TTDA, TACD, AGAT) are technically unsound; they carry
  medium risk that is well-managed by the existing go/no-go gate structure, provided the
  three missing gates (M0 compute, Co-PI confirmation, pi-0 availability) are added.

  The proposal should NOT be written until H1, H2, and H3 are resolved.
  Once those are resolved, the Writer can integrate the plan; the remaining MEDIUM fixes
  can be applied during the writing pass.
```

---

*Feasibility Audit produced by Auditor Agent, 2026-08-31. All findings are based on the documents listed in the header. No research results are fabricated. Priority labels (HIGH/MEDIUM/LOW) reflect risk to proposal fundability, not scientific interest.*
