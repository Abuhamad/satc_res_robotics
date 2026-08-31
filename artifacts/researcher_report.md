# Methods Coverage Report: Security and Trustworthiness of VLA Robot Foundation Models

*Note: Citation details are derived from live web search and knowledge bounding up to August 2026. Author lists are accurate to the first primary author.*

## Executive Research Overview
This report maps the current state-of-the-art methodology intersecting adversarial machine learning and embodied intelligence (Vision-Language-Action models). While early attacks on VLM-controlled robots relied on image-level perturbations (PGD/FGSM), the 2025-2026 landscape features domain-specific attacks targeting trajectory-level behavior, spatial grounding, physical patch transferability, and backdoor methodologies.  Corresponding defenses have shifted from static VLM token filtering to structure-aware fine-tuning, randomized smoothing applied to action spaces, and objective-decoupled backdoors.  

## 1. Adversarial Attacks on VLA / Embodied Policies
**Gap:** Current proposal tasks (T1-1, T2) rely on dated methods (PGD, FGSM, C&W, and basic jailbreaking). Methods must reflect physical attention hijacking and modality-specific derailing techniques.

* **Trajectory-Level Redirection Attacks**
  * **Venue/Year:** arXiv, 2026 (Puthumanaillam et al.)
  * **Description:** Attacks that steer VLA policies to deviate dynamically at the trajectory level rather than static single-frame misclassification.
  * **Location:** T1-1 (White/Gray-box attacks)
  * **Priority:** HIGH
  * **BibKey:** puthumanaillam2026trajectory

* **Physical Attention Hijacking (VLAGuard/Structure-Aware Attacks)**
  * **Venue/Year:** IROS 2026 (Zhang et al. / Yin et al.)
  * **Description:** Employs physical perturbations and adversarial patches targeting the vision-language alignment or spatial grounding mechanism of VLAs.
  * **Location:** T2 (Multimodal Attacks), T1-2 (Physical/Patch attacks)
  * **Priority:** HIGH
  * **BibKey:** zhang2026structure, yin2026vlaguard

* **Drift: Derailing Denoising Trajectories (Flow-Matching VLAs)**
  * **Venue/Year:** arXiv, 2026 (Tae et al.)
  * **Description:** Specifically targets modern flow-matching architectures (e.g., Pi0) using adversarial patches to derail intended action denoising trajectories.
  * **Location:** T1-1 (Attacks tailored to specific foundation architectures like Pi0)
  * **Priority:** MEDIUM
  * **BibKey:** tae2026drift

* **Universal Transferable Patch Attacks (When Robots Obey the Patch)**
  * **Venue/Year:** CVPR 2026 (Lu et al.)
  * **Description:** Systematizes the creation of universal adversarial patches that transfer across different VLA policies in physical spaces.
  * **Location:** T1-2 (Physical/Patch attacks), T1-3 (Black-box transfer)
  * **Priority:** HIGH
  * **BibKey:** lu2026whenrobots

* **Objective-Decoupled Optimization for Backdoor Attacks (BadVLA variation)**
  * **Venue/Year:** arXiv 2025 (Zhou et al.)
  * **Description:** Advances backdoor poisoning in VLAs by decoupling the trigger embedding from the fine-tuning objective.
  * **Location:** T1-1 (Poisoning/Backdoor)
  * **Priority:** MEDIUM
  * **BibKey:** zhou2025badvla

## 2. Defenses Relevant to VLA Robustness
**Gap:** T1-4 and T3-1 need VLA-specific robustness, going beyond VLM porting.

* **Structure-Aware Robust Fine-Tuning**
  * **Venue/Year:** IROS 2026 (Zhang et al.)
  * **Description:** Defense against attention hijacking by utilizing structure-aware robust fine-tuning techniques for VLAs.
  * **Location:** T1-4, T3-1 
  * **Priority:** HIGH
  * **BibKey:** zhang2026structure

* **Randomized Smoothing Meets Vision-Language Models**
  * **Venue/Year:** EMNLP 2025 (Seferis et al.)
  * **Description:** Extends certified robustness (randomized smoothing) to generative VLM outputs connecting to discrete service-robot commands.
  * **Location:** T1-4, T3-1
  * **Priority:** HIGH
  * **BibKey:** seferis2025randomized

* **Reconstructing Visual Tokens (Erasing Backdoors)**
  * **Venue/Year:** ICRA 2026 (Li et al.)
  * **Description:** Mitigates backdoor attacks in robotic policies by reconstructing visual tokens before action decoding.
  * **Location:** T1-4
  * **Priority:** MEDIUM
  * **BibKey:** li2026whenattention

## 3. Safety / Trustworthiness Benchmarks
**Gap:** Need contemporary 2025-2026 VLA security benchmarks.

* **AttackVLA: Benchmarking Adversarial and Backdoor Attacks on VLAs**
  * **Venue/Year:** arXiv 2025 (Li et al.)
  * **Description:** A dedicated benchmark suite evaluating a range of evasion and poisoning threats against VLA models.
  * **Location:** T3-1
  * **Priority:** HIGH
  * **BibKey:** li2025attackvla

* **ManipArena: Physical Realistic Evaluation**
  * **Venue/Year:** arXiv 2026 (Sun et al.)
  * **Description:** Provides a physical, diagnostically controlled evaluation protocol for general-purpose robotic intelligence, moving beyond simulator-centric benchmarks.
  * **Location:** T1/T2 Evaluation Plans, T3-1
  * **Priority:** HIGH
  * **BibKey:** sun2026maniparena

## 4. Interpretability / Attribution Methods
**Gap:** Need 2025-2026 spatial/multimodal reasoning attribution over generic VLM/LLM saliency.

* **Chain of Spatial Thoughts: Modality-Agnostic Spatial Grounding**
  * **Venue/Year:** arXiv 2026 (Schofield et al.)
  * **Description:** Explores modality-agnostic spatial grounding processes, providing a basis for interpreting how VLMs/VLAs map instructions to physical coordinates.
  * **Location:** T3-2
  * **Priority:** HIGH
  * **BibKey:** schofield2026chain

* **Multi-Modal Neuro-Symbolic Approach for Spatial Reasoning**
  * **Venue/Year:** arXiv 2025 (Jahangard et al.)
  * **Description:** Introduces neuro-symbolic techniques for fine-grained spatial reasoning in robotics, providing explicit rather than implicit/correlation-driven interpretability.
  * **Location:** T3-2
  * **Priority:** MEDIUM
  * **BibKey:** jahangard2025multimodal


## New bib keys to add
puthumanaillam2026trajectory
zhang2026structure
yin2026vlaguard
tae2026drift
lu2026whenrobots
zhou2025badvla
seferis2025randomized
li2026whenattention
li2025attackvla
sun2026maniparena
schofield2026chain
jahangard2025multimodal