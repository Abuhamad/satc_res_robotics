# NSF SaTC 2.0 (NSF 25-515) RES Panel Review

**Proposal Title:** "SaTC 2.0: RES: Toward Secure and Robust Generalist Robotic Models"  
**PI:** Mohammed Abuhamad, Loyola University Chicago  
**Program:** Trustworthy Computing & Information Security (SaTC 2.0)  
**Review Date:** August 31, 2026  
**Panel Assignment:** Research Experiences for Undergraduates (RES) / Secure and Trustworthy Robotics

---

## Executive Summary

This proposal addresses an emerging and timely problem: the security and trustworthiness of generalist Vision-Language-Action (VLA) robotic foundation models. The work proposes a comprehensive security framework across three tasks: (T0) building a multi-embodiment dataset repository, (T1) systematic vulnerability analysis via white/gray/black-box attacks, (T2) multimodal attack propagation, and (T3) safety benchmarks and interpretability. The proposal includes preliminary attack results on 4 VLA models (RT-1, RT-2, Octo, ACT) across 6 robots and 15 datasets, plus a novel robotics-specific defense mechanism based on action-space anomaly detection. While the scope and timeliness are commendable, significant concerns about technical novelty, evaluation rigor, feasibility of a 4-year single-PI effort, and clarity of threat models temper enthusiasm.

---

## 1. Intellectual Merit

### 1.1 Strengths

1. **Timely and Important Problem:** VLA models are rapidly entering deployment across industrial and service robotics. Security hardening at this foundational stage is strategically valuable and rare in the literature. The proposal positions itself as the first comprehensive security framework for end-to-end robotic policies.

2. **Comprehensive Threat Taxonomy:** Table 1 (attack taxonomy spanning evasion, poisoning, privacy, abuse; across training/inference; white/gray/black-box; multiple targets) is well-structured and provides clear categorization. The formal notation $\mathcal{M}(\{\mathbf{x}\}, \{\mathbf{t}\}, \{\mathbf{s}\})$ rigorously frames the threat space.

3. **Multi-Embodiment, Multi-Model Evaluation Plan:** 6 robots, 15 datasets, 5+ VLA models (RT-1, RT-2, Octo, ACT, OpenVLA) demonstrates breadth. This specificity raises the credibility of generalizability claims compared to single-model robotics security work.

4. **Concrete Preliminary Results:** White-box and black-box attack demonstrations show non-trivial success rates (white-box success rates vary by model/task; black-box token perturbations degrade performance significantly). These ground the proposal in evidence rather than speculation.

5. **Action-Space Anomaly Detection:** A novel robotics-specific defense unavailable to general VLMs (detects kinematically implausible actions, joint limits, workspace violations) that complements input-side defenses and remains effective when compromised modality is unknown.

6. **Educational Integration:** Explicit commitment to curriculum development, labs, workshops, and student engagement aligns well with SaTC program values and provides broader impact beyond research.

### 1.2 Weaknesses

#### Critical Weakness #1: Limited Attack Novelty; Over-Reliance on Ported Methods

**Issue:** The core attack methods—PGD, FGSM, C&W (white-box), prompt injection/jailbreak (gray/black-box)—are well-established from vision and LLM security literature. Robotic-specific adaptations exist (e.g., trajectory-level attacks, kinematic constraints) but are cited as future comparisons, not core contributions.

- White-box attacks: Standard gradient-based methods applied to visual encoders (EfficientNet-B3, ViT).
- Gray-box attacks: Surrogate-model transfer from CLIP/BLIP alignment.
- Black-box attacks: Token deletion/replacement/random perturbation is straightforward and shows limited sophistication.

**Concern:** This feels like an engineering/systems contribution—systematically applying known attacks to a new domain—rather than algorithmic innovation. For NSF SaTC RES, a single-PI proposal must compensate with exceptional execution, evaluation rigor, or theoretical insight. None are evident.

**Actionable Fix:**
- Develop attack methods that exploit multimodal VLA-specific properties not present in VLMs (e.g., temporal action consistency, kinematic coordination constraints, embodiment-specific action token adjacency). Demonstrate these outperform naive port-overs.
- Provide formal analysis of why robotic action quantization (discrete bins) creates vulnerabilities distinct from language tokenization.

---

#### Critical Weakness #2: Action-Space Anomaly Detection Insufficient as Core Defense

**Issue:** While novel to robotics, the proposed defense is more of a *safety filter* than a *security mechanism*:

1. **Bounded but valid attacks:** Adversarial examples can be crafted to satisfy kinematic constraints (workspace, joint limits, safety zones) and still cause harm (e.g., unsafe grasping, unstable manipulation, incorrect task execution).
2. **False negatives:** Preliminary results lack any demonstration of anomaly detector effectiveness. What is the false-positive rate? Can attackers adapt by learning valid action boundaries?
3. **Not a defense against all attack classes:** Ineffective against poisoning (training-time) or privacy attacks. Handles only inference-time evasion.
4. **Incomplete specification:** Threshold tuning for workspace/joint limits not detailed. Robustness to adversarial domain shift (e.g., when physical constraints change) not addressed.

**Concern:** The proposal claims this is a major technical contribution justifying the research scope, but no preliminary evaluation shows it actually stops attacks. Without evidence, this reads as a strawman defense.

**Actionable Fix:**
- Conduct preliminary adversarial robustness evaluation: Generate white-box adversarial examples constrained to the valid action space. Report detection rates and false-positive rates.
- Compare anomaly detection to baseline defenses (e.g., input smoothing, ensemble voting, certified defenses). Show relative advantage.
- Extend detector to catch subtle behavioral anomalies (e.g., predicted actions that are kinematically valid but contradict task intent) using auxiliary task classifiers or causal models.

---

#### Critical Weakness #3: Evaluation Rigor and Generalizability Gaps

**Issue:** Preliminary results raise more questions than answers:

1. **Arbitrary Success Metrics:** 30% action deviation threshold lacks justification. What physical consequence maps to this threshold? Why not use task success rate as primary metric?
2. **Limited Experimental Scope:** 3 simulation + 3 real tasks (Close Drawer, Pick Coke Can, Stack Cubes, etc.). These are basic manipulation tasks. What about locomotion, navigation, or complex multi-step reasoning?
3. **No Transferability Analysis:** Do attacks on RT-1 transfer to Octo or OpenVLA? Are black-box attacks transferable across models? The proposal mentions this but provides zero data.
4. **Baseline Defenses Missing:** No comparison to input smoothing, JPEG compression, adversarial training, or ensemble methods. Without baselines, impossible to assess whether proposed defenses are state-of-the-art.
5. **Closed-Model Evaluation Challenges:** RT-2 (55B PaLM-E) and proprietary OpenVLA variants may not be available for detailed white-box evaluation. How are results grounded in reality?
6. **Statistical Rigor:** Preliminary results show single runs or 5 runs with single random seed reported. No confidence intervals, significance tests, or multiple-run aggregation visible.

**Concern:** A 4-year NSF RES grant demands rigorous, reproducible evaluation. Current preliminary work doesn't meet this bar.

**Actionable Fix:**
- Expand evaluation to 10+ tasks spanning manipulation, locomotion, and navigation with diverse embodiments.
- Report primary metric as task success rate under attack (binary), secondary metrics as action deviation and physical-consequence proxies (safety violations, end-effector displacement).
- Conduct full transferability matrix: $M_i$ models $\times$ $T_j$ tasks $\times$ Attack $A_k$ methods.
- Compare all proposed defenses to 3+ baseline defenses; report Pareto frontier of robustness vs. computational cost.
- Run all experiments 10+ times, report mean ± std, perform statistical significance testing (e.g., Welch's t-test).

---

#### Weakness #4: Scope vs. Single-PI Feasibility Over 4 Years

**Issue:** The proposal spans an ambitious scope:

- **Data Management (T0):** Integrating 15 datasets, training/maintaining 5+ VLA models across 6 embodiments.
- **Attack Development (T1):** Implementing white/gray/black-box evasion, poisoning, privacy, and abuse attacks (~12-15 attack types from Table 1).
- **Defense Development (T1, T2, T3):** Multiple inference/training-time defenses, anomaly detection, interpretability methods.
- **Real Robot Experiments:** Executing attacks/defenses on physical Xarm7, Franka, Spot, etc.
- **Educational Output:** Curriculum development, workshops, student training.

**Constraints:**
- **Single PI at Loyola University Chicago:** Limited graduate student availability, modest computational infrastructure, no existing robotics lab described.
- **Cost and Logistics:** Real-robot experiments are expensive. Maintaining 6 robot platforms, 15 datasets, cloud inference for large VLAs (RT-2 55B requires cloud or expensive GPU) is resource-intensive.
- **Timeline Pressure:** Realistic estimate for quality execution of T1 alone is 2-3 years (attack development, evaluation, responsible disclosure). T2 and T3 cannot fully parallelize.

**Concern:** This reads as a 2-3 person, 6-year effort, not a single-PI, 4-year RES project. Over-commitment risks.

**Actionable Fix:**
- Sharpen scope: Focus on T1 (vulnerability analysis) and T3 (safety/interpretability). Defer comprehensive multimodal attacks (T2) to future work or position as a postdoc/PhD extension.
- Prioritize 2-3 embodiments (e.g., Franka, Xarm7, Spot) and 3-4 VLA models. Show depth, not breadth.
- Leverage cloud APIs for inference; focus on attack/defense logic, not model deployment infrastructure.
- Explicitly bound real-robot experiments to 20-30 hours per year per embodiment to manage cost/logistics.
- Hire a postdoc or fund 1-2 PhD students explicitly (not implicit in RES budget) to handle real-robot work.

---

#### Weakness #5: Threat Model and Trust Definition Lack Clarity

**Issue:** The proposal frames trust as "assurance that a robotic foundation model produces safe, intended physical actions under both benign and adversarial multimodal inputs." This is circular:

1. **What constitutes "intended"?** Defined by task specification, human operator, pre-trained prior? Proposal doesn't say.
2. **Threat Model Undefined:** Who has access to the model? (Cloud API with rate-limiting? Local inference? On-device?) Which threat scenarios are in-scope? (Insider data poisoning during training? Inference-time API jailbreaking? Physical sensor attacks?) Proposal conflates all.
3. **Trustworthiness vs. Robustness:** Trust in ML systems typically involves fairness, explainability, reproducibility, safety margins, and privacy. This proposal focuses narrowly on adversarial robustness. Are other trust dimensions in or out of scope?
4. **Inherited Vulnerabilities:** The claim that VLA models "inherit" vulnerabilities from vision and language backbones is asserted but not rigorously defined. Which vulnerabilities transfer? Which are neutralized by task structure?

**Concern:** Without clear threat models, evaluation claims lack grounding. "We defend against unknown attacks" is not scientifically testable.

**Actionable Fix:**
- Define explicit threat actors and scenarios: (a) Adversary with white-box access (insider threat), (b) Adversary with black-box API access (external), (c) Adversary controlling training data (supply-chain attack), (d) Adversary controlling sensor inputs (physical attack). For each, specify attack goals (cause task failure vs. cause specific harmful action).
- Define trust operationally as a vector: Robustness to white/gray/black-box attacks; Interpretability of predictions; Explainability of failures; Safety margin (actions avoid harm by $k$ sigma); Fairness (no task/embodiment bias). Report progress on each.
- Distinguish this SaTC work from generic robustness: Connect results to trustworthiness criteria (e.g., "A robot is trustworthy if it passes safety benchmarks $B_1, B_2, B_3$ with $\geq 95\%$ success and recovers from adversarial inputs within 2 timesteps").

---

## 2. Broader Impacts

### Strengths

1. **Public Safety & Acceptance:** Hardening VLA models improves public confidence in robotic deployment in shared human-robot spaces (logistics, healthcare, manufacturing).
2. **Educational Pathways:** Explicit curriculum development, high-school/undergraduate labs, and mentoring create workforce development pipeline in secure AI/robotics.
3. **Open-Source Community Resources:** Promised attack/defense tools, benchmarks, and datasets lower barriers to entry for other researchers.
4. **Interdisciplinary Bridge:** Connecting AI security, robotics, and cybersecurity communities is valuable.

### Weaknesses

1. **Dual-Use Concerns Minimized:** While responsible disclosure is mentioned ("offensive analysis serves solely to build defenses"), there is minimal discussion of how released attack tooling will be gated to prevent misuse. What governance model ensures tools don't enable weaponized robots or autonomous harm?

2. **Generalizability Claims Overstated:** Proposal claims methodologies "extend beyond robotics and benefit adjacent domains (security of AI/multimodal models)" but provides no evidence. How does robotics-specific action-space anomaly detection generalize to autonomous vehicles, medical AI, or other multimodal systems?

3. **Equity and Access:** Benchmarks and tools will likely be available to well-resourced researchers with access to VLA models and robot hardware. Does this widen or narrow the gap for institutions with limited resources?

4. **No Discussion of Long-Term Impact:** What happens when VLA architectures evolve in 2-3 years? Do defenses remain relevant? Proposal should address how to maintain/update benchmarks.

---

## 3. SaTC 2.0 Specific Criteria

### 3.1 Clarity of Trust Definition

**Score: Fair**

- Proposal defines trust narrowly as adversarial robustness; doesn't engage with broader trustworthiness dimensions (fairness, interpretability, privacy).
- Definition is goal-circular ("safe, intended actions") without operational grounding.
- **Recommendation:** Expand trust framework to align with NIST AI Risk Management Framework.

### 3.2 Concreteness of Threat Model

**Score: Fair-to-Good**

- Table 1 provides concrete attack taxonomy (evasion, poisoning, privacy, abuse; white/gray/black-box; training/inference).
- However, deployment threat scenarios are underspecified. Are threats from insider training-time attacks or external inference-time attacks the priority?
- Doesn't clearly distinguish between attacks on open-source models (e.g., OpenVLA) vs. commercial APIs.

**Recommendation:** Map threat model to realistic deployment scenarios (e.g., "autonomous warehouse picker defended against supply-chain backdoor injections" vs. "home robot defended against jailbreak via user-provided instructions").

### 3.3 Generalizable Security Science (Not Single-Platform)

**Score: Good**

- Multi-embodiment, multi-model evaluation (6 robots, 5 VLA architectures, 15 datasets) shows effort to generalize beyond one platform.
- However, all tested models share similar architectural patterns (vision encoder + LLM/VLM + action decoder). Generalizability to radically different architectures (e.g., RL-based policies, differentiable physics models) unclear.

**Recommendation:** Include at least one non-transformer-based model (e.g., CNN-LSTM) to test robustness of generalizations.

### 3.4 Evaluation Rigor and Reproducibility

**Score: Fair**

- Preliminary results are limited in scope (3 simulation + 3 real tasks, no baselines, no transferability analysis).
- Closed-source models (RT-2 via proprietary partners) may hinder reproducibility.
- Promised open-source implementation, but no timeline or commitment level.

**Recommendation:** 
- Commit to reproducibility standard: "All experiments reproducible on publicly available models (OpenVLA, Octo) and Simpler sim benchmark by end of Year 2."
- Pre-register experiment protocol with OSF (Open Science Framework).

### 3.5 Responsible Computing & Dual-Use Mitigation

**Score: Fair**

- Proposal mentions "responsible-disclosure practices" and gates for attack tools but lacks detail.
- No discussion of how to prevent attackers from using released tools to harm robots.
- No ethics review or institutional oversight mechanism described.

**Recommendation:**
- Define gating policy explicitly: e.g., "Attack code released only to researchers with institutional affiliation and under Data Use Agreement; no public release until 12 months after publication."
- Engage ethics board or responsible AI committee for guidance on dual-use mitigation.

### 3.6 Scope vs. Investment (4-Year Single-PI Budget)

**Score: Poor**

- Scope (T0-T3 across 5+ models, 6 embodiments, 15 datasets) is 2-3× larger than feasible for single-PI, 4-year effort.
- Budget not provided, but robotics infrastructure (6 robots, cloud compute, graduate students) likely exceeds typical NSF SaTC RES budget (~$200K-350K over 4 years).
- Real-robot experiments are logistics-heavy; few single-PI labs can sustain 6 platforms over 4 years.

**Recommendation:** Dramatically scope-down or request additional co-PI support (e.g., collaboration with Google Robotics, CMU, UC Berkeley for platform access).

---

## 4. Reviewer Assessment: Strengths & Weaknesses Summary

### Strengths

1. **Timeliness:** VLA security is underexplored and urgent as models enter production.
2. **Comprehensive Taxonomy:** Well-structured attack categorization and threat model.
3. **Preliminary Evidence:** Demonstrates non-trivial vulnerabilities in real models.
4. **Robotics-Specific Defense:** Action-space anomaly detection is novel (though underevaluated).
5. **Multi-Embodiment Scope:** Ambitious breadth increases credibility of generalizability.

### Weaknesses

1. **Limited Algorithmic Novelty:** Attacks are ports from VLM/LLM security; defenses are engineering adaptations.
2. **Action-Space Anomaly Detection Unvalidated:** No evidence it stops attacks; insufficient as core contribution.
3. **Evaluation Gaps:** Narrow task scope, missing baselines, no transferability analysis, arbitrary success metrics.
4. **Feasibility Concerns:** Scope exceeds single-PI 4-year effort; underestimates robotics infrastructure demands.
5. **Threat Model Ambiguity:** Unclear which threat scenarios are priority; trust definition is circular.
6. **Reproducibility Risk:** Dependence on closed-source models; limited detail on open-source commitment.

---

## 5. Top 5 Weaknesses & Actionable Fixes

### Weakness #1: Insufficient Technical Novelty in Attack Methods

**Severity: High**

**Current State:** Attacks are direct ports from vision/LLM literature without exploiting VLA-specific structure.

**Actionable Fix:**
1. Develop attacks that exploit action tokenization and temporal consistency (e.g., attacks that target action token adjacency or temporal causal relations).
2. Analyze mathematical properties of action space (discrete bins, kinematic constraints) that enable novel attack surfaces.
3. Demonstrate $\geq 20\%$ improvement over naive port-overs on attack success rate or imperceptibility.
4. Publish attack methodology as distinct contribution before benchmark results.

**Success Metric:** By Year 1.5, submit at least one paper introducing VLA-specific attack algorithms to a top-tier venue (e.g., USENIX Security, CCS).

---

### Weakness #2: Action-Space Anomaly Detection Lacks Preliminary Evidence

**Severity: High**

**Current State:** Proposed as core defense but zero preliminary results shown.

**Actionable Fix:**
1. Conduct white-box attack experiments with detector enabled. Report:
   - Detection rate (% of attacks caught before execution)
   - False-positive rate (% of benign actions flagged)
   - Pareto frontier: Detection rate vs. false-positive rate as threshold varies
2. Compare to baselines: input smoothing, adversarial training, ensemble averaging.
3. Test on at least 2 embodiments × 2 models.
4. Publish detector design and evaluation as a methods paper by Year 1.

**Success Metric:** Demonstrate detector catches ≥70% of white-box attacks with ≤5% false-positive rate by Year 1.

---

### Weakness #3: Evaluation Scope Too Narrow; Missing Baselines & Transferability

**Severity: High**

**Current State:** 3-6 tasks, no baseline defenses, no transferability analysis, 30% success threshold unjustified.

**Actionable Fix:**
1. Expand evaluation suite to ≥10 tasks spanning manipulation (grasping, placing, insertion), locomotion (navigation, climbing), and complex reasoning.
2. Implement 3-5 baseline defenses: input smoothing (Gaussian blur, JPEG compression), adversarial training, ensemble voting, certified defenses (randomized smoothing).
3. Conduct full transferability study:
   - Train attacks on model $M_1$, test on $M_2, M_3, \ldots$ (all model pairs).
   - Report transfer success rate matrix.
4. Define success metric operationally: "Attack succeeds if task completion rate drops ≥20% or safety zone is violated ≥1 time per 100 steps."
5. Run all experiments 10+ times, report mean ± std, perform Welch's t-tests for significance.

**Success Metric:** By Year 2, produce comprehensive benchmark paper with results on 10+ tasks, 5+ models, 5+ defenses, full transferability matrix.

---

### Weakness #4: Feasibility & Scope Over-Commitment

**Severity: Medium-High**

**Current State:** Ambitious scope (T0-T3, 6 robots, 5 models, 15 datasets) infeasible for single-PI 4-year effort.

**Actionable Fix:**
1. **Prioritize:** Focus on T1 (vulnerability analysis) as core contribution. Relegate T2 (multimodal) to secondary/exploratory work. Position T3 (safety/interpretability) as preliminary benchmarks, not full evaluation.
2. **Narrow embodiments:** Target 2-3 platforms (e.g., Franka Emika, Xarm7) with publicly available models. Use simulation (Simpler, Isaac Sim) for breadth instead of real robots.
3. **Model selection:** Commit to OpenVLA and Octo (open-source, reproducible). Use RT-2 only if cloud API access is secured; do not rely on local reproduction.
4. **Budget real-robot time:** Max 30 hours/year per embodiment; focus on high-impact scenarios (e.g., 5 attack types × 6 tasks).
5. **Hire support:** Request funding for 1 postdoc (attack methods) and 2 PhD students (evaluation, real robots), not just REU students. Clarify that "single-PI" effort includes advisor mentorship, not solo execution.

**Success Metric:** By Year 1, publish detailed work plan and timeline showing feasible milestones for each PI effort-allocation.

---

### Weakness #5: Threat Model & Trust Definition Lack Operational Grounding

**Severity: Medium**

**Current State:** Trust defined circularly; threat actors/scenarios underspecified; SaTC-specific criteria unclear.

**Actionable Fix:**
1. Define explicit threat actor profiles:
   - **Insider (white-box):** Disgruntled ML engineer with model code.
   - **External API (black-box):** Unauthorized user with limited query budget.
   - **Supply-chain:** Attacker can inject backdoors during training data collection.
   - **Physical (sensor):** Attacker can modify camera input or sensory readings.
2. For each actor, specify attack goals: (a) Cause task failure, (b) Cause specific harmful action, (c) Extract proprietary data, (d) Corrupt trajectory.
3. Define trustworthiness evaluation protocol: Robot is trustworthy if it (1) Resists attacks with <5% success rate, (2) Recovers gracefully (returns to safe state within 1 second), (3) Logs intrusions for audit, (4) Explains decisions to human operators (interpretability).
4. Map each task (T0-T3) to trustworthiness criteria; show causal link.
5. Align with SaTC program outcomes: "This work advances understanding of [which] trustworthiness dimensions in [robotics domain]?"

**Success Metric:** By proposal revision, include detailed threat model taxonomy (≥3 actor types × ≥4 goals × ≥3 capabilities levels) with explicit in/out-of-scope definitions.

---

## 6. Decision & Rating

### Summary Rationale

The proposal tackles an important and timely problem: security of generalist VLA robotic models. The comprehensive threat taxonomy and multi-embodiment evaluation scope are commendable. However, the technical contributions are primarily incremental—adapting known VLM attack methods to robotics without deep algorithmic innovation. The proposed core defense (action-space anomaly detection) lacks any preliminary evidence of effectiveness and appears to be a safety filter rather than a true security mechanism. Evaluation rigor is weak (narrow task scope, missing baselines, no transferability analysis), and the project scope dramatically exceeds what is feasible for a single-PI, 4-year RES grant, especially when accounting for robotics infrastructure demands. The threat model is ambiguous, and trustworthiness claims lack operational grounding.

While the work would likely produce useful datasets and benchmarks, it falls short of the technical rigor and novelty expected for competitive NSF SaTC funding. The proposal reads as an engineering systems integration effort ("apply attacks A1-A12 to models M1-M5 on robots R1-R6") rather than advancing fundamental security science in robotics.

### Rating

**Overall Rating: GOOD (3/5)**

- **Intellectual Merit:** GOOD (3/5) — Timely and comprehensive scope, but limited algorithmic novelty; defenses underdeveloped.
- **Broader Impacts:** GOOD (3/5) — Educational components strong; dual-use concerns minimized.
- **SaTC Alignment:** FAIR-TO-GOOD (2.5/5) — Threat model and trust definition need refinement; scope-to-resources misaligned.

### Funding Recommendation

**BORDERLINE / NOT COMPETITIVE for RES at current form**

**Detailed Justification:**

This proposal sits at the boundary. If funded, it would likely produce useful artifacts (benchmarks, datasets, open-source tools) and contribute to nascent VLA security literature. However, it does not rise to **Highly Competitive** or **Competitive** status due to:

1. **Limited Novelty:** Attacks are adaptations of existing methods; defenses are engineering refinements. No breakthrough insight.
2. **Evaluation Gaps:** Preliminary work is too narrow to support ambitious claims about generalizability.
3. **Feasibility Risk:** Over-committed scope and single-PI model suggest execution risk; deadline pressure may force shortcuts.
4. **Clarity Issues:** Threat model, trust definition, and core technical innovation need clearer articulation.

**Funding Level (if favorably reviewed):** If revised to sharpen scope and strengthen preliminary results, could merit funding at **$150K-200K over 3 years** (reduced from typical 4-year RES budget) with explicit co-PI support or partnerships for real-robot access.

---

## 7. Improvement Pressure Test: What Would Make This Competitive?

### Required Changes for Acceptance

1. **Demonstrate Novel Attack Method(s):** Show that VLA-specific attacks (exploiting action tokenization, temporal consistency, kinematic constraints) outperform naive VLM ports by ≥25% in efficiency or success rate. Publish as methods paper.

2. **Validate Action-Space Anomaly Detector:** Provide preliminary evidence (on ≥100 white-box attacks) that detector catches ≥70% of attacks with ≤5% false-positive rate. Compare to 2-3 baseline defenses.

3. **Expand Evaluation Rigor:** Conduct experiments on ≥10 tasks, ≥4 models, ≥4 defenses. Report full transferability matrix. Use task success rate as primary metric; justify all thresholds.

4. **Scope Reduction:** Explicitly narrow to T1 (vulnerability analysis) and T3 (safety/interpretability). Defer T2 (multimodal attacks) to Phase 2 or postdoc project.

5. **Clarify Threat Model:** Define 3-4 specific threat actors with explicit attack goals. Map each defense to threat(s) it mitigates.

6. **Feasibility Plan:** Provide detailed timeline and resource allocation showing how all tasks fit within single-PI 4-year effort. Identify partnerships or co-PI support for real-robot access.

7. **SaTC Alignment:** Explicitly connect findings to SaTC program outcomes (e.g., "This work advances understanding of certification mechanisms for trustworthy AI in cyber-physical systems").

### Impact of Changes

If all changes implemented:

- **Rating upgrade:** GOOD → VERY GOOD (4/5)
- **Funding recommendation upgrade:** BORDERLINE → COMPETITIVE (potentially fundable)
- **Estimated probability of funding:** 30-40% (with strong reviews from other panelists)

---

## 8. Meta-Assessment: Reviewer Sentiment

| Dimension | Level | Comment |
|-----------|-------|---------|
| **Enthusiasm** | Medium | Problem is timely; execution concerns dampen enthusiasm. |
| **Confidence** | Medium-High | Confident in assessment of novelty gaps and feasibility risks; less certain about potential with revisions. |
| **Funding Likelihood** | Low-to-Medium | 25-35% chance of funding at major NSF program; higher (40-50%) if NSF opens robotics-specific security track. |

---

## 9. Reviewer Questions for Rebuttal

1. **On Technical Novelty:** Can you articulate 2-3 algorithmic innovations specific to VLA security that are not present in prior VLM security work? What is the fundamental difference between attacking a VLM and attacking a VLA?

2. **On Anomaly Detector:** What percentage of adversarially crafted actions satisfy your kinematic constraints? If >80%, how is the detector doing more than checking physics feasibility? Early preliminary results (even negative results) would clarify scope.

3. **On Feasibility:** How many person-years of effort does this proposal require? Can you map each task to graduate student chapters or postdoc projects? Where is the co-PI support for real-robot maintenance and management?

4. **On Threat Model:** In your primary threat scenario, does the attacker have white-box, gray-box, or black-box access? Which is the priority for defense investment? (This should drive task weighting.)

5. **On Reproducibility:** What fraction of your evaluation will use open-source models/simulators? For closed-source models (e.g., RT-2), what is your plan to ensure reproducibility after the grant ends?

6. **On Generalization:** You claim findings generalize to "all VLA architectures." How do you ensure generalizability to future architectures (e.g., if models shift to diffusion-based action generation or symbolic reasoning)?

---

## 10. Conclusion

This proposal addresses a timely and important problem but falls short of the technical rigor and novelty needed for competitive SaTC funding at the current RES level. The breadth of scope (T0-T3, 6 robots, 5 models) is impressive but infeasible for a single-PI 4-year effort. Core technical contributions—adapted attacks and underevaluated defenses—lack novelty. With substantial revisions focusing on algorithmic innovation, evaluation rigor, and feasibility, this work could become competitive.

**Overall Recommendation:** REJECT, with encouragement to revise and resubmit to a future SaTC solicitation, ideally with explicit robotics security framing and co-PI partnerships.

---

## Appendix: Detailed Evaluation Rubric

| Criterion | Score | Evidence |
|-----------|-------|----------|
| Intellectual Merit - Novelty | 2.5/5 | Attacks are ported methods; defenses are adaptations. No algorithmic breakthrough. |
| Intellectual Merit - Impact | 3.5/5 | Multi-embodiment evaluation and benchmarking valuable to community; foundational contribution. |
| Broader Impacts - Educational | 4/5 | Strong curriculum/student engagement plans; clear mentoring structure. |
| Broader Impacts - Dual-Use | 2.5/5 | Minimal detail on responsible disclosure and attack tool gating. |
| SaTC Alignment - Trust Clarity | 2/5 | Definition is circular; operationalization needed. |
| SaTC Alignment - Threat Model | 3/5 | Taxonomy is detailed; deployment scenarios underspecified. |
| SaTC Alignment - Generalizability | 3.5/5 | Multi-model/embodiment scope is good; architecture diversity limited. |
| Evaluation Rigor | 2.5/5 | Preliminary results narrow in scope; missing baselines; weak statistical rigor. |
| Feasibility | 2/5 | Scope far exceeds single-PI capacity; robotics infrastructure demands underestimated. |
| Clarity | 3/5 | Well-written; technical framing clear; but threat model and trust definition vague. |
| **AVERAGE** | **2.9/5** | **GOOD (borderline)** |

---

*Panel Review Completed: August 31, 2026*  
*Reviewer Classification: External Expert, AI Security & Robotics*
