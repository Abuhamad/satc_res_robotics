# Novelty & Differentiation Assessment
**Proposal:** SaTC 2.0: RES: Toward Secure and Robust Generalist Robotic Models
**Reviewer role:** Novelty Detector (skeptical senior reviewer)
**Sources reviewed:** `01_v2.tex` (Overview, Vision/Goals, Intellectual Merit, Background timeline), `02_v2.tex` (Research Plan T0–T3, threat model, preliminary studies, work plan), `sections/0_project_summary_v2.tex`, `refs.bib`, `refs_v2_additions.bib`, `artifacts/researcher_report.md`, `artifacts/writer_changelog.md`.
**Core finding up front:** The proposal's own bibliography (added by the project's Researcher agent) already documents 8–10 directly competing 2025–2026 papers that anticipate the specific mechanisms and the "first" framing claimed in the Overview and Intellectual Merit sections. The Research Plan (`02_v2.tex`) has been partially hedged in response to this ("we frame as research to be conducted," go/no-go gates), but the Overview/Intellectual Merit/Project Summary language was **not** correspondingly softened. This internal inconsistency is the single largest novelty-related reviewer risk.

---

## 1. Executive Assessment

The proposal sits in one of the fastest-moving sub-fields in ML security right now: adversarial/backdoor attacks on vision-language-action (VLA) models. Between the initial literature scan and the current proposal draft, at least three purpose-built VLA-security benchmarks/attack-taxonomy papers (`li2025attackvla` "AttackVLA", `badvla`/`zhou2025badvla`, `advvla`) and several 2026 mechanism papers targeting the exact attack surfaces claimed as novel here (`puthumanaillam2026trajectory` trajectory-level redirection, `tae2026drift` DRIFT on flow-matching VLAs, `zhang2026structure` structure-aware robust fine-tuning, `seferis2025randomized` certified robustness for VLM/VLA outputs, `li2026whenattention` backdoor-erasure via token reconstruction, `lu2026whenrobots` universal transferable patches) have already appeared in CVPR/ICCV/IROS/EMNLP-tier venues or on arXiv. Given the current date (Sept. 2026), this is not "future work to watch" — it is the existing competitive landscape at time of submission.

The proposal's differentiators are real but narrow: (1) explicit kinematic/Jacobian-consistency constraints tying perturbations to physically reachable actions, (2) grounding attack/defense success in physical-consequence metrics (end-effector displacement, safety-zone/force-threshold violations) rather than token-level proxies alone, (3) a genuinely large cross-embodiment × cross-model transferability matrix (6 embodiments, multiple model families), and (4) a single multi-task TACD model instead of per-task detectors. None of these are conceptually new mechanisms; they are careful engineering/evaluation-rigor contributions layered onto attack/defense families (PGD-style perturbation, trajectory-chunk drift, temporal-consistency detection, adversarial fine-tuning) that are already public, several from the same 2025–2026 window this proposal would compete in.

**Bottom line:** the proposal is defensible as **systematic infrastructure and rigor** (breadth, physical grounding, reproducibility, cross-embodiment scale) but is **not defensible as first-discovery** of the threat surfaces, attack primitives, or defenses it names. Reviewers with current VLA-security literature knowledge (a near-certainty on a SaTC panel in this cycle) will flag the "first comprehensive" language as an overclaim and, at worst, as evidence of an incomplete/selectively-cited related-work section, since the missing citations are already sitting in the project's own bib file.

---

## 2. Novelty Classification

**Incremental, bordering Moderately Novel** (see split rationale below).

- The *named contributions read individually* (ABBP, TTDA, TACD, AGAT) are each an incremental variant of an existing technique family (PGD/FGSM/C&W-style optimization; trajectory/chunk-level drift attacks already published as DRIFT and Trajectory-Level Redirection; temporal-consistency/anomaly detection; adversarial fine-tuning) with an added constraint or scope change.
- The *program as a whole* (systematic taxonomy + cross-modal analysis + benchmark, executed at declared scale across 6 embodiments/15 datasets with physically-grounded metrics) could reach Moderately Novel if the proposal stops claiming primacy and instead argues integration/rigor/scale as the contribution — but as currently framed ("first comprehensive... framework," "novel methodologies... previously unexplored," "first comprehensive taxonomy") it overclaims relative to what the citation record supports.

---

## 3. Technical Novelty

```yaml
Technical Novelty:
  Score: 4
  Evidence: >
    ABBP is PGD/FGSM/C&W plus a bin-boundary targeting objective and a
    kinematic Jacobian constraint (02_v2.tex explicitly frames baselines as
    "not contributions" and treats the discretization exploit as an
    open go/no-go question, not a validated mechanism). TTDA is a
    slowly-accumulating multi-step perturbation against action-chunk
    policies -- conceptually identical to the already-published
    "Trajectory-Level Redirection Attacks on VLA" (puthumanaillam2026trajectory)
    and "DRIFT: Derailing Denoising Trajectories of Flow-Matching VLAs"
    (tae2026drift), the latter of which the proposal's own Research Plan
    text says it will "build on and compare against." TACD is temporal/
    sequence-level anomaly detection, a well-studied defense pattern in
    time-series and control security, adapted to actions. AGAT is
    standard adversarial fine-tuning (LoRA rank-16) with kinematically-
    constrained perturbations, directly adjacent to zhang2026structure's
    "Structure-Aware Robust Fine-Tuning" and seferis2025randomized's
    certified-robustness extension to VLM/VLA outputs.
  Concerns: >
    No new learning architecture, optimization principle, or attack
    class is introduced; every primitive is "known technique +
    constraint/scope change." The proposal itself hedges ABBP with a
    go/no-go gate ("gated by a formal go/no-go check on whether
    action-space discretization yields a structurally distinct
    vulnerability"), which is an admission that technical novelty is
    unproven, not established.
```

## 4. Methodological Novelty

```yaml
Methodological Novelty:
  Score: 5
  Evidence: >
    Genuine methodological contributions: (1) normalizing physical
    consequence across modalities (end-effector displacement, safety-
    zone/force-threshold violation rate) instead of relying only on
    token-level proxies; (2) a full model x model x attack
    transferability matrix across 6 embodiments and multiple model
    families, which is broader in embodiment scope than most cited
    single-embodiment attack papers; (3) a single multi-task TACD model
    with per-task calibrated thresholds instead of per-task detector
    proliferation.
  Concerns: >
    sun2026maniparena ("ManiParena") already proposes a comprehensive,
    physically-grounded real-world evaluation protocol for generalist
    manipulation, undercutting the claim that physical grounding itself
    is new. li2025attackvla ("AttackVLA") already benchmarks adversarial
    AND backdoor attacks on VLA models -- the proposal must show its
    benchmark differs on axes (embodiment count, physical-consequence
    metrics, transferability matrix depth) rather than existing at all,
    and this differentiation is not explicitly argued anywhere in the
    text; it only appears as a citation.
```

## 5. Scientific Novelty

```yaml
Scientific Novelty:
  Score: 4
  Evidence: >
    The proposal poses a plausible unanswered sub-question: does
    action-space discretization (256-bin quantization) create a
    structurally distinct vulnerability class relative to token-level
    vulnerabilities already known in VLMs? This is a legitimate,
    narrowly-scoped scientific question.
  Concerns: >
    The broader scientific claims in 01_v2.tex ("uncharted threat
    landscape," "previously unexplored vulnerabilities in
    vision-language-action integration") are no longer accurate given
    badvla, advvla, li2025attackvla, puthumanaillam2026trajectory, and
    tae2026drift collectively cover backdoor, adversarial, and
    trajectory-drift vulnerabilities in VLA integration already. The
    proposal answers "is this attack surface exploitable in practice at
    scale, with kinematic realism," which is a validation/rigor question,
    not a previously-unanswered existence question.
```

## 6. Application Novelty

```yaml
Application Novelty:
  Score: 6
  Evidence: >
    Cross-embodiment scale (6 robots/embodiments, 15 datasets including
    OXE) and the explicit mapping of digital adversarial budgets to
    physical safety consequences (force-threshold and safety-zone
    violations) is a genuinely underused application framing compared
    to the single-embodiment, single-model-family scope of most cited
    2025-2026 competitors (e.g., zhang2026structure and tae2026drift
    each target one architecture family).
  Concerns: >
    Domain is not new (robot/VLA security is now an active publication
    area, not an unexplored one); the application-novelty argument
    rests entirely on breadth/scale, which is a resourcing advantage,
    not a conceptual one, and is vulnerable to "someone will just run
    the existing attack on more robots" style dismissal.
```

## 7. Impact Potential

```yaml
Impact Potential:
  Score: 6
  Evidence: >
    If VLA-SecBench is released with genuine cross-embodiment coverage,
    physical-consequence metrics, and a public transferability matrix,
    it would have real community utility regardless of who publishes
    "first" -- comparable benchmarks (ImageNet-C, RobustBench) became
    field standards through comprehensiveness and maintenance, not
    through first-mover novelty alone. NSF SaTC panels also value
    sustained community infrastructure.
  Concerns: >
    li2025attackvla and sun2026maniparena are both already positioned
    to occupy this "standard benchmark" niche; if either becomes the
    de facto community benchmark before this 4-year award concludes
    Phase 2 (VLA-SecBench v1.0 is milestone M7, Year 4), the impact
    argument weakens substantially. Impact is contingent on execution
    speed and differentiation, not guaranteed by the plan alone.
```

---

## 8. Similarity Analysis

```yaml
Closest Prior Work:
  - Contribution: "First comprehensive threat taxonomy/framework for multimodal robotic foundation models"
    Similar Work: li2025attackvla (AttackVLA, arXiv Nov 2025) -- benchmarks adversarial AND backdoor attacks on VLA models
    Similarity: Both claim systematic/benchmarking coverage of attacks against VLA models across attack classes.
    Key Difference: Proposal adds cross-embodiment scale (6 embodiments) and physical-consequence metrics not confirmed present in AttackVLA; "first" claim is not defensible given AttackVLA predates this proposal's submission cycle.

  - Contribution: "Action-Bin Boundary Perturbation (ABBP)"
    Similar Work: madry2017towards (PGD), goodfellow2014explaining (FGSM), carlini2017towards (C&W) -- explicitly named as baselines in 02_v2.tex
    Similarity: ABBP is a gradient-based Lp-bounded perturbation attack, same optimization family as the baselines.
    Key Difference: Adds a bin-boundary-crossing objective and a kinematic Jacobian consistency constraint; the proposal itself has not yet validated that this yields a smaller effective perturbation budget than the baselines (framed as an open go/no-go question).

  - Contribution: "Temporal Trajectory Drift Attack (TTDA)"
    Similar Work: puthumanaillam2026trajectory (Trajectory-Level Redirection Attacks on VLA, arXiv 2026); tae2026drift (DRIFT: Derailing Denoising Trajectories of Flow-Matching VLAs, arXiv 2026)
    Similarity: Near-identical concept -- slow, per-step-plausible perturbations that accumulate into a trajectory-level failure, exploiting the multi-step/chunked or denoising structure of modern VLA policies. tae2026drift is even conceptually named "drift," mirroring "Temporal Trajectory Drift."
    Key Difference: TTDA is scoped to chunking policies (e.g., Octo) in Phase 1 and explicitly plans to extend to flow-matching policies (pi-0) in Years 3-4 "contingent on model availability" -- i.e., the proposal's own extension target is the same territory tae2026drift already occupies now. Differentiation is not established in the text.

  - Contribution: "Temporal Action Consistency Detector (TACD)"
    Similar Work: li2026whenattention (backdoor-erasure via visual token reconstruction, arXiv 2026); zhang2026structure (Structure-Aware Robust Fine-Tuning defense, IROS 2026)
    Similarity: Sequence/trajectory-level anomaly or consistency detection as a defense against action-space and attention-based manipulation.
    Key Difference: TACD's single multi-task model with per-task calibrated thresholds (vs. per-task model proliferation) is a legitimate engineering differentiator, but it is a defense-deployment efficiency argument, not a new detection principle.

  - Contribution: "Action-Grounded Adversarial Fine-Tuning (AGAT)"
    Similar Work: zhang2026structure (Structure-Aware Robust Fine-Tuning, IROS 2026); seferis2025randomized (Randomized Smoothing Meets Vision-Language Models, EMNLP 2025)
    Similarity: All are training-time robustness interventions for VLA/VLM action outputs; AGAT is standard adversarial training (LoRA-adapted) using ABBP-style perturbations.
    Key Difference: LoRA-rank-16 compute efficiency framing is practical but not conceptually distinct from structure-aware fine-tuning; seferis2025randomized already offers a *certified* (not just empirically robust) alternative, which is a strictly stronger robustness guarantee than AGAT's empirical adversarial training.

  - Contribution: "VLA-SecBench (standardized security/safety/interpretability benchmark)"
    Similar Work: li2025attackvla (AttackVLA); sun2026maniparena (ManiParena, comprehensive real-world evaluation)
    Similarity: Both are already-published (or already-arXived) comprehensive, multi-attack/multi-model evaluation suites for VLA robustness/manipulation.
    Key Difference: Cross-model transferability matrix + spatial-action interpretability tool + explicit physical-consequence metrics (force-threshold/safety-zone violations) are plausible differentiators, but none of this differentiation is written into the proposal text as an explicit comparison; it exists only as parallel citations.
```

---

## 9. Saturation Analysis

```yaml
Field Saturation:
  Status: Active, trending toward Saturated for the specific sub-niche of "VLA adversarial/backdoor attacks and defenses"
  Justification: >
    Between 2025 and the current date (Sept. 2026), at least 8 dedicated
    VLA-security papers have appeared across CVPR, ICCV, IROS, EMNLP, and
    arXiv (badvla/zhou2025badvla, advvla, li2025attackvla,
    puthumanaillam2026trajectory, tae2026drift, zhang2026structure,
    yin2026vlaguard, lu2026whenrobots, seferis2025randomized,
    li2026whenattention). This is an 18-24 month publication burst rate
    typical of a field moving from "emerging" to "active/competitive,"
    not "underexplored." The proposal's own Overview language ("just
    beginning," "largely unexplored attack surface," "uncharted threat
    landscape") describes the state of the field as of ~2023-2024, not
    as of the current submission date. The broader end-to-end VLA
    modeling field (background timeline in 01_v2.tex, ~40 models
    2022-2025) is itself Active/Maturing, which independently increases
    competitive pressure on any security research that lags model
    releases.
```

---

## 10. Assumption Stress Test

```yaml
Assumptions:
  - Assumption: The threat landscape for VLA models is "uncharted" / "largely unexplored."
    Risk: Directly contradicted by the proposal's own bibliography (badvla, advvla, li2025attackvla and others). If a reviewer checks the citation list, this framing reads as either outdated or as understating known competing work.
  - Assumption: 256-bin action-space discretization creates a structurally distinct, exploitable vulnerability class (ABBP's core premise).
    Risk: Unvalidated by the proposal's own admission (a go/no-go gate at M1/M3). If the go/no-go fails, ABBP degenerates to "PGD with an extra constraint," collapsing a headline contribution.
  - Assumption: Kinematic/Jacobian consistency constraints meaningfully differentiate ABBP/TTDA/AGAT from prior trajectory-drift and structure-aware fine-tuning work.
    Risk: Plausible but untested; DRIFT and Trajectory-Level Redirection Attacks may already implicitly respect per-step kinematic plausibility (their abstracts describe per-step plausible perturbations), which would erase this differentiator.
  - Assumption: A "first" or "standardized" benchmark claim remains credible through a 4-year award when AttackVLA and ManiParena already exist today.
    Risk: High -- competing benchmarks may become the de facto standard well before VLA-SecBench v1.0 ships in Year 4 (M7), especially since AttackVLA is already public.
  - Assumption: Co-PI TBD for robot-learning/real-robot expertise will materialize with sufficient capacity to execute the 6-embodiment, 15-dataset scope that is the strongest differentiator.
    Risk: The scale-based differentiation argument (Application Novelty) depends entirely on execution capacity that is not yet staffed, per the proposal's own "[Co-PI: TBD]" placeholder.
```

---

## 11. Reviewer Attack Simulation

```yaml
Reviewer Attacks:
  Reviewer A: >
    (Conservative, prior-work-focused) "This proposal claims to be the
    'first comprehensive taxonomy and framework' and to reveal
    'previously unexplored vulnerabilities,' but its own reference list
    includes BadVLA, AdvVLA (ICCV 2025), and AttackVLA -- an existing
    benchmark for adversarial AND backdoor attacks on VLA models. TTDA
    is essentially indistinguishable in concept from two already-cited
    2026 papers (DRIFT, Trajectory-Level Redirection Attacks) that the
    Research Plan says it will merely 'build on and compare against.'
    This is not first-discovery research; it is a systematic replication
    and extension study, and it should be described as such. The
    overclaiming language undermines confidence in the literature review
    quality."
  Reviewer B: >
    (Methodology-focused) "ABBP is explicitly gated behind a go/no-go
    decision on whether it is even a distinct vulnerability class -- this
    is presented as a headline attack primitive in the Intellectual Merit
    section while being simultaneously hedged as unproven in the Research
    Plan. That inconsistency should be resolved before review: either the
    PI has preliminary evidence ABBP outperforms PGD/FGSM/C&W under a
    physically-normalized budget, or ABBP should not be listed as a
    pioneering contribution in the summary-level sections."
  Reviewer C: >
    (Impact-focused) "If executed at the claimed scale (6 embodiments,
    15 datasets, cross-model transferability matrix, physical-consequence
    metrics), this would be valuable community infrastructure -- but that
    value comes from comprehensiveness and maintenance, not novelty, and
    two comparably-scoped benchmarks (AttackVLA, ManiParena) already exist
    or are in progress. The proposal needs to argue why VLA-SecBench will
    become the standard rather than a third redundant option, and that
    argument is currently absent from the text."
```

---

## 12. Funding Competitiveness Analysis

```yaml
Funding Competitiveness:
  Rating: Moderate
  Justification: >
    Feasibility and infrastructure (PI's security-research track record,
    6-embodiment data mixture, prior SHIELD attack methodology) are
    strong and would support a Moderate-to-Strong feasibility rating on
    their own. However, Novelty is the binding constraint: a SaTC panel
    reviewing VLA security in this cycle will very likely include
    reviewers current on the exact 2025-2026 literature already cited
    in this proposal's own bib file, and the "first"/"uncharted"/
    "previously unexplored" framing will read as overclaiming rather
    than accurate positioning. Competitiveness is Moderate as written;
    it could reach Strong if the overclaiming is corrected and the
    scale/physical-grounding/integration argument is made explicit and
    load-bearing instead of implicit.
```

---

## 13. Novelty Risks

```yaml
Novelty Risks:
  - Risk: "First comprehensive threat taxonomy/framework for multimodal robotic foundation models" is factually contestable.
    Competing Work: li2025attackvla (AttackVLA); badvla / zhou2025badvla; advvla (ICCV 2025)
  - Risk: TTDA (temporal/trajectory drift attack) substantially overlaps an already-published attack of the same concept.
    Competing Work: puthumanaillam2026trajectory (Trajectory-Level Redirection Attacks on VLA); tae2026drift (DRIFT: Derailing Denoising Trajectories of Flow-Matching VLAs)
  - Risk: AGAT (adversarial fine-tuning defense) overlaps existing structure-aware and certified-robustness defenses that may already dominate on guarantees (certification) or scope (attention hijacking).
    Competing Work: zhang2026structure (Structure-Aware Robust Fine-Tuning); seferis2025randomized (Randomized Smoothing Meets Vision-Language Models)
  - Risk: TACD (sequence-level consistency defense) overlaps existing backdoor/attention-based detection-and-erasure defenses for robotic policies.
    Competing Work: li2026whenattention (When Attention Betrays: Erasing Backdoor Attacks by Reconstructing Visual Tokens); yin2026vlaguard (VLAGuard)
  - Risk: VLA-SecBench's "standardized benchmark" claim competes directly with an already-arXived dedicated VLA attack/backdoor benchmark.
    Competing Work: li2025attackvla (AttackVLA); sun2026maniparena (ManiParena)
  - Risk: ABBP's core mechanism (action-bin boundary crossing) has not been shown to be a structurally distinct vulnerability versus known token-level VLM attacks; the proposal's own go/no-go framing acknowledges this.
    Competing Work: Standard gradient attack literature (madry2017towards, goodfellow2014explaining, carlini2017towards) plus generic VLM discretized-output attack literature already cited in T1-1.
  - Risk: The claimed "unexplored multimodal attack surface" for vision-language coupling mechanisms (FiLM/projection-MLP/cross-attention) overlaps recent physical attention-hijacking work.
    Competing Work: zhang2026structure; yin2026vlaguard (physical attention hijacking in VLA/wireless sensor network settings)
  - Risk: Interpretability contribution (spatial-action interpretability tool) overlaps recent spatial-grounding/attribution methods for embodied models.
    Competing Work: schofield2026chain (Chain of Spatial Thoughts); jahangard2025multimodal (neuro-symbolic spatial reasoning)
  - Risk: Internal inconsistency between hedged Research Plan language ("we frame as research to be conducted," go/no-go gates) and unhedged Overview/Intellectual Merit/Project Summary claims ("first," "pioneering," "previously unexplored") creates a credibility risk independent of the underlying science.
    Competing Work: N/A (self-consistency risk, evidenced by writer_changelog.md showing 02_v2.tex was hedged post hoc while 01_v2.tex/project summary were not).
```

---

## 14. Novelty Repair Recommendations

```yaml
Novelty Repair Recommendations:
  - Recommendation: Remove or substantially soften "first comprehensive," "pioneering," "previously unexplored," and "uncharted" language in 01_v2.tex Overview/Intellectual Merit and the Project Summary; replace with claims about scale, physical grounding, and systematic cross-embodiment coverage.
    Expected Benefit: Removes the single largest, easiest-to-find reviewer objection (a direct contradiction with the proposal's own bibliography) without requiring any change to the technical plan.
  - Recommendation: Add an explicit "Relationship to Concurrent Work" paragraph or table in the Research Plan that directly compares ABBP/TTDA/TACD/AGAT/VLA-SecBench against BadVLA, AdvVLA, AttackVLA, DRIFT, Trajectory-Level Redirection Attacks, Structure-Aware Robust Fine-Tuning, and Randomized Smoothing, stating precisely what is shared and what is different (kinematic constraint, physical-consequence metric, embodiment count, single multi-task model, etc.).
    Expected Benefit: Converts implicit citations into an explicit, load-bearing novelty argument; pre-empts Reviewer A/B attacks by showing awareness and positioning rather than omission.
  - Recommendation: Resolve the ABBP go/no-go framing before submission if possible -- report even a small preliminary result showing the perturbation-budget or transferability difference from PGD/FGSM/C&W baselines, or otherwise demote ABBP from "pioneering contribution" language in the summary sections to "candidate mechanism to be validated."
    Expected Benefit: Removes the internal inconsistency Reviewer B is likely to flag and gives the panel concrete evidence rather than a promise.
  - Recommendation: Reframe the central contribution around scale and physical-consequence grounding as the primary novelty axis (6 embodiments, 15 datasets, end-effector displacement / safety-zone / force-threshold metrics, single multi-task TACD) rather than around attack/defense primitives that have close 2025-2026 analogs.
    Expected Benefit: Shifts the reviewer's evaluation criterion from "is this mechanism new" (where the proposal is weak) to "is this the most comprehensive, physically-realistic, reproducible evaluation infrastructure" (where the proposal is comparatively strong).
  - Recommendation: Consider an explicit differentiation argument against certified-robustness defenses (seferis2025randomized): either argue why empirical adversarial training (AGAT) is preferable in this deployment setting (e.g., latency/compute budget under the stated 3-10Hz real-time constraint, where randomized smoothing's multi-sample inference cost may be prohibitive), or add a certified-robustness baseline comparison.
    Expected Benefit: Converts a currently-unaddressed "stronger competing guarantee" risk into an argued, defensible design choice.
  - Recommendation: Note the field-saturation trend explicitly in the Background section (rapid 2025-2026 publication burst) and use it to justify urgency/timing rather than let a panel discover it as an inconsistency.
    Expected Benefit: Reframes a novelty liability ("this field is crowded") into a motivation asset ("this field is moving fast and needs standardized, physically-grounded infrastructure now").
```

---

## 15. Proposal Advancement Decision

```yaml
Decision: Major Revision Required
Rationale: >
  Overall Novelty (4/10) falls below the Advance-With-Revisions threshold
  (>=7) and Impact (6/10) is below the Advance threshold (>=8), placing
  this squarely in Major Revision territory per the stated thresholds.
  The revision required is primarily rhetorical/positioning (remove
  "first"/"uncharted" claims, add explicit concurrent-work
  differentiation, resolve the ABBP hedging inconsistency) rather than a
  fundamental redesign of the research plan -- the underlying
  scale/physical-grounding/cross-embodiment program has a credible,
  though not transformative, novelty case if reframed. Left unreframed,
  an expert SaTC panel with current VLA-security literature knowledge
  (highly likely given the field's publication rate) would very plausibly
  score this Novelty <5 and move it to Reject and Reframe, since the
  "first comprehensive" claim is directly falsifiable from the
  proposal's own citations.
```

---

## 16. Novelty Scorecard

```yaml
Novelty Scorecard:
  Technical Novelty: 4
  Methodological Novelty: 5
  Scientific Novelty: 4
  Application Novelty: 6
  Impact Potential: 6
  Funding Competitiveness: 5

Summary Scores (as requested):
  Novelty: 4
  Impact: 6
  Differentiation: 4
```
