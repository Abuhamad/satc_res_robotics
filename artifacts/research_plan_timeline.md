# NSF SaTC 2.0 RES — Research Plan and 4-Year Timeline
## Toward Secure and Trustworthy Generalist Vision-Language-Action Robotic Foundation Models

**Proposal Title:** SaTC 2.0: RES: Toward Secure and Robust Generalist Robotic Models  
**Program:** NSF 25-515 (SaTC 2.0 RES)  
**Duration:** 4 years (Year 1: ~Sep 2027 – Aug 2028, ... Year 4: ~Sep 2030 – Aug 2031)  
**Team:** PI (AI/ML security, adversarial ML) + Co-PI [ASSUMPTION — see §7]  
**Generated:** 2026-08-31 (Planner Agent)

> **Collaboration Plan flag:** If combined direct costs across both investigators exceed $600K, NSF requires a Collaboration Plan as a supplementary document. This plan does not compute dollar amounts; the PI must confirm the total and prepare the plan if needed.

---

## Part 1 — Executive Research Program

```yaml
Research Program:
  Vision: >
    A future in which generalist VLA robotic foundation models can be deployed in
    safety-critical environments with mathematically-grounded security guarantees —
    because the threat landscape specific to robotic action spaces has been
    systematically characterized, attacked, defended, and benchmarked.

  Mission: >
    Develop the first research program that (a) identifies and formalizes
    VLA-specific attack primitives rooted in action-space quantization and
    temporal trajectory structure, (b) designs and empirically validates
    layered defenses unique to the robotic action domain, (c) evaluates
    attack/defense transfer across models and embodiments with physically
    grounded metrics, and (d) releases open benchmarks and tools that
    enable the broader community to build on this foundation.

  Goal: >
    Produce a rigorously evaluated, open-science security framework for
    generalist VLA models (OpenVLA, Octo, pi-0 / flow-matching variants)
    that demonstrates: novel VLA-specific attacks outperform ported VLM
    baselines; validated defenses achieve meaningful detection/protection
    rates; and results transfer across at least two model families and
    two embodiment classes.

  Impact: >
    (1) Direct: hardened open-source VLA models; (2) Community: reusable
    attack/defense tooling and the first VLA security benchmark with
    physically-grounded metrics; (3) Workforce: SaTC-aligned curriculum
    integrating adversarial robotics into undergraduate and graduate courses;
    (4) Policy: threat taxonomy aligned with NIST AI RMF informing future
    robotic deployment standards.
```

---

## Part 2 — Research Objectives

```yaml
Objectives:
  - Objective: "O1 — VLA-Specific Attack Formalization"
    Success Criteria: >
      Formal characterization of ≥2 attack classes that exploit mechanisms
      structurally absent in VLMs (action-bin quantization, temporal chunk
      dependency); demonstrated superiority over naive ported PGD/C&W baselines
      on task-success-rate reduction metric across ≥2 model × embodiment pairs.

  - Objective: "O2 — Validated Multi-Layer Defense"
    Success Criteria: >
      Empirically-validated defense stack (anomaly detection layer +
      adversarial fine-tuning layer) with reported detection rate, false-positive
      rate, and comparison to ≥3 baseline defenses on ≥2 models × ≥2 embodiments.

  - Objective: "O3 — Cross-Modal Attack Characterization"
    Success Criteria: >
      Tightly-coupled multimodal adversarial examples (visual + language joint
      perturbation) shown to achieve higher transferability across embodiments
      than independently designed unimodal attacks; evaluated on ≥4 embodiment
      × model combinations.

  - Objective: "O4 — Open Benchmark and Transferability Framework"
    Success Criteria: >
      Publicly released VLA security benchmark suite including: full
      transferability matrix (≥3 models × ≥2 embodiments × ≥4 attack types);
      physically grounded primary metrics (task completion under attack,
      end-effector displacement, safety-zone violation rate); and ≥1
      interpretability tool validated on action attribution.

  - Objective: "O5 — Reproducibility and Open Science"
    Success Criteria: >
      All Year-1 and Year-2 experiments reproducible on OpenVLA + Octo
      on the Simpler benchmark by Month 24; attack/defense tooling released
      under institutional data-use agreement; OSF pre-registration before
      each major experiment.
```

---

## Part 3 — Research Aims

```yaml
Aims:
  - Aim: "Aim 1 — VLA-Specific Threat Landscape: Repository, Taxonomy, and Novel Attack Primitives"
    Maps_to: "T0 (repository infrastructure), T1-1 (white-box), T1-2 (gray-box), T1-3 (black-box)"
    Purpose: >
      Build the multi-embodiment data/model repository and develop attack methods
      that exploit structural properties of VLA action spaces that are absent in
      pure VLM or language-model settings — specifically the semantic continuity
      of discretized action bins and the temporal-chunk dependency of multi-step
      action prediction.
    Genuine_Contribution: >
      Two novel attack primitives (research to be conducted, not results already
      obtained):
      (A) Action-Bin Boundary Perturbation (ABBP): a gradient-based white-box
      attack that drives predicted action tokens across bin boundaries in a
      coordinated, kinematically consistent way across all action dimensions
      simultaneously. Because adjacent action bins represent physically close
      — but discretely different — control signals, small cross-boundary
      perturbations produce physically meaningful trajectory deviation with
      less perturbation budget than required for equivalent effect on continuous
      language token spaces. The attack formulation explicitly constrains the
      Jacobian of the action decoder to exploit correlated dimension coupling
      (e.g., x,y,z,roll,pitch,yaw must be perturbed jointly to maintain
      reachability), a constraint structure absent in language generation.
      (B) Temporal Trajectory Drift Attack (TTDA): a trajectory-level gray/
      black-box attack that crafts slowly-accumulating adversarial perturbations
      across the multi-step action chunk predicted by Octo- and diffusion-based
      policies (pi-0). Each individual step satisfies per-step kinematic limits
      (passing naive anomaly checks), but the cumulative trajectory drifts to a
      task-failing or workspace-violating end configuration. This is structurally
      impossible in single-output VLMs. We will formalize the sufficient
      conditions for such drift, characterize how chunk length and denoising
      trajectory depth (in flow-matching models) affect attack feasibility.
      Both are framed as research to be conducted; existing PGD/FGSM/C&W and
      token-deletion attacks serve as baselines, not contributions.
    Expected_Outcome: >
      Formal attack taxonomy grounded in VLA architecture; code repository with
      baseline + novel attacks; ≥1 publication on VLA-specific attack primitives.

  - Aim: "Aim 2 — Layered VLA-Specific Defense: Validation and Characterization"
    Maps_to: "T1-4 (defense strategies)"
    Purpose: >
      Design, implement, and empirically validate a multi-layer defense architecture
      with a defense layer that is unique to the robotic action domain and is
      rigorously baseline-compared. Remove the 'strawman defense' concern by
      providing real measured detection/FP rates and Pareto curves.
    Genuine_Contribution: >
      (A) Temporal Action Consistency Detector (TACD): an anomaly detector
      that operates over full action chunk sequences rather than individual steps,
      using a trajectory forecasting model trained on benign demonstrations to
      flag anomalous sequences. Unlike per-step kinematic-limit checking, TACD
      catches TTDA-style gradual drift (each step valid; sequence anomalous).
      The key novelty is the distinction between step-level and sequence-level
      anomaly: we will formalize when per-step detectors fail by construction and
      show TACD's complementary coverage. Threshold and FP characterization will
      be reported across embodiments and attack types as part of the evaluation.
      (B) Action-Grounded Adversarial Fine-Tuning (AGAT): an adversarial
      training procedure using ABBP-style perturbations (kinematically constrained
      to VLA action spaces) as data augmentation during fine-tuning — analogous
      to PGD-based adversarial training but with VLA-specific constraint structure.
      Both layers will be evaluated against ≥3 baselines: input smoothing,
      standard (VLM-ported) adversarial training, and ensemble voting.
      We reframe the action-space anomaly detector honestly as a layered
      safety+security filter, not a sole defense, and explicitly note it does
      not address poisoning or privacy attacks.
    Expected_Outcome: >
      Validated defense stack with detection rate / FP rate Pareto curves and
      comparison table; ≥1 publication on VLA-specific defense.

  - Aim: "Aim 3 — Cross-Modal and Physical Attack Propagation"
    Maps_to: "T2 (multimodal attacks)"
    Purpose: >
      Develop tightly-coupled multimodal adversarial attacks that exploit the
      vision-language grounding mechanism in VLA architectures and evaluate
      cross-embodiment transferability.
    Genuine_Contribution: >
      Tightly-coupled multimodal attack design exploiting the joint distribution
      of visual and textual representations in VLA policies — specifically the
      intermediate vision-language alignment layers (FiLM, Q-Former, dual
      ViT encoders in OpenVLA). The 'tightly-coupled' property refers to
      adversarial examples designed so that the visual perturbation and textual
      perturbation co-reinforce each other at the grounding layer, rather than
      operating independently. We will empirically test whether such coupling
      increases cross-embodiment transferability vs. independent perturbations.
      Physical attention hijacking (visual adversarial patches targeting
      spatial grounding) will be studied as a physical-world variant.
    Expected_Outcome: >
      Cross-modal attack framework; transferability matrix across ≥4 model ×
      embodiment pairs; ≥1 publication on multimodal VLA attack propagation.

  - Aim: "Aim 4 — Security Benchmarks, Interpretability, and Transferability Framework"
    Maps_to: "T3 (safety + interpretability)"
    Purpose: >
      Establish the first publicly released VLA security benchmark suite with
      physically-grounded metrics, a full cross-model transferability matrix,
      and action-level interpretability tools that help explain why attacks
      succeed or defenses fail.
    Genuine_Contribution: >
      (A) VLA-SecBench: a benchmark suite integrating task-success-rate under
      attack as primary metric, with secondary metrics — maximum end-effector
      displacement, safety-zone violation rate, force-threshold violation count —
      reported as mean ± std over ≥10 runs. Covers ≥3 model families ×
      ≥2 embodiment classes × ≥4 attack types. Extends and complements
      concurrent work (li2025attackvla, sun2026maniparena).
      (B) Transferability Matrix: systematic $M_i \times M_j \times A_k$
      analysis of attack transfer across model pairs and attack types, addressing
      the reviewer's explicit request and providing the community with a
      structured understanding of cross-model vulnerability.
      (C) Spatial-Action Interpretability Tool: adapts spatial-grounding
      attribution methods (gradient-based + inference-based) to the VLA action
      domain — explaining which visual/linguistic features most influence
      predicted action tokens under normal and adversarial conditions.
    Expected_Outcome: >
      Open-source benchmark suite; transferability matrix report; interpretability
      tool; ≥1 publication + workshop at robotics or security venue.
```

---

## Part 4 — Hypotheses

```yaml
Hypotheses:
  - Aim: "Aim 1"
    Hypothesis: >
      Action-bin quantization in VLA models (uniform 256-bin discretization
      per dimension) creates an attack surface structurally distinct from
      language tokenization: the semantic continuity across adjacent bins
      and the kinematic coupling across action dimensions allow an adversary
      with gradient access to engineer trajectory-redirecting perturbations
      at lower perturbation budget than equivalent distortions on language
      token spaces. Temporal chunk generation creates an additional
      trajectory-drift vulnerability absent in single-output VLMs.
    Success_Conditions: >
      ABBP achieves ≥20% higher task-failure rate than PGD baseline
      at equivalent L∞ perturbation budget on ≥2 model × task combinations;
      TTDA causes task failure without triggering per-step kinematic-limit
      checks on ≥1 flow-matching model (pi-0 or similar).
    Note: "These are experimental targets framing what 'success' means — not claims of results already obtained."

  - Aim: "Aim 2"
    Hypothesis: >
      A multi-layer defense (TACD + AGAT) achieves meaningfully higher
      detection of TTDA-style drift attacks — which per-step anomaly detectors
      miss by construction — and better clean-accuracy/robustness tradeoff
      than porting VLM defenses directly to VLA settings.
    Success_Conditions: >
      TACD detection rate ≥70% at ≤5% FP on ≥2 model × embodiment pairs
      for TTDA-style attacks; AGAT shows ≥10% robustness improvement over
      standard VLM-ported adversarial training at matched computational cost.
    Note: "Thresholds are reviewer-informed targets for experimental design, not pre-claimed results."

  - Aim: "Aim 3"
    Research_Questions:
      - "RQ3a: Do tightly-coupled multimodal perturbations (joint visual-language) achieve higher cross-embodiment transferability than independently designed unimodal perturbations?"
      - "RQ3b: What vision-language grounding components (FiLM, Q-Former, dual ViT encoders) are most responsible for the cross-modal coupling that enables successful multimodal attacks?"

  - Aim: "Aim 4"
    Research_Questions:
      - "RQ4a: Is task-success-rate under attack monotonically correlated with action-token deviation metrics? (Tests the validity of 30%-threshold proxy.)"
      - "RQ4b: Which attack types transfer most reliably across model families, and does transferability scale with architectural similarity?"
      - "RQ4c: Can spatial-grounding attribution tools reliably identify which input regions are responsible for adversarially-induced action changes?"
```

---

## Part 5 — Staged Scope: MVP vs. Scale-Up

### 5.1 Rationale for Staging

The panel's feasibility concern is that the original scope — 6 robots, 6 embodiments, 15 datasets, 5+ model families, 12+ attack types, full defense suite, interpretability, real-robot experiments — reads as a 2–3 person, 6-year effort. The staged approach preserves all aims and methods; nothing is cut, only sequenced. This converts the infeasibility concern into a defensible 4-year, 2-investigator plan. The generalizability claims are preserved because:
- OpenVLA and Octo represent architecturally distinct VLA families (single-encoder VLM-based vs. multi-modal transformer with diffusion head) — results on these two generalize claims about autoregressive vs. diffusion-based policies.
- Xarm7 (7-DOF arm, real) and Google robot / Simpler sim represent real vs. simulated embodiments — results generalize claims about sim-to-real and physical consequence.
- Scale-up in Years 3-4 validates generalization to a third architectural family (flow-matching / pi-0) and a morphologically distinct embodiment class (quadruped or bimanual).

### 5.2 Minimum Viable Research (Years 1–2)

```yaml
MVP_Scope:
  Models:
    - OpenVLA (7B, Prismatic VLM, dual ViT encoder + LLaMA-2; open; white-box tractable)
    - Octo (27-93M, transformer + diffusion head; open; fine-tunable)
    Rationale: >
      Both are fully open, reproduced in existing preliminary work, architecturally
      complementary (autoregressive vs. diffusion), and avoid RT-2 (55B) and proprietary
      model reproducibility concerns flagged by reviewers.
  Embodiments:
    - Xarm7 (real robot, 7-DOF; existing hardware; PI/Co-PI access confirmed)
    - Google robot via Simpler benchmark (sim; existing infrastructure)
    Rationale: >
      Matches existing preliminary setup; minimizes new hardware acquisition risk.
  Tasks:
    - Extend existing 3-sim (Close Drawer, Move Closer, Pick Coke Can) and
      3-real (Stack Cubes, Duck in Bowl, Sweep) to ≥10 tasks total
    - Add ≥4 new tasks to support transferability matrix and sufficient
      sample diversity for statistical significance
  Attacks:
    - Baselines: PGD, FGSM, C&W (white-box), token deletion (black-box) — ported from VLM literature
    - Novel: ABBP (Aim 1A) and TTDA (Aim 1B) — to be developed in Y1
  Defense:
    - TACD (Aim 2A) with preliminary detection/FP evaluation
    - AGAT (Aim 2B) with baseline comparison
    - Baselines: input smoothing, VLM-ported adversarial training, ensemble voting
  Statistical_rigor:
    - ≥10 runs per experiment, multiple seeds, mean ± std, Welch's t-test
    - Task-success-rate under attack as primary metric; derive 30%-deviation
      threshold from physical consequence mapping or replace with TSR

MVP_Deliverables:
  - "Novel VLA-specific attack code (ABBP + TTDA) with baseline comparison"
  - "Validated defense stack (TACD + AGAT) with detection/FP Pareto curves"
  - "≥2 publications: (1) attack primitives; (2) defense validation"
  - "Prototype VLA-SecBench on 2-model × 2-embodiment × 4-attack slice"
  - "OSF pre-registration for all Year-2 experiments"
```

### 5.3 Scale-Up Research (Years 3–4)

```yaml
ScaleUp_Scope:
  Add_Models:
    - pi-0 or equivalent flow-matching VLA (motivates TTDA in denoising trajectory space)
    - ACT or RoboCat as vision-only policy (controls for language modality)
    - RT-2 / OpenVLA-OFT via API (cloud; no full white-box; tests black-box and transfer)
  Add_Embodiments:
    - Franka arm (bimanual scenario) or Spot (quadruped locomotion)
    - Provides morphologically distinct embodiment class for generalizability
  Add_Tasks:
    - Locomotion and navigation tasks (quadruped or mobile base)
    - Multi-step compositional tasks requiring sequential sub-task completion
  New_Attacks:
    - Aim 3 (T2) multimodal tightly-coupled attacks
    - Physical adversarial patches in real-robot settings
  New_Defenses:
    - Certified robustness via randomized smoothing (seferis2025randomized)
    - Backdoor token reconstruction (li2026whenattention)
    - Full Pareto frontier analysis: robustness vs. computational cost
  Benchmarks:
    - Full transferability matrix (≥3 models × ≥2 embodiments × ≥4 attack types)
    - T3 complete: VLA-SecBench public release, spatial-action interpretability tool
    - Comparison with AttackVLA (li2025attackvla) and ManipArena (sun2026maniparena)
  Deliverables_Y3_Y4:
    - "Full VLA-SecBench v1.0 public release"
    - "Transferability matrix paper"
    - "Multimodal attack paper (T2)"
    - "Interpretability tool + benchmark paper (T3)"
    - "SaTC curriculum modules with attack/defense labs"
```

---

## Part 6 — Work Packages

```yaml
Work_Packages:

  - Name: "WP0 — Infrastructure and Repository"
    Aim: "Supporting all aims"
    Lead: "Co-PI (robot infrastructure); PI (model pipeline)"
    Objective: >
      Build and maintain the multi-embodiment data/model repository;
      establish computing infrastructure; set up reproducibility framework.
    Inputs: "Existing OXE datasets, OpenVLA/Octo checkpoints, Simpler benchmark, Xarm7 hardware"
    Outputs: "Dataset repository; fine-tuned model zoo; CI/CD pipeline for experiment reproducibility"
    Timeline: "Y1Q1–Y1Q3 (initial); maintained throughout"

  - Name: "WP1 — Attack Primitive Development"
    Aim: "Aim 1"
    Lead: "PI (ABBP formal design + gradient-based implementation); Co-PI (TTDA temporal formulation + chunk-level analysis)"
    Objective: >
      Design, implement, and validate ABBP and TTDA; implement baselines
      (PGD/FGSM/C&W, token deletion) as comparison; conduct white- and
      gray/black-box evaluations on MVP scope.
    Inputs: "WP0 model zoo; formal attack models; 02_v2.tex T1-1/T1-2/T1-3"
    Outputs: "Attack code library; baseline comparison results; attack novelty paper"
    Timeline: "Y1Q2–Y2Q2"

  - Name: "WP2 — Defense Development and Validation"
    Aim: "Aim 2"
    Lead: "PI (AGAT adversarial training); Co-PI (TACD temporal detector + real-robot FP testing)"
    Objective: >
      Design, implement, and empirically validate TACD and AGAT;
      compare against ≥3 baselines; characterize detection/FP Pareto curves
      per embodiment and attack type.
    Inputs: "WP1 attack library; WP0 model zoo"
    Outputs: "Defense code library; Pareto curve figures; defense paper"
    Timeline: "Y1Q3–Y2Q4"

  - Name: "WP3 — Evaluation Rigor and Statistical Framework"
    Aim: "Aims 1, 2, 4"
    Lead: "PI (metric design, statistical analysis); Co-PI (physical metric instrumentation)"
    Objective: >
      Establish the physically-grounded evaluation protocol (TSR, EE displacement,
      safety-zone violation); implement ≥10-run statistical reporting with std and
      significance tests; replace the 30%-deviation threshold with physically-derived
      justification or TSR as primary metric.
    Inputs: "WP1/WP2 results; ManipArena protocol"
    Outputs: "Evaluation framework code; physical metric instrumentation protocol"
    Timeline: "Y1Q2–Y2Q1 (framework); applied throughout"

  - Name: "WP4 — Multimodal Attack Propagation"
    Aim: "Aim 3"
    Lead: "PI (formal coupling design); Co-PI (physical patch implementation)"
    Objective: >
      Develop tightly-coupled visual-language adversarial attack; evaluate against
      independent unimodal baselines; test cross-embodiment transferability.
    Inputs: "WP1 (attack baselines), WP0 (scale-up models)"
    Outputs: "Multimodal attack code; transferability analysis; T2 paper"
    Timeline: "Y3Q1–Y3Q4"

  - Name: "WP5 — Benchmark Suite and Transferability Matrix"
    Aim: "Aim 4"
    Lead: "PI (benchmark design, transferability analysis); Co-PI (physical evaluation execution)"
    Objective: >
      Build VLA-SecBench; construct full transferability matrix; develop and
      validate spatial-action interpretability tool.
    Inputs: "WP1/WP2/WP4 results; scale-up models (WP0)"
    Outputs: "VLA-SecBench v1.0 (open source); transferability matrix; T3 paper; interpretability tool"
    Timeline: "Y3Q2–Y4Q4"

  - Name: "WP6 — Education and Broader Impacts"
    Aim: "Broader impacts"
    Lead: "PI (curriculum); Co-PI (robotics lab component)"
    Objective: >
      Develop SaTC-aligned curriculum modules, hands-on attack/defense labs,
      and workshops for undergraduates and high school students.
    Inputs: "Research findings from WP1–WP5"
    Outputs: "Curriculum modules; lab materials; workshop events"
    Timeline: "Y2Q2–Y4Q4"
```

---

## Part 7 — Task Breakdown

```yaml
Tasks:

  WP0_Tasks:
    - Task: "WP0-T1 — Fine-tune OpenVLA and Octo on Xarm7 + Simpler tasks"
      Deliverable: "Reproducible baseline models + training scripts"
      Lead: "Co-PI"
      Dependency: "Hardware access; Simpler benchmark"
      Timeline: "Y1Q1–Y1Q2"

    - Task: "WP0-T2 — Expand task suite to ≥10 tasks (add ≥4 new tasks)"
      Deliverable: "Extended task suite with balanced embodiment coverage"
      Lead: "Co-PI"
      Dependency: "WP0-T1"
      Timeline: "Y1Q2–Y1Q3"

    - Task: "WP0-T3 — Computing infrastructure setup (GPU cluster access, cloud API for RT-2)"
      Deliverable: "Reproducibility CI/CD; allocation confirmed"
      Lead: "PI"
      Dependency: "Budget approval"
      Timeline: "Y1Q1"

    - Task: "WP0-T4 — Scale-up model zoo (pi-0, ACT, RT-2 API)"
      Deliverable: "Extended model zoo with Year-3 models"
      Lead: "Co-PI"
      Dependency: "Model availability; compute"
      Timeline: "Y3Q1"

  WP1_Tasks:
    - Task: "WP1-T1 — Formalize ABBP attack: bin-boundary sensitivity analysis, Jacobian constraint"
      Deliverable: "Formal attack specification + theoretical analysis draft"
      Lead: "PI"
      Dependency: "WP0-T1"
      Timeline: "Y1Q2"

    - Task: "WP1-T2 — Implement ABBP on OpenVLA (EfficientNet + ViT encoder targets)"
      Deliverable: "ABBP attack code; comparison to PGD/C&W baseline on ≥2 tasks"
      Lead: "PI"
      Dependency: "WP1-T1"
      Timeline: "Y1Q3"

    - Task: "WP1-T3 — Formalize TTDA: temporal chunk dependency analysis on Octo + pi-0"
      Deliverable: "TTDA formal model; sufficient conditions for per-step detection bypass"
      Lead: "Co-PI (temporal analysis) + PI (formal model)"
      Dependency: "WP0-T1"
      Timeline: "Y1Q3–Y1Q4"

    - Task: "WP1-T4 — Implement TTDA on Octo (diffusion head temporal exploitation)"
      Deliverable: "TTDA code; task-failure vs. perturbation-budget curve"
      Lead: "Co-PI"
      Dependency: "WP1-T3"
      Timeline: "Y2Q1"

    - Task: "WP1-T5 — Implement baseline attacks (PGD, FGSM, C&W, token deletion) as comparison"
      Deliverable: "Baseline attack library; unified evaluation harness"
      Lead: "PI"
      Dependency: "WP0-T1"
      Timeline: "Y1Q2–Y1Q3"

    - Task: "WP1-T6 — Run white-box + gray-box comparative evaluation (ABBP vs. baselines)"
      Deliverable: "Results table; statistical analysis; attack novelty paper draft"
      Lead: "PI"
      Dependency: "WP1-T2, WP1-T5, WP3-T1"
      Timeline: "Y2Q1–Y2Q2"

    - Task: "WP1-T7 — Black-box transfer evaluation (TTDA cross-model transfer on MVP scope)"
      Deliverable: "Transfer results; preliminary transferability matrix slice"
      Lead: "PI"
      Dependency: "WP1-T4, WP1-T5"
      Timeline: "Y2Q2–Y2Q3"

  WP2_Tasks:
    - Task: "WP2-T1 — Design TACD: trajectory forecasting model trained on benign demonstrations"
      Deliverable: "TACD architecture spec; training data protocol"
      Lead: "Co-PI (trajectory model) + PI (anomaly threshold design)"
      Dependency: "WP0-T2 (extended task suite for benign demonstrations)"
      Timeline: "Y1Q3–Y1Q4"

    - Task: "WP2-T2 — Implement and train TACD on Xarm7 + Simpler embodiments"
      Deliverable: "Trained TACD models; detection/FP rate on TTDA examples"
      Lead: "Co-PI"
      Dependency: "WP2-T1, WP1-T4"
      Timeline: "Y2Q1–Y2Q2"

    - Task: "WP2-T3 — Design AGAT: VLA-specific adversarial training with ABBP perturbations"
      Deliverable: "AGAT fine-tuning procedure; ablation vs. standard adversarial training"
      Lead: "PI"
      Dependency: "WP1-T2"
      Timeline: "Y1Q4–Y2Q1"

    - Task: "WP2-T4 — Implement ≥3 baseline defenses (input smoothing, VLM-ported adv training, ensemble)"
      Deliverable: "Baseline defense library"
      Lead: "PI"
      Dependency: "WP0-T1"
      Timeline: "Y1Q3–Y2Q1"

    - Task: "WP2-T5 — Comparative evaluation: TACD + AGAT vs. baselines on ABBP + TTDA attacks"
      Deliverable: "Defense paper; Pareto curve figures; detection rate tables"
      Lead: "PI (analysis) + Co-PI (real-robot FP measurement)"
      Dependency: "WP2-T2, WP2-T3, WP2-T4, WP3-T1"
      Timeline: "Y2Q3–Y2Q4"

    - Task: "WP2-T6 — Scale-up defense evaluation (randomized smoothing, backdoor token reconstruction)"
      Deliverable: "Extended defense comparison; certified robustness bounds"
      Lead: "PI"
      Dependency: "WP0-T4, WP2-T5"
      Timeline: "Y3Q2–Y3Q4"

  WP3_Tasks:
    - Task: "WP3-T1 — Physically-grounded metric implementation: TSR, EE displacement, safety-zone violation"
      Deliverable: "Metric instrumentation code; justification for/against 30% threshold vs. TSR"
      Lead: "Co-PI (physical instrumentation) + PI (statistical framework)"
      Dependency: "WP0-T1"
      Timeline: "Y1Q2–Y1Q3"

    - Task: "WP3-T2 — Statistical reporting framework: ≥10 runs, std, Welch's t-test automation"
      Deliverable: "Statistical analysis pipeline; reporting template"
      Lead: "PI"
      Dependency: "WP3-T1"
      Timeline: "Y1Q3"

    - Task: "WP3-T3 — OSF pre-registration for Year-2 experiments"
      Deliverable: "Pre-registration documents"
      Lead: "PI"
      Dependency: "WP1-T6 protocol finalized"
      Timeline: "Y2Q1"

  WP4_Tasks:
    - Task: "WP4-T1 — Design tightly-coupled multimodal attack: joint visual-language coupling at grounding layer"
      Deliverable: "Formal coupling design; architectural analysis of FiLM / Q-Former coupling"
      Lead: "PI"
      Dependency: "WP1-T6 (baseline established)"
      Timeline: "Y3Q1"

    - Task: "WP4-T2 — Implement and evaluate multimodal attack (T2) on Year-3 model scope"
      Deliverable: "Multimodal attack code; comparison to independent unimodal baselines"
      Lead: "PI (design) + Co-PI (physical patch variant)"
      Dependency: "WP4-T1, WP0-T4"
      Timeline: "Y3Q2–Y3Q3"

    - Task: "WP4-T3 — Cross-embodiment transferability evaluation for multimodal attacks"
      Deliverable: "Transferability data feeding into WP5 matrix"
      Lead: "PI"
      Dependency: "WP4-T2"
      Timeline: "Y3Q3–Y3Q4"

  WP5_Tasks:
    - Task: "WP5-T1 — Assemble VLA-SecBench v0.5 (MVP slice: 2 models × 2 embodiments × 4 attacks)"
      Deliverable: "Benchmark prototype; internal evaluation"
      Lead: "PI"
      Dependency: "WP1-T6, WP2-T5, WP3-T2"
      Timeline: "Y2Q4"

    - Task: "WP5-T2 — Full transferability matrix construction (≥3 models × ≥2 embodiments × ≥4 attack types)"
      Deliverable: "Transferability matrix table + analysis; paper draft"
      Lead: "PI (analysis); Co-PI (multi-embodiment runs)"
      Dependency: "WP1-T7, WP4-T3, WP0-T4"
      Timeline: "Y3Q4–Y4Q2"

    - Task: "WP5-T3 — Spatial-action interpretability tool: gradient + inference-based attribution"
      Deliverable: "Interpretability tool code; validation on ≥2 attack cases"
      Lead: "PI"
      Dependency: "WP5-T1"
      Timeline: "Y3Q3–Y4Q1"

    - Task: "WP5-T4 — VLA-SecBench v1.0 public release"
      Deliverable: "Benchmark suite; documentation; hosting on GitHub/HuggingFace"
      Lead: "PI"
      Dependency: "WP5-T2, WP5-T3"
      Timeline: "Y4Q2–Y4Q3"

    - Task: "WP5-T5 — T3 benchmark paper submission"
      Deliverable: "Benchmark paper (venue TBD: ICRA/CoRL/S&P/USENIX)"
      Lead: "PI + Co-PI"
      Dependency: "WP5-T4"
      Timeline: "Y4Q3"

  WP6_Tasks:
    - Task: "WP6-T1 — Develop VLA security curriculum module (undergraduate level)"
      Deliverable: "Lecture slides; lab assignments"
      Lead: "PI"
      Dependency: "WP1-T6 results available"
      Timeline: "Y2Q2–Y2Q4"

    - Task: "WP6-T2 — Adversarial robotics lab (hands-on ABBP + defense exercises)"
      Deliverable: "Lab materials; student evaluation rubric"
      Lead: "Co-PI (robot component) + PI (attack component)"
      Dependency: "WP0 infrastructure; WP1-T2"
      Timeline: "Y2Q3–Y3Q1"

    - Task: "WP6-T3 — Workshop / seminar (annual SaTC PI meeting presentation + community workshop)"
      Deliverable: "Workshop proceedings; community engagement"
      Lead: "PI"
      Timeline: "Y2Q4, Y3Q4, Y4Q4"
```

---

## Part 8 — Dependency Graph

```yaml
Dependencies:
  Critical_Path:
    - "WP0-T1 (baseline models) → WP1-T2 (ABBP impl) → WP1-T6 (attack eval) → WP2-T5 (defense eval) → WP5-T1 (benchmark v0.5)"
    - "WP0-T1 → WP1-T3 (TTDA formal) → WP1-T4 (TTDA impl) → WP2-T2 (TACD) → WP2-T5 → WP5-T1"
    - "WP5-T1 → WP5-T2 (transferability) → WP5-T4 (v1.0 release) → WP5-T5 (T3 paper)"

  Parallel_Opportunities:
    - "WP0-T1 and WP0-T3 (computing setup) run in parallel — Y1Q1"
    - "WP1-T1 (ABBP formal) and WP1-T3 (TTDA formal) run in parallel — Y1Q2-Q3 — PI and Co-PI respectively"
    - "WP2-T3 (AGAT design) runs in parallel with WP2-T1 (TACD design) — Y1Q4"
    - "WP2-T4 (baseline defenses) runs in parallel with WP2-T1/T3 — Y1Q3-Y2Q1"
    - "WP3-T1/T2 (metric framework) runs in parallel with WP1-T5 (baseline attacks) — Y1Q2-Q3"
    - "WP4 (multimodal) runs in parallel with WP5-T1/T2 starting Y3"
    - "WP6-T1 (curriculum) runs in parallel with WP1-T6/WP2-T5 starting Y2Q2"

  Key_Sequential_Constraints:
    - "WP5-T2 (full transferability) REQUIRES WP0-T4 (scale-up models) — must not start before Y3Q1"
    - "WP4-T2 (multimodal attack) REQUIRES WP1-T6 baseline established — Y2Q2 gate"
    - "WP2-T2 (TACD) REQUIRES WP1-T4 (TTDA examples exist) — Y2Q1"
    - "Real-robot experiments (Co-PI) REQUIRE Xarm7 availability and safety clearance"
```

---

## Part 9 — Evaluation Plan

### 9.1 Addressing Reviewer Weaknesses Directly

```yaml
Evaluation_Plan:

  Aim_1_Attack_Novelty:
    Primary_Metric: "Task Success Rate under attack (TSR_att) — binary task completion"
    Secondary_Metrics:
      - "Attack Success Rate (action token deviation > empirically-derived threshold)"
      - "Maximum end-effector trajectory displacement (meters) under attack"
      - "Perturbation budget required (L∞ norm) to achieve ≥50% TSR reduction"
    Baselines:
      - "PGD (Madry et al., white-box)"
      - "FGSM (Goodfellow et al., white-box)"
      - "C&W (Carlini & Wagner, white-box)"
      - "Token deletion / random token replacement (black-box, our existing results)"
      - "Trajectory-level redirection (puthumanaillam2026trajectory — VERIFY)"
      - "Flow-matching denoising attack (tae2026drift — VERIFY)"
    Success_Criteria: >
      ABBP achieves statistically significant (p<0.05, Welch's t-test) higher
      TSR reduction than PGD at matched L∞ budget on ≥2 model × task pairs.
      TTDA bypasses per-step kinematic checks on ≥1 flow-matching model.
    Statistical_Reporting: "Mean ± std over ≥10 runs, multiple seeds, Welch's t-test"
    Addressing_Reviewer_Concern: >
      Directly addresses 'attacks are ported from VLM without VLA-specific novelty':
      side-by-side comparison with ported baselines using shared evaluation harness.

  Aim_2_Defense_Validation:
    Primary_Metric: "Detection Rate vs. False-Positive Rate (Pareto curves per attack type)"
    Secondary_Metrics:
      - "Robustness accuracy: TSR under attack after defense applied"
      - "Clean accuracy degradation (compared to undefended baseline)"
      - "Computational overhead (inference time increase, %)"
    Baselines:
      - "Input smoothing (Gaussian noise preprocessing)"
      - "Standard adversarial training (PGD-AT, VLM-ported)"
      - "Ensemble voting (2-model majority)"
      - "Structure-aware fine-tuning (zhang2026structure — VERIFY)"
      - "Randomized smoothing (seferis2025randomized — VERIFY)"
    Success_Criteria: >
      TACD: ≥70% detection at ≤5% FP rate for TTDA-class attacks on ≥2 model ×
      embodiment pairs. AGAT: ≥10% robustness improvement over PGD-AT at matched cost.
    Statistical_Reporting: "Same as Aim 1; additionally: Pareto frontier plots with CIs"
    Addressing_Reviewer_Concern: >
      Directly addresses 'anomaly detection lacks preliminary evidence':
      explicit detection/FP numbers and baseline comparison table.

  Aim_3_Multimodal:
    Primary_Metric: "TSR_att for multimodal vs. unimodal attacks"
    Secondary_Metrics:
      - "Cross-embodiment transferability rate (%)"
      - "Cross-modal benign-adversarial shift score"
    Baselines:
      - "Independent visual attack (ABBP on vision only)"
      - "Independent language attack (token deletion on text only)"
      - "Physical attention-hijacking patch (yin2026vlaguard — VERIFY)"
    Statistical_Reporting: "≥10 runs per condition; two-way ANOVA for modality × model effects"

  Aim_4_Benchmark:
    Primary_Metric_Definition: >
      Task Success Rate under Attack (TSR_att): binary success/failure judgment
      by the same 2-point scoring system used in preliminary experiments, averaged
      over ≥10 evaluation episodes per condition. This REPLACES the 30%-deviation
      proxy as primary metric. The action-deviation threshold is retained only as
      a secondary metric, justified by mapping to end-effector displacement.
    Transferability_Matrix: >
      Full matrix: M_i models (≥3) × M_j target models (≥2) × A_k attack types (≥4).
      Reports: transfer rate (%), TSR_att drop, perturbation budget scaling.
    Coverage:
      - "Models: OpenVLA, Octo, pi-0 (Y3+), ACT or RT-2-API (Y3+)"
      - "Embodiments: Xarm7 (real), Google robot/Simpler (sim), Franka or Spot (Y3+)"
      - "Attack types: ABBP, TTDA, multimodal (T2), backdoor (zhou2025badvla baseline)"
    Comparison_to_concurrent_benchmarks:
      - "AttackVLA (li2025attackvla — VERIFY): compare metric definitions and coverage"
      - "ManipArena (sun2026maniparena — VERIFY): adopt shared physical metric protocol"
    Statistical_Reporting: "All results: mean ± std over ≥10 runs; significance tests"
    Addressing_Reviewer_Concern: >
      Directly addresses 'evaluation is narrow': ≥10 tasks, ≥3 models, ≥2 embodiments,
      ≥3 baseline defenses, transferability matrix, physical metrics, statistical rigor.
```

---

## Part 10 — Deliverables

```yaml
Deliverables:

  Year_1:
    - Deliverable: "D1.1 — Reproducible MVP model zoo"
      Description: "OpenVLA + Octo fine-tuned on ≥10 Xarm7 + Simpler tasks; open-source scripts"
    - Deliverable: "D1.2 — Baseline attack library"
      Description: "PGD/FGSM/C&W/token-deletion implementations with unified evaluation harness"
    - Deliverable: "D1.3 — ABBP formal specification + initial implementation"
      Description: "Technical report or workshop paper on ABBP theory and early results"
    - Deliverable: "D1.4 — Physically-grounded evaluation framework"
      Description: "TSR, EE displacement, safety-zone violation metric code; instrumentation protocol"

  Year_2:
    - Deliverable: "D2.1 — VLA-specific attack paper (ABBP + TTDA vs. baselines)"
      Description: "Full paper: IEEE S&P / USENIX Security / CoRL / ICRA target"
    - Deliverable: "D2.2 — Defense validation paper (TACD + AGAT vs. baselines)"
      Description: "Full paper with detection/FP Pareto curves; comparative defense table"
    - Deliverable: "D2.3 — VLA-SecBench v0.5 (prototype benchmark)"
      Description: "2-model × 2-embodiment × 4-attack slice; internal release with documentation"
    - Deliverable: "D2.4 — OSF pre-registration documents"
      Description: "Pre-registration for Year-2 and Year-3 experiments"
    - Deliverable: "D2.5 — Undergraduate VLA security curriculum module"
      Description: "Lecture + lab materials; first pilot offering"

  Year_3:
    - Deliverable: "D3.1 — Multimodal attack paper (T2: tightly-coupled visual-language attacks)"
      Description: "Full paper on cross-modal VLA attacks + transferability analysis"
    - Deliverable: "D3.2 — Scale-up defense evaluation (randomized smoothing, backdoor defense)"
      Description: "Extended defense paper or journal extension"
    - Deliverable: "D3.3 — Partial transferability matrix (≥3 models × ≥2 embodiments)"
      Description: "Preprint or workshop contribution; feeds WP5-T4"

  Year_4:
    - Deliverable: "D4.1 — VLA-SecBench v1.0 (public release)"
      Description: "Full benchmark suite; GitHub/HuggingFace hosting; documentation; DOI"
    - Deliverable: "D4.2 — Transferability matrix paper"
      Description: "Full systematic study; venue: ICRA / CoRL / USENIX"
    - Deliverable: "D4.3 — T3 benchmark + interpretability paper"
      Description: "Benchmark paper + spatial-action attribution tool"
    - Deliverable: "D4.4 — Open-source attack/defense toolkit"
      Description: "Consolidated code repository; dual-use governance: delayed public release + institutional DUA"
    - Deliverable: "D4.5 — SaTC curriculum + workshop materials"
      Description: "Final curriculum with attack/defense labs, disseminated to community"
```

---

## Part 11 — Timeline (Year-by-Year with Quarter-Level Granularity)

```
YEAR 1 — Foundation and MVP Attack Development
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Q1 (Sep–Nov):
  PI:   WP0-T3 (compute infrastructure); WP1-T5 (baseline attack library)
  CoPI: WP0-T1 (fine-tune OpenVLA + Octo on Xarm7 + Simpler)
  Both: Team setup; IRB/safety protocols; OSF account registration
  Milestone: Reproducible baseline models operational; compute confirmed

Q2 (Dec–Feb):
  PI:   WP1-T1 (ABBP formalization); WP1-T5 complete; WP3-T1 start
  CoPI: WP0-T2 (expand task suite to ≥10 tasks); WP3-T1 (physical metrics)
  Both: WP3-T1 metric framework first draft
  Milestone: ABBP formal spec complete; ≥10-task suite deployed [Go/No-Go: if
             ABBP formal analysis shows no structural distinction from language
             space, pivot to Kinematic Coupling Exploitation variant]

Q3 (Jul–Aug):  [Note: US academic calendar — summer]
  PI:   WP1-T2 (ABBP implementation on OpenVLA); WP2-T4 (baseline defenses)
  CoPI: WP1-T3 (TTDA formal analysis for Octo); WP2-T1 (TACD design)
  Both: WP3-T2 (statistical framework)
  Milestone: ABBP code running; TTDA formal model complete; statistical pipeline ready

Q4 (Mar–May):  [academic spring]
  PI:   WP2-T3 (AGAT design); WP1-T6 prep (evaluation protocol locked)
  CoPI: WP1-T4 (TTDA implementation on Octo); WP2-T1 (TACD architecture)
  Both: End-of-year internal review
  Milestone: TTDA implementation running; AGAT specification complete
  Annual Deliverable: D1.1, D1.2, D1.3, D1.4

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
YEAR 2 — MVP Evaluation, Defense Validation, First Publications
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Q1 (Sep–Nov):
  PI:   WP1-T6 (attack comparative evaluation: ABBP vs. baselines); WP3-T3 (OSF prereg)
  CoPI: WP2-T2 (TACD training on Xarm7 + Simpler benign demos)
  Both: Statistical analysis pipeline deployed
  Milestone: ABBP vs. baseline results on ≥2 model × task; TSR metric validated
  [Go/No-Go: if ABBP shows <10% improvement over PGD, evaluate KCE variant or
  reframe ABBP as enhanced baseline with architectural analysis novelty]

Q2 (Dec–Feb):
  PI:   WP1-T6 complete; attack paper draft; WP1-T7 (black-box transfer)
  CoPI: WP2-T2 complete (TACD results); WP2-T5 start
  Milestone: Attack paper submitted; preliminary transferability data available

Q3 (Mar–May):
  PI:   WP2-T5 (comparative defense evaluation); paper revision/resubmit
  CoPI: WP2-T5 (real-robot FP measurement for TACD); WP6-T1 start
  Milestone: Defense paper draft complete
  [Go/No-Go: if TACD FP rate >10% on real robot, characterize causes and
  adjust threshold / feature set; report honestly rather than cherry-pick]

Q4 (Jun–Aug):
  PI:   WP2-T5 complete; WP5-T1 (VLA-SecBench v0.5); WP6-T1 complete
  CoPI: WP6-T2 start (adversarial robotics lab materials)
  Both: Annual review; SaTC PI meeting attendance and presentation
  Milestone: VLA-SecBench v0.5 prototype; curriculum module piloted
  Annual Deliverables: D2.1, D2.2, D2.3, D2.4, D2.5

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
YEAR 3 — Scale-Up Models, Multimodal Attacks, Extended Defenses
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Q1 (Sep–Nov):
  PI:   WP4-T1 (multimodal attack design); WP0-T4 coordination
  CoPI: WP0-T4 (integrate pi-0 / ACT / Franka or Spot into model zoo)
  Both: Assess Year-2 publication outcomes; adjust Year-3 scope if needed
  Milestone: Scale-up model zoo operational; multimodal attack formal design complete

Q2 (Dec–Feb):
  PI:   WP4-T2 (multimodal attack implementation); WP2-T6 (extended defenses)
  CoPI: WP4-T2 (physical patch variant); WP5-T2 start (transferability matrix)
  Milestone: Multimodal attack vs. unimodal baseline comparison; randomized smoothing eval

Q3 (Mar–May):
  PI:   WP4-T3 (cross-embodiment transferability); WP5-T3 (interpretability tool)
  CoPI: WP5-T2 (multi-embodiment runs for transferability matrix)
  Both: Multimodal paper draft
  Milestone: Transferability matrix populated for ≥3 models × ≥2 embodiments (partial)

Q4 (Jun–Aug):
  PI:   WP4-T3 complete; multimodal paper submitted; WP5-T3 interpretability validation
  CoPI: WP5-T2 running; WP6-T3 (workshop)
  Both: SaTC PI meeting; community workshop on VLA security
  Milestone: Multimodal paper submitted; interpretability tool v0.5 working
  Annual Deliverables: D3.1, D3.2, D3.3

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
YEAR 4 — Benchmark Completion, Synthesis, Open Release
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Q1 (Sep–Nov):
  PI:   WP5-T2 (transferability matrix complete); WP5-T3 (interpretability final)
  CoPI: WP5-T2 (final multi-embodiment runs); WP6-T2 finalize lab materials
  Milestone: Full transferability matrix computed; interpretability tool validated

Q2 (Dec–Feb):
  PI:   WP5-T4 (VLA-SecBench v1.0 release prep); transferability paper draft
  CoPI: WP5-T4 (benchmark integration and documentation)
  Milestone: VLA-SecBench v1.0 submitted for release [Go/No-Go: ensure all
             dual-use gating is applied before public release]

Q3 (Mar–May):
  PI:   WP5-T5 (T3 benchmark paper); D4.4 (toolkit release with DUA)
  CoPI: WP5-T5 (co-author); WP6-T3 (final workshop)
  Both: Final publications push; dissemination
  Milestone: Benchmark paper submitted; toolkit publicly available under DUA

Q4 (Jun–Aug):
  PI:   Grant closeout; final NSF reporting; knowledge transfer
  CoPI: Final robot experiments and documentation
  Both: SaTC PI meeting final presentation; community workshop
  Milestone: All deliverables complete; final report submitted
  Annual Deliverables: D4.1, D4.2, D4.3, D4.4, D4.5
```

---

## Part 12 — Milestones and Go/No-Go Decision Points

```yaml
Milestones:
  M1_Y1Q2:
    Milestone: "ABBP formal specification complete"
    Success_Criteria: "Formal distinction from VLM attack documented; bin-boundary sensitivity analysis done"
    Go_NoGo: >
      GO if structural distinction from language token space is formally supportable.
      NO-GO pivot: reframe as Kinematic Coupling Exploitation (KCE) variant, or proceed
      with ABBP as empirically demonstrated novelty without formal gap claim.

  M2_Y1Q3:
    Milestone: "MVP model zoo operational on ≥10 tasks"
    Success_Criteria: "OpenVLA + Octo baseline TSR ≥ preliminary results on existing 6 tasks"
    Go_NoGo: >
      GO if baseline performance matches preliminary experiments (confirms reproducibility).
      NO-GO: diagnose training issues before proceeding to attack evaluation.

  M3_Y2Q1:
    Milestone: "ABBP vs. baseline comparative results on ≥2 model × task pairs"
    Success_Criteria: "ABBP shows statistically significant advantage over PGD at matched L∞ budget"
    Go_NoGo: >
      GO if ABBP improvement is ≥10% TSR reduction over PGD (p<0.05).
      NO-GO: if advantage is marginal, pivot to architectural analysis of WHY
      (formalizes the null result as a finding: VLA discretization does not create
      new vulnerability class beyond continuous-domain attacks). Adjust contribution
      framing before Year-2 paper submission.

  M4_Y2Q3:
    Milestone: "TACD detection rate / FP rate characterized on TTDA attacks"
    Success_Criteria: "≥70% detection at ≤5% FP on ≥1 model × embodiment"
    Go_NoGo: >
      GO: proceed to comparative defense paper as planned.
      NO-GO (detection <50% or FP >15%): characterize failure modes; reframe TACD
      as a necessary-but-insufficient component; extend with learned threshold
      tuning per embodiment; report honestly. Do not inflate results.

  M5_Y2Q4:
    Milestone: "VLA-SecBench v0.5 prototype complete"
    Success_Criteria: "2-model × 2-embodiment × 4-attack benchmark running; documented"
    Go_NoGo: >
      GO: proceed with Year-3 scale-up as planned.
      NO-GO: if fewer than 4 attack types implemented, delay multimodal work and
      consolidate Year-3 around existing scope.

  M6_Y3Q2:
    Milestone: "Multimodal attack vs. unimodal comparison results available"
    Success_Criteria: "Tightly-coupled attack shows ≥5% higher cross-embodiment transfer than independent unimodal"
    Go_NoGo: >
      GO: proceed with T2 paper as full contribution.
      NO-GO: if coupling shows no benefit, reframe T2 as a negative result study
      characterizing when multimodal coupling helps vs. hurts — scientifically
      valid and honest contribution.

  M7_Y4Q2:
    Milestone: "VLA-SecBench v1.0 ready for public release"
    Success_Criteria: "Full benchmark with documentation; dual-use review complete; ≥3 models tested"
    Go_NoGo: >
      GO: release under institutional DUA.
      NO-GO: delay release; extend documentation and dual-use review; target Y4Q3.
```

---

## Part 13 — Risk Register

```yaml
Risks:

  - Risk: "R1 — Compute limits for large VLAs (OpenVLA 7B, pi-0, RT-2)"
    Category: "Infrastructure"
    Likelihood: "MEDIUM-HIGH"
    Impact: "HIGH (blocks white-box attacks on 7B+ models)"
    Mitigation: >
      (a) Request compute allocation (NSF ACCESS / institutional HPC) in Year-1;
      (b) white-box attacks on visual encoder only (not full 7B backbone) — valid
      threat model since encoders are shared/open;
      (c) for RT-2: use API-based black-box evaluation only (explicitly a threat
      model strength: realistic attacker assumption);
      (d) use ABBP on smaller ViT encoder (tractable) rather than end-to-end backprop.
    Fallback: >
      Scope white-box evaluation to OpenVLA encoder + Octo (27-93M);
      all large-model evaluation moves to gray/black-box.

  - Risk: "R2 — Real-robot access and availability (Xarm7 downtime, safety incidents)"
    Category: "Infrastructure / Personnel"
    Likelihood: "MEDIUM"
    Impact: "MEDIUM (delays Co-PI real-robot experiments)"
    Mitigation: >
      (a) Maintain Simpler sim as primary evaluation platform (all core results
      reproducible without real robot);
      (b) bound real-robot time to ≤20 hours/year per embodiment (physical
      validation only, not primary data);
      (c) establish safety protocols and co-PI lab rules in Y1Q1;
      (d) Co-PI brings institutional real-robot access — confirmed assumption.
    Fallback: >
      Report sim results as primary; note real-robot limitation honestly;
      transfer real-robot evaluation to Year-4 if Year-2/3 hardware issues arise.

  - Risk: "R3 — ABBP shows no structural advantage over PGD (null result on M3)"
    Category: "Technical"
    Likelihood: "MEDIUM"
    Impact: "HIGH (weakens Aim 1 novelty claim)"
    Mitigation: >
      (a) Formal analysis in Y1Q2 (M1) provides early signal — if the distinction
      is not formally supportable, pivot to TTDA as primary novel contribution
      before significant experimental investment;
      (b) In any case, TTDA (temporal chunk exploitation) remains structurally
      distinct from all VLM attacks and constitutes genuine novelty.
    Fallback: >
      Reframe Aim 1 around TTDA as primary and ABBP as empirical enhancement;
      Aim 1 contribution is 'trajectory-level' vs. 'frame-level' distinction,
      which is independently novel.

  - Risk: "R4 — TACD FP rate too high on real robot (kinematic variation)"
    Category: "Technical"
    Likelihood: "MEDIUM"
    Impact: "MEDIUM (weakens Aim 2 defense claim)"
    Mitigation: >
      (a) Conduct FP characterization on diverse benign demonstrations before
      computing detection rate — calibrate threshold per embodiment;
      (b) report full FP vs. detection tradeoff curve rather than single-point claim;
      (c) if FP remains high, reframe TACD as a forensic tool (post-hoc attack
      detection on logs) rather than an online runtime filter.
    Fallback: >
      Adjust TACD scope; ensure AGAT (adversarial fine-tuning) remains as the
      primary novel defense contribution independently.

  - Risk: "R5 — Multimodal coupling shows no transferability benefit (null result on M6)"
    Category: "Technical"
    Likelihood: "MEDIUM"
    Impact: "LOW-MEDIUM (T2 scope reduced but scientifically reportable)"
    Mitigation: >
      Pre-register hypothesis before Year-3 experiments (OSF); if null result,
      characterize when/why coupling fails; publish as a systematic negative result
      study (informative for community).
    Fallback: "Reframe T2 contribution as characterization of multimodal attack surface."

  - Risk: "R6 — Key VERIFY references do not exist as published papers"
    Category: "Research Integrity"
    Likelihood: "MEDIUM (12 of 19 candidate references unverified)"
    Impact: "MEDIUM (citation accuracy; reviewer credibility)"
    Mitigation: >
      PI must verify all 19 references in refs_v2_additions.bib before submission;
      drop any that do not resolve; replace with confirmed published alternatives.
      All unverified references are currently marked NEEDS VERIFICATION in the .bib.
    Fallback: "Report only verified methods in proposal text."

  - Risk: "R7 — Co-PI institutional change or departure"
    Category: "Personnel"
    Likelihood: "LOW"
    Impact: "HIGH (real-robot and scale-up scope at risk)"
    Mitigation: >
      (a) Core MVP scope (Years 1-2) primarily PI-led with sim evaluation;
      (b) document Co-PI contributions clearly; establish shared data/code repo;
      (c) include personnel plan in Collaboration Plan (required if >$600K combined).
    Fallback: "Reduce real-robot scope; consolidate sim-only evaluation pipeline."

  - Risk: "R8 — Budget exceeds $600K with two investigators"
    Category: "Funding Compliance"
    Likelihood: "MEDIUM (depends on Co-PI salary, fringe, indirect)"
    Impact: "HIGH (requires Collaboration Plan)"
    Mitigation: >
      PI must compute exact 4-year budget before submission.
      If total exceeds $600K, prepare NSF Collaboration Plan as supplementary document.
      If approaching $1.2M RES cap, scope real-robot hardware and Co-PI FTE accordingly.
    Fallback: "Reduce Co-PI effort or hardware acquisition; maintain MVP scope."
```

---

## Part 14 — Division of Labor

> **ASSUMPTION (marked for PI adjustment):** The Co-PI brings complementary expertise in robot learning, robotics systems, and real-robot experimentation. The specific Co-PI has NOT been named in this document. The PI should confirm Co-PI identity, institutional affiliation, and expertise coverage before submission. Adjust responsibility assignments as needed.

```yaml
Division_of_Labor:

  PI_Responsibilities:
    Expertise: "AI/ML security, adversarial ML, VLM/LLM security"
    Primary_Leads:
      - "T0: Model pipeline, training infrastructure, CI/CD"
      - "T1-1/T1-2/T1-3: Attack design and formal analysis (ABBP, TTDA theory)"
      - "T1-4: Adversarial training (AGAT) and defense porting from VLM literature"
      - "T2: Multimodal attack coupling design and formal analysis"
      - "T3: Benchmark design, transferability matrix analysis, statistical framework"
      - "Evaluation framework: metric design, statistical reporting, OSF pre-registration"
      - "Threat taxonomy and threat model development"
      - "All publications: lead author or co-lead"
      - "Education: curriculum modules"
    Supporting_Roles:
      - "Real-robot attack deployment (works with Co-PI who runs hardware)"
      - "Interpretability tool development (gradient-based methods)"

  CoPI_Responsibilities:
    Assumed_Expertise: "Robot learning, robotics systems, real-robot experimentation — ASSUMPTION"
    Primary_Leads:
      - "T0: Robot hardware setup, embodiment fine-tuning (Xarm7, Franka if added)"
      - "T1-1/T1-3: TTDA implementation on temporal/diffusion-based policies"
      - "T1-4: TACD design and real-robot false-positive characterization"
      - "Physical metric instrumentation (EE displacement, force thresholds, safety zones)"
      - "Real-robot experiment execution and safety protocols"
      - "Scale-up model integration (pi-0, Franka/Spot embodiments)"
      - "Physical patch adversarial attacks (T2 physical-world variant)"
      - "Education: adversarial robotics lab (robot component)"
    Supporting_Roles:
      - "Transferability matrix execution (multi-embodiment runs)"
      - "Benchmark data collection (robot demonstrations for TACD training)"

  Justification_of_Feasibility: >
    The two-investigator structure directly addresses M1 (scope > single-PI/4-year):
    (1) PI handles formal attack theory and ML pipeline — does not require robot
    time or hardware access, can run in parallel with Co-PI real-robot work.
    (2) Co-PI handles real-robot execution independently — does not block PI
    theoretical and simulation-based work.
    (3) Years 1-2 MVP is feasible for a single PI: Co-PI primarily provides
    infrastructure and real-robot validation. The scope expansion in Years 3-4
    leverages Co-PI's scale-up platform access.
    (4) Parallelizable tracks (see §8) are explicitly assigned to different
    investigators to prevent bottlenecks.

  Collaboration_Plan_Trigger: >
    If total combined direct costs across PI + Co-PI exceed $600K, NSF 25-515
    requires a Collaboration Plan. PI must: (a) compute exact budget; (b) if
    exceeded, prepare a 1-2 page plan describing roles, communication, shared
    resources, and conflict resolution. This plan's responsibility matrix provides
    the basis for that document.
```

---

## Part 15 — Resource Requirements

```yaml
Resources:
  Personnel:
    PI:
      - "1 summer month/year salary (years 1-4)"
    CoPI:
      - "Effort per institutional arrangement — PI to determine"
    Graduate_Students:
      - "≥2 PhD students: 1 led by PI (adversarial ML focus), 1 led by Co-PI (robotics focus)"
      - "Support: academic year RA + summer, years 1-4"
    Undergraduate_REU:
      - "1-2 REU students/year (curriculum lab development, benchmark data collection)"

  Infrastructure:
    Computing:
      - "GPU cluster access: NSF ACCESS allocation + local cluster"
      - "Minimum: 4× A100 80GB equivalent for OpenVLA 7B white-box attacks"
      - "Cloud API budget for RT-2 / large model black-box queries (Year 3-4)"
    Robot_Hardware:
      - "Xarm7 (existing Co-PI access — ASSUMPTION)"
      - "Simpler benchmark (open-source, no hardware cost)"
      - "Year-3 scale-up: Franka or Spot (Co-PI institutional access — ASSUMPTION)"
    Budget_Note: >
      GPU compute is the primary infrastructure cost driver. Single GPU node
      ($12,500 one-time, as in existing budget) may be insufficient for OpenVLA
      fine-tuning; PI should assess whether ACCESS allocation is sufficient or
      additional hardware is needed. Two-investigator structure may require
      Collaboration Plan if total >$600K.

  Data:
    - "OpenXEmbodiment (OXE) dataset (open)"
    - "Simpler benchmark demonstrations (open)"
    - "Xarm7 proprietary demonstrations (collected in WP0-T1)"
    - "Scale-up embodiment demonstrations (collected in WP0-T4)"
    - "DROID, VIMA, SPOC datasets (open; subset for fine-tuning)"
```

---

## Part 16 — Sponsor Alignment Validation

```yaml
Alignment_Validation:

  NSF_SaTC_2.0_RES_Priorities:
    "Trustworthy Computing / AI Security": >
      STRONG ALIGNMENT. Proposal directly addresses VLA security, a frontier
      AI/ML system. NIST AI RMF alignment explicit. Threat taxonomy covers
      NIST adversarial AI categories.
    "Research Experiences (RES)": >
      STRONG ALIGNMENT. REU students, curriculum modules, undergraduate labs,
      workshops. Educational integration woven throughout Y2-Y4.
    "Foundational security science (not just applied)": >
      IMPROVED ALIGNMENT vs. original. Novel ABBP/TTDA formalizations and
      TACD novelty framing provide foundational science, not just benchmarking.
    "Reproducibility / open science": >
      STRONG ALIGNMENT. OSF pre-registration, open benchmark (VLA-SecBench v1.0),
      open-source tooling with DUA.
    "Responsible disclosure / dual-use governance": >
      EXPLICIT. Attack tooling released under institutional DUA; delayed public
      release post-publication; stated in proposal.

  Strengths:
    - "Staged MVP scope directly answers feasibility concern"
    - "Two-investigator structure plausibly covers both ML security and real-robot expertise"
    - "Novel attack primitives (ABBP, TTDA) provide genuine VLA-specific science claim"
    - "Defense validation plan directly addresses 'strawman defense' concern"
    - "Evaluation rigor plan (TSR, physical metrics, ≥10 runs, baselines) addresses eval weakness"
    - "Explicit transferability matrix answers reviewer's explicit request"
    - "Benchmark (VLA-SecBench) positions proposal as infrastructure-providing for community"

  Weaknesses:
    - "ABBP/TTDA claims are ambitious — panel may require preliminary evidence (at least a formal argument). This plan does not fabricate preliminary results; the PI must generate this before submission."
    - "TACD without real detection numbers is still a potential concern — plan requires real experiments before submission"
    - "Co-PI identity and expertise not confirmed — this is an assumption that the PI must resolve"
    - "19 candidate references unverified — all must be verified before submission"
    - "Budget recomputation for 4-year, 2-PI structure remains a pre-submission blocker"
    - "Threat model / trust definition upgrade (B5 from revision_plan.md) not addressed in this plan — PI should add explicit threat-actor profiles to the proposal"
```

---

## Part 17 — Planning Summary

### Aims Summary

| Aim | Maps to | Core Novelty | Lead(s) | MVP or Scale-up |
|-----|---------|--------------|---------|-----------------|
| Aim 1 | T0, T1-1/2/3 | ABBP (bin-boundary attack) + TTDA (temporal drift) | PI (ABBP) + Co-PI (TTDA) | MVP Y1-2 |
| Aim 2 | T1-4 | TACD (sequence anomaly) + AGAT (VLA-specific adv. training) | Co-PI (TACD) + PI (AGAT) | MVP Y1-2 |
| Aim 3 | T2 | Tightly-coupled multimodal attack + physical patches | PI (formal) + Co-PI (physical) | Scale-up Y3 |
| Aim 4 | T3 | VLA-SecBench + transferability matrix + interpretability tool | PI + Co-PI | Scale-up Y3-4 |

### MVP vs. Scale-Up Split

| Dimension | Years 1–2 (MVP) | Years 3–4 (Scale-Up) |
|-----------|-----------------|----------------------|
| Models | OpenVLA + Octo | + pi-0, ACT, RT-2 API |
| Embodiments | Xarm7 (real) + Google robot/Simpler (sim) | + Franka or Spot |
| Tasks | 10+ manipulation | + locomotion, compositional, navigation |
| Attacks | ABBP + TTDA + baselines | + multimodal (T2), physical patches, backdoor |
| Defenses | TACD + AGAT + 3 baselines | + randomized smoothing, backdoor token recon |
| Benchmark | VLA-SecBench v0.5 (prototype) | VLA-SecBench v1.0 (full release) |
| Evaluation | 2 models × 2 embodiments × 4 attacks | 3+ models × 3+ embodiments × 4+ attacks + full transferability matrix |

### Top Competitiveness Improvements vs. Panel Concerns

| Panel Concern | This Plan's Response | Evidence of Improvement |
|---------------|---------------------|------------------------|
| (a) Scope exceeds single-PI feasibility | 2-investigator team with explicit division of labor; staged MVP scope Y1-2 vs. scale-up Y3-4 | Parallelizable tracks per investigator; MVP fully executable at PI pace with Co-PI support |
| (b) Attacks are ported from VLM without VLA-specific novelty | ABBP (bin-boundary quantization) and TTDA (temporal chunk drift) are structurally absent from VLM attacks; formal argument provided | Go/No-Go M3 gates this claim; TTDA remains novel even if ABBP null result |
| (c) Action-space anomaly detection lacks preliminary evidence | WP2-T2/T5 explicitly generates detection/FP Pareto curves; TACD extension to sequence-level anomaly (beyond per-step) is the specific new claim | M4 go/no-go at Y2Q3; reframed as layered filter not sole defense |
| (d) Evaluation is narrow; no baselines; no transferability | TSR as primary metric; ≥10 tasks; ≥3 baseline defenses; transferability matrix (M_i × M_j × A_k); physical metrics; ≥10 runs with std and significance test | Evaluation plan §9 directly maps to each reviewer bullet point |

### Pre-Submission Blockers (PI Must Resolve — Not in This Plan's Scope)

1. **TACD/ABBP preliminary evidence** — the plan designs experiments; the PI must run them before submission.
2. **Co-PI identity and expertise confirmation** — this entire 2-investigator structure depends on a real Co-PI being secured.
3. **Collaboration Plan** — required if combined direct costs >$600K; must be prepared if applicable.
4. **Reference verification** — all 19 candidate references in refs_v2_additions.bib must be verified against primary sources; drop any that do not resolve.
5. **Budget recomputation** — 4-year, 2-PI budget must be computed; ensure within RES cap ($1.2M total, $600K Collaboration Plan threshold).
6. **Threat model upgrade** (B5 from revision_plan.md) — explicit threat-actor profiles (white-box insider, black-box API, supply-chain, physical/sensor) must be added to the proposal; this plan does not fabricate that content.

---

*This document was produced by the Planner Agent on 2026-08-31. It is a planning instrument; no preliminary results, specific success rates, or reference details are fabricated here. All numerical targets (e.g., ≥70% detection) are framing targets for experimental design informed by panel reviewers, not claimed results.*
