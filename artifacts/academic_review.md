# NSF SaTC 2.0: RES Academic Reviewer Assessment

**Proposal Title**: "Toward Secure and Robust Generalist Robotic Models"  
**PI**: Mohammed Abuhamad (Loyola University Chicago)  
**Co-PI**: [TBD]  
**Budget**: $555,171 total (4 years)  
**Evaluation Date**: September 8, 2026  
**Review Mode**: Academic Reviewer (Skeptical Senior Peer)  

---

## EXECUTIVE SUMMARY

This proposal addresses an important and timely problem—security of Vision-Language-Action (VLA) foundation models in robotics—and proposes a comprehensive three-task framework: (T1) vulnerability analysis via white/gray/black-box attacks, (T2) modality-inherited vulnerabilities, and (T3) safety benchmarks and interpretability, culminating in an open VLA-SecBench benchmark.

**Critical Issues Preventing Funding Recommendation:**

1. **Co-PI Status Unresolved (Co-PI: TBD)** — A blocking feasibility issue. Robotics expertise is undefined.
2. **Preliminary Evaluation is Weak** — Only 3 toy simulation tasks + 3 simple real robot tasks; no defense evaluation; no comparison to concurrent work (BadVLA, AdvVLA).
3. **Technical Novelty is Incremental** — Attacks are adaptations of existing VLM/LLM techniques; defenses lack validation. ABBP and TTDA are framed as "proposed research to be validated" with conditional go/no-go checks.
4. **Scope Exceeds Feasibility** — 6 embodiments, 15 datasets, 6 model families for 1 part-time PI + 1 graduate student is unrealistic.
5. **Multimodal Attacks (T2) Deferred** — Repositioned from core contribution to "scale-up track in Years 3–4," reducing MVP novelty.

**Recommendation: REJECT** — Major revisions required before resubmission.

---

## 1. SIGNIFICANCE

**Score: 6/10**

### Strengths
- **Timely Problem**: VLA models (RT-1, RT-2, OpenVLA, Octo) are deployed in industrial and service robotics. Security hardening at this foundational stage is strategically important and relatively unexplored.
- **Critical Gap**: Recent work (Robey et al. 2024: jailbreaks on LLM-controlled robots; Shi et al. 2024: adversarial vulnerabilities in quadrupedal control) demonstrates that vulnerabilities are real.
- **Practical Deployment Context**: Millions of industrial robots + service robots (logistics, medicine, home, defense) will eventually adopt foundation models. Understanding threats is necessary for safety.

### Limitations
- **Not Unprecedented**: Prior work has already identified jailbreaks (Robey et al.), backdoors (BadVLA, AdvVLA), and adversarial attacks on robot policies. This proposal frames itself as "first comprehensive framework," but more accurately it's "first systematic evaluation across embodiments + incremental attacks + benchmarking."
- **Threat Immediacy Unclear**: Are practitioners *today* deploying VLAs in adversarial settings, or is this a future-looking concern? The proposal doesn't quantify the immediate threat to practitioners.
- **Limited Scope Impact**: Even if successful, findings apply to a narrow domain (end-to-end learned policies). Don't generalize to classical control, symbolic AI, or hybrid systems.

**Verdict**: Important but not groundbreaking significance. Problem is well-motivated but not uniquely urgent vs. other SaTC investments.

---

## 2. PERCEIVED NOVELTY

**Score: 5/10**

### Core Contributions Assessed

**ABBP (Action-Bin Boundary Perturbation)**
- Claims to exploit 256-bin discretization of action space via kinematically-consistent Jacobian constraint.
- Formulation is **vague**: No formal specification of objective function, constraint formulation, or comparison to PGD.
- Framing is hedged: "We frame ABBP as research to be conducted, gated by a formal go/no-go check on whether action-space discretization yields a structurally distinct vulnerability."
- **Verdict**: Conditional contribution. If action-bin discretization yields distinct vulnerability, novelty is moderate (adaptation of constrained optimization). If not, ABBP is not a contribution.
- **Risk**: High. Preliminary evidence of superiority over PGD is absent.

**TTDA (Temporal Trajectory Drift Attack)**
- Targets multi-step action chunks in chunking policies (Octo), exploiting per-step kinematic checks to allow cumulative drift.
- Somewhat novel but **narrow scope**: Only applies to chunking policies. Extension to flow-matching policies deferred to Years 3–4 "contingent on model availability."
- Lacks formal analysis: "We will formalize sufficient conditions for such drift" is future work.
- **Verdict**: Novel for specific architecture but unvalidated. Narrow applicability limits impact.
- **Risk**: Moderate-High. Formal analysis may reveal drift is infeasible or requires impractical perturbations.

**Defenses (TACD, AGAT)**
- TACD (Temporal Action Consistency Detector): Multi-task trajectory forecasting with per-task thresholds. This is trajectory-level anomaly detection, which is **standard practice**, not novel.
- AGAT (Action-Grounded Adversarial Fine-Tuning): Adversarial fine-tuning with LoRA rank-16. Standard technique. No novelty.
- **Verdict**: Low novelty. TACD is reasonable but not innovative.

**VLA-SecBench**
- Open benchmark with cross-model transferability matrix, interpretability tools, attack/defense implementations.
- **Novelty**: Low. Benchmarking is engineering. Similar efforts underway (AttackVLA, ManiparArena, cited in proposal).
- **Value**: High for community. Infrastructure contribution, not research innovation.

### Non-Novel Elements (Porting Existing Work)
- **White-box attacks**: PGD, FGSM, C&W (2014–2017 methods) applied to visual encoders.
- **Gray-box attacks**: Prompt injection, jailbreak, membership inference. Standard LLM/VLM attack vectors.
- **Black-box attacks**: Token deletion/replacement, transfer-based. Existing methodology.
- **Multimodal attacks (T2)**: "Variations of attacks by Qi et al., Walmer et al. will be implemented against robotic models." This is porting, not innovation. **Critically, T2 is deferred to Years 3–4.**

### Reviewer Concern
"This proposal is primarily an engineering integration of known attack taxonomies and defense methods, with two incremental attack proposals (ABBP, TTDA) that are conditionally validated and one core defense (TACD) that is a standard anomaly detector. Much is porting VLM attacks to VLAs without exploiting VLA-specific structure. This is solid systems engineering but not a compelling research innovation."

**Verdict**: Below novelty bar for competitive SaTC funding. Would need clear evidence that ABBP/TTDA yield structurally distinct, practically superior attacks.

---

## 3. TECHNICAL DEPTH

**Score: 6/10**

### Strengths
- **Comprehensive Threat Taxonomy** (Table 1 in 02_v2.tex): Evasion, poisoning, privacy, abuse; across training/inference; white/gray/black-box. Well-structured and clear.
- **Multi-Modal Threat Formulation**: Formal notation $\mathcal{M}(\{\mathbf{x}\}, \{\mathbf{t}\}, \{\mathbf{s}\})$ frames input modalities rigorously.
- **Preliminary System Design**: Described five VLA architectures (RT-1, RT-2, Octo, ACT, RoboCat) with technical details on visual encoders, adapters, LLM backbones.
- **Evaluation Metrics**: Task Success Rate, action-token deviation, end-effector displacement, safety-zone violations, imperceptibility, transferability. Thoughtful metric selection.

### Weaknesses

**ABBP Formulation Vague**
- Proposal states: "ABBP optimizes perturbations to drive predicted action tokens across bin boundaries in a coordinated fashion across all degrees of freedom, subject to a kinematically-consistent Jacobian constraint."
- Questions:
  - How is Jacobian constraint formally incorporated? Hard constraint or soft penalty?
  - How does this differ from constrained optimization in prior work (e.g., Carlini-Wagner)?
  - Why is a "formal go/no-go check" necessary? Suggests uncertainty about whether ABBP is fundamentally different from PGD.
- **No Preliminary Comparison**: Zero evidence that ABBP outperforms or differs from PGD.
- **Verdict**: Lack of technical rigor in flagship contribution.

**TTDA Lacks Formal Analysis**
- Proposal states: "We will formalize sufficient conditions for such drift and characterize how chunk length affects feasibility."
- This is **future work**. No formal analysis provided.
- Claim that attack surface is "structurally absent in single-output VLMs" is unproven.
- **Verdict**: Foundational work incomplete.

**Preliminary Results Are Weak**
- White-box attacks (Figure 1): Success rates reported (~80% for PGD on RT-1) but no comparison to baseline accuracy or prior work. Is ABBP better? Unclear.
- Black-box attacks (Figure 2): Task success drops from ~100% to near 0% with 20% token perturbation. This shows fragility but is not a sophisticated attack.
- Only 25 evaluation episodes × 5 runs = 125 trials. Limited statistical power.
- No confidence intervals or significance tests.
- No defense evaluation whatsoever.

**Evaluation Plan Detailed but Not Grounded**
- Promises cross-model transferability matrix, yet zero preliminary transferability data.
- Promises comparison to 3+ baseline defenses, yet zero preliminary defense evaluation.
- Plans for 6 embodiments, 15 datasets, but preliminary scope is 2 embodiments, 4 models.
- Large gap between preliminary and full scope raises execution risk.

**Defenses Underdeveloped**
- TACD: Multi-task trajectory forecasting is standard. No preliminary false-positive rates, detection rates, or comparisons.
- AGAT: LoRA fine-tuning is standard. No preliminary robustness evaluation.
- No evidence these defenses stop attacks.

**Multimodal Coupling Formulation Missing**
- T2 promises to target FiLM, projection MLP, cross-attention with "model-specific co-perturbation objective." No formal definition. No preliminary results.
- Proposal positions this as "scale-up track in Years 3–4," deferring core work.

**Verdict**: Technical depth is solid in framing and experimental design, but novel contributions lack formal grounding or validation. Risk is high that ABBP/TTDA will not deliver.

---

## 4. EVALUATION STRENGTH

**Score: 5/10**

### Planned Evaluation (Strengths)
- Primary metric (Task Success Rate under attack) is appropriate and physically grounded.
- Secondary metrics (action-token deviation, end-effector displacement, safety violations) are well-chosen.
- Cross-model transferability matrix addresses generalization.
- Evaluation across 6 embodiments, 15 datasets is ambitious scope.
- Planned comparison to 3+ baseline defenses.
- Welch's t-tests for significance (statistical rigor).

### Planned Evaluation (Limitations)
- TSR is binary; may be coarse for subtle attacks.
- 30% action-token deviation proxy lacks justification.
- Assumes defenses are applicable across embodiments; embodiment-specific false-positive rates not discussed.
- "At least ten runs with multiple seeds" is acceptable but modest for deep learning.

### Preliminary Evaluation (Major Weaknesses)

**Limited Task Scope**
- Only 3 simulation tasks (Close Drawer, Move Closer, Pick Coke Can) and 3 real robot tasks (Stack Cubes, Duck in Bowl, Sweep).
- These are basic manipulation tasks. No complex multi-step reasoning, navigation, or high-consequence scenarios.
- Gap between preliminary scope (2 embodiments) and full scope (6 embodiments) is large.

**Weak Baselines**
- White-box: Only PGD, FGSM, C&W. No comparison to certified defenses, randomized smoothing, or recent work.
- Black-box: Only 20% token perturbation. No comparison to other black-box attack methods.
- Defense baselines: **None**. No comparison to input smoothing, ensemble voting, or other defenses.

**No Comparison to Concurrent Work**
- Cites BadVLA (backdoor attacks on VLAs), AdvVLA (adversarial attacks on VLAs), but does not compare attacks or defenses.
- Does not benchmark against these concurrent efforts.

**Arbitrary Success Metrics**
- 30% action-token deviation used to define attack success. How was this threshold chosen? Is it imperceptible? Unproven.
- Figures report success rates but no comparison to baseline model accuracy.

**Limited Model Coverage**
- Only 4 models evaluated (RT-1, RT-2, Octo, ACT).
- Full scope targets 6 models. OpenVLA, RoboCat evaluation missing.

**No Transferability Preliminary Results**
- Proposal promises cross-model transferability matrix; zero preliminary data.
- Do attacks on RT-1 transfer to Octo? Unknown. This is critical for understanding generalization.

**No Defense Evaluation**
- TACD and AGAT: Zero preliminary results.
- How well do they work? False-positive rates? Unknown.
- No comparison to baselines.

**Statistical Rigor**
- Figures lack error bars, confidence intervals, significance tests.
- Only 5 random seeds; limited statistical power.

**Reviewer Concern**
"Preliminary evaluation does not support feasibility of ambitious full evaluation. Attacks not compared to prior work or shown to outperform baselines. Defenses completely unevaluated. Scope gap between preliminary (2 embodiments, 4 models) and full (6 embodiments, 6 models) suggests execution risk of incomplete evaluation."

**Verdict**: Planned evaluation is comprehensive and well-designed, but preliminary data is insufficient to demonstrate feasibility. High risk of under-delivery on full evaluation.

---

## 5. CLARITY & POSITIONING

**Score: 7/10**

### Strengths
- Generally well-written with strong figures (VLA timeline, threat taxonomy, pipeline architecture, work-plan Gantt chart).
- Clear problem motivation and three-task structure.
- Comprehensive background on robotic learning and foundation models.
- Detailed timeline with milestones and dependencies.

### Weaknesses

**Co-PI Status Unresolved**
- Budget lists "George K. Thiruvathukal, Co-Principal Investigator" with salary allocation.
- But text states "[Co-PI: TBD]".
- Is Thiruvathukal confirmed or not? This is ambiguous and problematic for evaluation.

**ABBP Confidence Unclear**
- Framing as "proposed research to be validated rather than completed results" and "gated by a formal go/no-go check" suggests uncertainty about whether attack works.
- Why not perform go/no-go analysis before proposal submission?

**Multimodal Attacks Downgraded**
- Initially claims three "conceptual ideas," including "investigation of modality-specific vulnerabilities in multimodal robots" (T2).
- Later repositions T2 as "scale-up track in Years 3–4 that builds on T1 baselines."
- This is a significant scope reduction. If multimodal attacks are core, they should be in MVP.

**"First Comprehensive Framework" Claim Overstated**
- Proposal repeatedly claims this is the "first comprehensive framework." But:
  - Robey et al. (2024): jailbreak attacks on robots
  - Shi et al. (2024): adversarial vulnerabilities
  - BadVLA, AdvVLA (cited): attacks on VLAs
- More honest framing: "First systematic evaluation across multiple embodiments and model families + two novel attacks (ABBP, TTDA) + open benchmark."

**Threat Model Ambiguous**
- Discusses white/gray/black-box attacks but doesn't clearly prioritize which threat scenario is most realistic.
- Doesn't distinguish between open-source models (OpenVLA) vs. commercial APIs.
- "Trust" defined as producing "safe, intended physical actions" — circular definition. What is "intended"?

**Risk Mitigation Absent**
- What if ABBP/TTDA fail (go/no-go check returns negative)? No contingency.
- What if certain models (RT-2) are unavailable? No contingency.
- What if transferability is zero? Impact on benchmark utility not discussed.

**Responsible Disclosure Vague**
- States "attack tooling will be gated appropriately to prevent misuse" but provides no specifics.
- No timeline for disclosure relative to publication.
- No approval process defined.

**Verdict**: Proposal is clear and well-structured, but key ambiguities (Co-PI status, ABBP confidence, multimodal scope, threat model) create confusion. Honest framing of novelty would strengthen proposal.

---

## 6. RELATED WORK POSITIONING

**Score: 6/10**

### Strengths
- VLA Timeline (Figure in 01_v2.tex): Comprehensive evolution from RT-1 (2022) through 2025 models (SpatialVLA, GR00T, Gemini Robotics). Valuable context.
- Covers foundation models (RT-X, Octo, OpenVLA), defenses (JailGuard, ECSO, alignment methods), and robotic vulnerabilities (Robey et al., Shi et al.).
- Threat taxonomy cites VLM security literature (evasion, poisoning, privacy, abuse).

### Gaps

**Concurrent Work Not Deeply Engaged**
- Cites BadVLA and AdvVLA but doesn't clearly differentiate:
  - BadVLA: Backdoor attacks on VLAs
  - AdvVLA: Adversarial attacks on VLAs
  - This proposal: Comprehensive evaluation + ABBP/TTDA + defenses + benchmark
- Major omission: How does ABBP differ from or improve on AdvVLA attacks? Unclear.

**Recent Jailbreak Work Underexplored**
- Cites Robey et al. (2024) on jailbreaks but doesn't deeply engage.
- Are jailbreaks (text-only) fundamentally different from TTDA (temporal trajectory)? Proposal doesn't explain.
- How do defenses for jailbreaks (ECSO, MLLM-Protector) relate to TACD? Not discussed.

**Certified Defenses Sidelined**
- Proposal mentions "randomized smoothing for certified robustness" in future work but doesn't plan certified defenses as core contribution.
- This is a missed opportunity; certified defenses are more principled than detection-based anomaly detectors.

**Interpretability in Robotics**
- Cites generic VLM interpretability methods (Attention Rollout, heatmaps, probing tasks).
- Limited engagement with robotics-specific interpretability (causal analysis of actions, counterfactual trajectories).

**Transferability Theory**
- Promises cross-model transferability matrix but doesn't ground in related work on adversarial transferability.
- What factors drive or inhibit transfer across VLA architectures? No theoretical framework provided.

**Embodiment-Specific Vulnerabilities**
- Targets 6 embodiments but doesn't discuss whether vulnerabilities differ (e.g., are arms more/less vulnerable than quadrupeds?).
- No engagement with embodiment-aware learning literature.

**Positioning Against Concurrent Work**
- Proposal should explicitly state: "BadVLA targets training-time backdoors; AdvVLA targets single-model adversarial robustness. We provide: (1) systematic evaluation across embodiments, (2) novel attacks (ABBP, TTDA) exploiting [specific VLA properties], (3) multimodal attack analysis, (4) open benchmark."
- Currently, positioning is generic.

**Verdict**: Related work coverage is comprehensive but positioning is somewhat shallow. Proposal should more clearly articulate what is novel relative to BadVLA, AdvVLA, and concurrent work.

---

## 7. FEASIBILITY PERCEPTION

**Score: 5/10**

### Positive Factors
- Budget ($555K) is reasonable and not inflated. Realistic for 4-year project.
- Timeline (4 years, MVP + scale-up) is realistic for phased approach.
- Preliminary experiments demonstrate PI can execute robotic learning experiments.
- Infrastructure in place (GPU cluster, Loyola RDC, SSL lab with robotic equipment).
- Prior work on AI security shows PI is capable.

### Negative Factors

**Team Size vs. Scope**
- 1 PI (1 summer month/year) = ~1.3 months/year
- 1 Co-PI (1 summer month/year, but TBD) = ~1.3 months/year
- 1 Graduate student (full-time) = ~12 months/year
- 1 Undergraduate student (10 hrs/week) = ~0.25 FTE
- **Total: ~15 person-months/year**

**Scope for 15 Person-Months/Year:**
- T0: Build/train/evaluate models on 6 embodiments, 15 datasets
- T1: Implement white/gray/black-box attacks (12-15 attack types from Table 1)
- T1-4: Develop and evaluate defenses (TACD, AGAT, baselines)
- T2: Multimodal attacks (deferred to Years 3–4 but still added work)
- T3-1: Safety benchmarks
- T3-2: Interpretability methods
- Real robot experiments on 6 embodiments
- Educational output (curriculum, workshops)

**This is 30–35 person-months/year of work.** Ratio of work-to-capacity is 2–2.3×.

**Co-PI Status Risk**
- If Co-PI falls through, remaining team lacks robot learning expertise.
- PI is AI security researcher; graduate student alone cannot manage robotics experiments.
- **Critical feasibility blocker**.

**Model Availability Risk**
- Budget includes $[PLACEHOLDER] for "black-box API for proprietary VLAs in Years 3–4."
- Placeholder suggests uncertainty about cost and availability.
- If proprietary models unavailable, benchmark is incomplete.

**Real-Robot Logistics**
- Maintaining 6 robot platforms over 4 years is expensive and labor-intensive.
- Proposal budgets ~30 GPU compute + travel but doesn't clearly budget for robot maintenance, dataset management, or systems engineering.
- Single PI lab at Loyola likely does not have dedicated robotics engineering staff.

**Preliminary Scope vs. Full Scope**
- Preliminary: 2 embodiments (Xarm7, Google robot), 4 models, 3 tasks each.
- Full: 6 embodiments, 6 models, 10+ tasks per embodiment.
- Gap suggests risk of incomplete full evaluation.

**Phase 2 Scope Creep**
- Years 1–2 (MVP): ABBP, TTDA, TACD, AGAT on 2 embodiments.
- Years 3–4 (Scale-up): Multimodal attacks, certified defenses, full VLA-SecBench release.
- Phase 2 is compressed and dependent on Phase 1 completion. If Phase 1 runs behind, Phase 2 is squeezed.

**Student Retention**
- Graduate student graduation cycle: onboarding + research = 2–3 years. If student graduates Year 2, replacement must be recruited and onboarded. Transition loss is ~6 months.
- Proposal doesn't discuss contingency for turnover.

**Contingency Planning: Absent**
- What if ABBP/TTDA fail go/no-go checks? No backup attacks specified.
- What if models unavailable? No fallback to simulation-only evaluation.
- What if multimodal coupling proves infeasible? No alternative T2 approach.
- What if graduate student leaves? No replacement/backup plan.

**Verdict**: Proposal is feasible under ideal conditions but faces significant execution risks. Co-PI TBD is a critical blocker. Team-to-scope ratio is tight (2–2.3×). Contingency planning is absent. High risk of incomplete deliverables or rushed execution.

---

## 8. BROADER IMPACTS

**Score: 7/10**

### Strengths
- **Educational Integration**: Curriculum modules, labs, workshops for HS/undergrad/grad students. Detailed mentoring plans (undergrad weekly meetings, grad student bi-weekly meetings, career guidance).
- **Open-Source Release**: Commitment to release attack tools, defenses, datasets, benchmarks under permissive licenses. Enables community reuse.
- **VLA-SecBench**: Open benchmark could become standard for community evaluation.
- **Workforce Development**: CyberRamblers program already recruiting from underrepresented groups (50% goal). Synergistic activities show PI's engagement (SecureAI program, CS seminar series, curriculum development).
- **Interdisciplinary Bridge**: Connects AI security, robotics, and cybersecurity communities.

### Limitations
- **Responsible Disclosure Details Sparse**: Promises "attack tooling will be gated appropriately" but no specifics on gates, timelines, or approval processes. Could be clearer.
- **Industry Engagement Missing**: No workshops or outreach to roboticists/vendors. How will findings be communicated to practitioners?
- **Generalizability Overstated**: Claims findings "extend beyond robotics and benefit adjacent domains (AI/multimodal security)" but provides no evidence. How does action-space anomaly detection generalize to autonomous vehicles or medical AI?
- **Long-Term Sustainability**: What happens when VLA architectures evolve in 2–3 years? How will benchmarks be maintained/updated? No discussion.
- **Equity & Access**: Benchmarks require access to VLA models and robot hardware. Does this widen or narrow gap for under-resourced institutions? Not discussed.

**Verdict**: Broader impacts are well-developed with concrete educational and community outcomes. Could be enhanced with industry engagement, long-term sustainability plans, and clearer responsible disclosure strategy.

---

## 9. REVIEWER ATTACKS (Critical Arguments)

### Attack 1: "This is primarily engineering integration, not research innovation."
**Severity: CRITICAL**

The proposal adapts known VLM attack methods (PGD, FGSM, C&W, jailbreak, membership inference) to robotics, implements standard defenses (anomaly detection, adversarial training), and builds a benchmark. This is engineering systems integration—valuable for the community but not advancing fundamental security science in robotics.

**Evidence:**
- Attacks are from 2014–2017 literature (PGD, FGSM, C&W).
- Gray/black-box attacks (prompt injection, jailbreak) are standard LLM attacks.
- TACD is trajectory-level anomaly detection (standard).
- AGAT is adversarial training with LoRA (standard).
- Multimodal attacks proposed as "variations of existing attacks" and deferred to Phase 2.

**Implication:** Proposal should be submitted to a systems/tools venue (e.g., USENIX Security tools track, or a robotics conference) rather than NSF SaTC RES, which expects novel algorithms or theoretical insights.

---

### Attack 2: "Co-PI TBD makes proposal un-evaluable and creates blocking feasibility risk."
**Severity: CRITICAL**

The proposal lists a Co-PI in the budget (George K. Thiruvathukal) but states "[Co-PI: TBD]" in the text. Robotics foundation models require expertise in manipulation, control, embodiment-specific constraints, and real-robot experimentation. The PI (AI security researcher) does not provide this expertise.

**Evidence:**
- Budget includes Co-PI salary but Co-PI identity is unclear.
- PI publication record focuses on AI security (CCS, IEEE ICDCS, TIFS, IEEE IoT-J), not robotics.
- Facilities section mentions "SSL lab has robotic equipment" but no robot expert listed.
- Graduate student alone cannot manage robotics experiments across 6 embodiments.

**Implication:** Without a confirmed roboticist, the project is infeasible. If Co-PI recruitment falls through, team lacks critical expertise.

---

### Attack 3: "Preliminary evaluation does not support feasibility of ambitious full evaluation."
**Severity: MAJOR**

Preliminary results are on 3 toy simulation tasks + 3 simple real robot tasks. Full scope targets 6 embodiments, 15 datasets, 6 models. No defense evaluation. No comparison to concurrent work (BadVLA, AdvVLA). Statistical rigor is weak (5 runs, no significance tests).

**Evidence:**
- Scope gap: Preliminary 2 embodiments/4 models vs. full 6 embodiments/6 models.
- Zero defense evaluation.
- No comparison to BadVLA, AdvVLA, or other baselines.
- Figures lack error bars, confidence intervals.
- Only 5 random seeds per task.

**Implication:** High risk that once full evaluation begins, attacks/defenses will not perform as hypothesized, or execution will be rushed/incomplete.

---

### Attack 4: "ABBP and TTDA are conditionally validated; not established contributions."
**Severity: MAJOR**

ABBP is "gated by a formal go/no-go check on whether action-space discretization yields a structurally distinct vulnerability." This hedging suggests the PI is uncertain whether the attack works. TTDA "will formalize sufficient conditions for such drift" — formal analysis not yet done.

**Evidence:**
- Proposal frames ABBP as "research to be conducted, gated by go/no-go check."
- No formalization of Jacobian constraint or comparison to PGD.
- TTDA lacks formal analysis of drift conditions.
- No preliminary evidence of superiority over baselines.

**Implication:** These are not contributions yet; they are proposed research with uncertain feasibility. Proposal should not claim them as core contributions.

---

### Attack 5: "Multimodal attacks (T2), claimed as core, are deferred to Phase 2."
**Severity: MAJOR**

Proposal lists three main "conceptual ideas," including "investigation of modality-specific vulnerabilities in multimodal robots" (T2). But T2 is repositioned: "We present T2 as a scale-up track in Years 3 and 4 that builds on attack baselines established in T1."

**Evidence:**
- Intellectual merit section cites (2) investigation of multimodal vulnerabilities as core.
- T2 section states it is a "scale-up track in Years 3–4."
- This is a downgrade of scope.

**Implication:** MVP is weaker than claimed. Core contributions (ABBP, TTDA) are incremental; major contribution (multimodal attacks) is deferred.

---

### Attack 6: "Scope far exceeds single-PI capacity over 4 years."
**Severity: MAJOR**

Targeting 6 embodiments, 15 datasets, 6 models, 3 attack categories, 2 defenses, 1 benchmark with 15 person-months/year is unrealistic. Equivalent to 30–35 person-months/year of work.

**Evidence:**
- Team FTE: ~15 person-months/year.
- Scope: T0-T3, 6 robots, 5+ models, 15 datasets, 12+ attack types, multiple defenses.
- Real-robot logistics (maintenance, data management) not explicitly budgeted.

**Implication:** Proposal will deliver incomplete results or sacrifice depth for breadth.

---

### Attack 7: "Novelty claims are overstated; work is primarily porting and benchmarking."
**Severity: MAJOR**

Proposal claims "first comprehensive framework" and "first systematic evaluation," but concurrent work (BadVLA, AdvVLA, Robey et al.) is already addressing similar problems. ABBP and TTDA are incremental; VLA-SecBench is benchmarking (infrastructure, not research).

**Evidence:**
- Attacks are adaptations of existing methods (PGD, jailbreak, membership inference).
- VLA-SecBench is similar to AttackVLA, ManiparArena (cited).
- No algorithmic breakthrough in attacks or defenses.

**Implication:** Novelty is below the bar for research funding in a competitive SaTC program.

---

### Attack 8: "Risk mitigation and contingency planning are absent."
**Severity: MODERATE**

Proposal does not discuss what happens if:
- ABBP/TTDA fail go/no-go checks (become non-contributions).
- Proprietary models (RT-2) are unavailable for research.
- Transferability is zero (benchmark utility reduced).
- Graduate student leaves (team disrupted).
- Multimodal coupling proves infeasible.

**Evidence:**
- Budget includes $[PLACEHOLDER] for proprietary VLA APIs (uncertainty about cost/availability).
- No backup attacks if ABBP/TTDA fail.
- No fallback to simulation-only evaluation if real robots unavailable.
- No contingency for student turnover.

**Implication:** High execution risk. Proposal does not demonstrate preparedness for common obstacles.

---

### Attack 9: "Defenses are underevaluated and appear to be safety filters, not security mechanisms."
**Severity: MODERATE**

TACD (trajectory-level anomaly detection) and AGAT (adversarial fine-tuning) lack any preliminary evaluation. Zero preliminary results shown. Defenses may not stop attacks that are constrained to be kinematically plausible.

**Evidence:**
- No preliminary false-positive rates, detection rates, or robustness evaluation for defenses.
- No comparison to baseline defenses.
- Action-space anomaly detection may only filter obviously invalid actions, not sophisticated attacks.

**Implication:** Defenses are unvalidated. Proposal claims defense contribution without evidence.

---

### Attack 10: "Threat model and trust definition are ambiguous and lack operational grounding."
**Severity: MODERATE**

Proposal defines trust circularly ("safe, intended physical actions") and doesn't clearly prioritize threat scenarios. Unclear whether defending against insider white-box attacks vs. external black-box attacks. Multimodal inputs mentioned but priority unclear.

**Evidence:**
- Trust defined as producing "safe, intended actions" — circular.
- Threat model spans white/gray/black-box but doesn't prioritize.
- Doesn't distinguish between open-source models (OpenVLA) vs. commercial APIs.

**Implication:** Without clear threat models, evaluation claims lack grounding. Proposal is addressing too many threats without depth in any.

---

## 10. IMPROVEMENT PRESSURE TEST

### What Would Make This Competitive?

**Required Changes:**

1. **Resolve Co-PI Status (Blocking)**
   - Identify and confirm robot learning expert as Co-PI with publication record in robotics.
   - Provide letter of commitment clarifying effort allocation and role.
   - Update organizational structure and budget accordingly.

2. **Narrow MVP Scope (Critical)**
   - Focus on 2 embodiments (Xarm7, Google robot) with open-source models (OpenVLA, Octo).
   - Reduce to 3 key attack categories (white-box, black-box, multimodal).
   - Defer complex multi-embodiment evaluation and certified defenses to Phase 2.
   - This makes scope feasible for 1 grad student + 0.5 PI time.

3. **Validate ABBP and TTDA (Critical)**
   - Perform go/no-go analysis on ABBP before resubmission. Include results in proposal.
   - Formalize Jacobian constraint and optimization objective for ABBP.
   - Compare ABBP to PGD on preliminary tasks. Show advantage (lower budget, higher imperceptibility, better transfer).
   - Formalize sufficient conditions for TTDA drift. Show feasibility with preliminary attacks.
   - If attacks are not superior to baselines, reposition as "systematic evaluation of existing attacks" rather than novel contributions.

4. **Strengthen Preliminary Evaluation (Critical)**
   - Add defense results: TACD detection rates (≥70% on attacks), false-positive rates (≤5% on benign).
   - Evaluate AGAT robustness on toy task.
   - Compare attacks to BadVLA, AdvVLA methods.
   - Increase evaluation to 10+ runs with significance testing (Welch's t-test).
   - Add human evaluation of imperceptibility (informal survey).

5. **Clarify Threat Models and Trust Definition (Major)**
   - Define 3-4 explicit threat actors: insider white-box, external black-box, supply-chain poisoning, physical sensors.
   - For each actor, specify attack goals: cause task failure, cause specific harm, extract data, corrupt trajectory.
   - Define trustworthiness operationally: "Robot is trustworthy if (1) resists attacks with <5% success, (2) recovers within 1 second, (3) logs intrusions, (4) explains decisions."
   - Map each research task (T0-T3) to trustworthiness criteria.

6. **Detail Risk Mitigation (Major)**
   - Plan B if ABBP/TTDA don't work: fall back to established attack methods (PGD).
   - Plan B if models unavailable: use open-source models only (OpenVLA, Octo).
   - Plan for graduate student turnover: clear documentation, onboarding.
   - Model availability contingency: specify which models are required vs. optional.

7. **Specify Responsible Disclosure (Major)**
   - Define gating policy: e.g., "Attack code released under NDA to academic researchers; 6-month embargo before public release."
   - Approval process: ethics board review? Vendor pre-disclosure?
   - Timeline: release schedule relative to publication.

8. **Add Industry/Practitioner Engagement (Moderate)**
   - Plan workshops or webinars for roboticists and vendors.
   - Identify practitioners who will pilot tools or provide feedback.
   - Discuss pathways for findings to influence practice (e.g., industry standards, robot safety guidelines).

9. **Improve Evaluation Rigor (Moderate)**
   - Add more realistic tasks (multi-step manipulation, navigation, reasoning).
   - Include transfer evaluation: attack trained on one model, tested on another.
   - Report robustness-compute tradeoff: how much computational cost for defenses?

10. **Clarify Novelty & Positioning (Moderate)**
    - Explicitly state what is novel relative to BadVLA, AdvVLA, concurrent work.
    - Reposition from "first comprehensive framework" to "systematic evaluation across embodiments + incremental attacks + open benchmark."
    - Articulate VLA-specific attack properties that are not present in VLMs.

### Impact of Changes

- **Narrowed scope** makes project feasible for team size/budget.
- **Confirmed Co-PI** eliminates critical risk.
- **Validated ABBP/TTDA** removes conditional framing; establishes contributions.
- **Stronger preliminary eval** reduces execution risk.
- **Clear threat models** address SaTC program alignment.
- **Risk mitigation** demonstrates preparedness.

**If all changes implemented:**
- **Rating upgrade**: REJECT → Borderline or Weak Accept
- **Funding likelihood upgrade**: 15–20% → 40–50%
- **Major caveat**: Even with changes, novelty concerns remain. Proposal is primarily "benchmarking + porting," not research breakthrough. This will limit funding enthusiasm.

---

## 11. COMPARATIVE STANDING

If 10 similar SaTC proposals on AI/ML security are submitted, this proposal would rank:

**Estimated Ranking: 6th–8th quintile (below average to borderline)**

**Why below average:**
- Important problem (✓) but not uniquely urgent
- Weak preliminary evaluation (✗)
- Unresolved Co-PI (✗)
- Incremental novelty (✗)
- Feasibility concerns (✗)

**Why above strong rejects:**
- VLA-SecBench and open-source tools valuable (✓)
- Educational components strong (✓)
- Problem is timely (✓)

**Competitive landscape:**
- **Rank 1–2** (Strong Accept): Novel attack method with formal guarantees + certified defense + comprehensive preliminary validation. Full team confirmed.
- **Rank 3–4** (Accept): Solid contribution + good preliminary eval + feasible scope. This proposal with major revisions might reach this.
- **Rank 5–6** (Borderline): Important problem but modest novelty. Execution risk. **Current proposal is here.**
- **Rank 7–8** (Reject): Over-ambitious scope, weak evaluation, unresolved team.
- **Rank 9–10** (Strong Reject): Fundamental technical flaws or inappropriate for program.

---

## 12. DECISION SIMULATION

```
Decision: REJECT
Recommendation: Require Major Revisions Before Resubmission
Funding Likelihood (Current Form): 15–20%
```

### Rationale

The proposal addresses a timely and important problem (VLA security in robotics) and proposes a structured three-task framework. The team has demonstrated preliminary capability in robotic learning and adversarial evaluation. Broader impacts are well-developed.

**However, critical weaknesses prevent funding recommendation:**

1. **Co-PI Status TBD** (Blocking): Robotics expertise is undefined. Feasibility cannot be assessed without confirmed Co-PI.

2. **Preliminary Evaluation Weak**: Only toy tasks; no defense eval; no comparison to concurrent work (BadVLA, AdvVLA). Execution risk is high.

3. **Novelty Incremental**: Much work is porting VLM attacks. ABBP and TTDA are conditional contributions with uncertain feasibility. Multimodal attacks deferred to Phase 2. Below bar for research innovation.

4. **Scope Exceeds Feasibility**: 6 embodiments, 15 datasets, 6 models for 1.3 FTE researchers is 2–2.3× overcommitted.

5. **Threat Model Ambiguous**: Trust definition is circular; threat scenarios underspecified. Unclear which attacks are priority.

With substantial revisions (especially Co-PI confirmation, MVP scope narrowing, and validated ABBP/TTDA), proposal could become competitive. But current form does not meet funding threshold.

---

## 13. META ASSESSMENT

| Dimension | Level | Rationale |
|-----------|-------|-----------|
| **Enthusiasm** | Low | Problem is timely; execution concerns dampen enthusiasm significantly. |
| **Confidence** | Moderate | Confident in assessment of novelty, feasibility, and evaluation gaps. Less certain about potential with major revisions. |
| **Funding Likelihood** | Low | 15–20% chance at major NSF SaTC program; 30–40% if revised as suggested. |

---

## 14. SUMMARY: TOP 5 MAJOR WEAKNESSES

### 1. **Co-PI TBD (Critical)**
Robotics expertise is undefined. Blocking feasibility risk.  
**Location**: Budget, Intellectual Merit section  
**Fix**: Identify and confirm Co-PI with robot learning expertise.

### 2. **Preliminary Evaluation Weak (Critical)**
Only toy tasks (3 sim + 3 real); zero defense evaluation; no comparison to concurrent work.  
**Location**: 02_v2.tex, Preliminary Experiments  
**Risk**: Execution risk of incomplete full evaluation.  
**Fix**: Add defense eval, increase task complexity, compare to BadVLA/AdvVLA.

### 3. **Novelty Incremental (Major)**
ABBP and TTDA conditional; much work is porting VLM attacks. T2 multimodal attacks deferred to Phase 2.  
**Location**: Overview, T1-1, T1-3, T2 sections  
**Fix**: Perform go/no-go validation before submission. Reposition as "systematic evaluation + benchmarking."

### 4. **Scope Exceeds Feasibility (Major)**
6 embodiments, 15 datasets, 6 models for 1.3 FTE is 2–2.3× overcommitted.  
**Location**: T0-T3, Budget  
**Fix**: Narrow to 2 embodiments, 3 models; defer scale-up to Phase 2.

### 5. **Threat Model & Trust Ambiguous (Major)**
Circular trust definition; threat scenarios underspecified; unclear priorities.  
**Location**: Overview, Background, T1-T3  
**Fix**: Define explicit threat actors/goals. Operationalize trustworthiness. Map tasks to SaTC criteria.

---

## CONCLUSION

This proposal is a competent engineering effort addressing an important problem, but falls below the threshold for competitive NSF SaTC funding due to critical weaknesses: unresolved Co-PI, weak preliminary evaluation, incremental novelty, scope-feasibility mismatch, and ambiguous threat models.

**Recommendation: REJECT** with encouragement to revise and resubmit.

**Path to Fundability**: (1) Confirm Co-PI, (2) Narrow MVP scope to 2 embodiments/3 models, (3) Validate ABBP/TTDA before resubmission, (4) Strengthen preliminary defense evaluation, (5) Clarify threat models and trustworthiness criteria.

With these changes, proposal could reach **Borderline or Weak Accept** status.

---

**Review Completed**: September 8, 2026  
**Reviewer Mode**: Academic Reviewer (Skeptical Senior Peer)  
**Overall Score**: 5.5/10 (Below Funding Threshold)

