# Graph Report - satc_res_robotics  (2026-09-24)

## Corpus Check
- 42 files · ~117,277 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 205 nodes · 189 edges · 23 communities (22 shown, 1 thin omitted)
- Extraction: 96% EXTRACTED · 4% INFERRED · 0% AMBIGUOUS · INFERRED: 7 edges (avg confidence: 0.85)
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `36fb82b6`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- Orchestrator
- academic_review
- Visualization Agent
- revision_plan
- auditor_feasibility
- context_report
- integrity_review_final
- novelty_assessment
- researcher_report
- writer_changelog
- research-writing-instructions
- SKILL
- verification-report-template
- prompt-boost
- proposal-review-boost
- writer-academic-writing-cs
- writing-introduction
- writing-quality-check
- punctuation-patterns
- structure-patterns
- doublecheck
- writing-abstract
- ltex.dictionary.en-US

## God Nodes (most connected - your core abstractions)
1. `Orchestrator` - 18 edges
2. `Visualization Agent` - 10 edges
3. `writing-quality-check` - 9 edges
4. `academic_review` - 7 edges
5. `integrity_review` - 7 edges
6. `auditor_feasibility` - 7 edges
7. `timeline_update` - 6 edges
8. `burstiness` - 6 edges
9. `punctuation-patterns` - 6 edges
10. `structure-patterns` - 6 edges

## Surprising Connections (you probably didn't know these)
- `Visualization Agent` --references--> `Robot Example Figure 1`  [INFERRED]
  .github/agents/Visualization.agent.md → figures/examples/1.png
- `Visualization Agent` --references--> `Robot Example Figure 2`  [INFERRED]
  .github/agents/Visualization.agent.md → figures/examples/2.png
- `Visualization Agent` --references--> `Robot Example Figure 3`  [INFERRED]
  .github/agents/Visualization.agent.md → figures/examples/3.png
- `Visualization Agent` --references--> `Robot Example Figure 4`  [INFERRED]
  .github/agents/Visualization.agent.md → figures/examples/4.png
- `Visualization Agent` --references--> `Robot Example Figure 5`  [INFERRED]
  .github/agents/Visualization.agent.md → figures/examples/5.png

## Hyperedges (group relationships)
- **Review & Feasibility Artifact Corpus** — artifacts_academic_review_academic_review, artifacts_auditor_feasibility_auditor_feasibility, artifacts_context_report_context_report, artifacts_integrity_review_integrity_review, artifacts_integrity_review_final_integrity_review_final, artifacts_novelty_assessment_novelty_assessment [EXTRACTED 0.85]
- **Academic Writing & Review Quality Framework** — github_skills_building_skill_skill_skill, github_skills_doublecheck_skill_doublecheck, github_skills_doublecheck_assets_verification_report_template_verification_report_template, github_skills_prompt_boost_skill_prompt_boost, github_skills_proposal_review_boost_skill_proposal_review_boost, github_skills_writer_academic_writing_cs_skill_writer_academic_writing_cs [EXTRACTED 0.95]
- **Multi-Agent Proposal Lifecycle System** — agents_rules_graphify_graphify, agents_workflows_graphify_graphify, github_agents_academic_reviewer_agent_academic_reviewer, github_agents_architect_agent_proposal_architect, github_agents_auditor_agent_auditor, github_agents_context_agent_context_agent [EXTRACTED 0.95]

## Communities (23 total, 1 thin omitted)

### Community 0 - "Orchestrator"
Cohesion: 0.06
Nodes (34): graphify, graphify, Workflow graphify, Core Principle, Primary Questions, Proposal Architect, Audit Framework, Auditor (+26 more)

### Community 1 - "academic_review"
Cohesion: 0.12
Nodes (18): 1 SIGNIFICANCE, academic_review, EXECUTIVE SUMMARY, Limitations, NSF SaTC 20 RES Academic Reviewer Assessment, Strengths, Critical Structural Issues, Executive Integrity Summary (+10 more)

### Community 2 - "Visualization Agent"
Cohesion: 0.20
Nodes (10): Robot Example Figure 1, Robot Example Figure 2, Robot Example Figure 3, Robot Example Figure 4, Robot Example Figure 5, Robot Example Figure 6, Language Black Box Results Figure, Core Principle (+2 more)

### Community 3 - "revision_plan"
Cohesion: 0.22
Nodes (9): 1 Executive Revision Summary, 2 Issue Aggregation deduplicated cross-referenced, 3 Issue-to-Section Mapping, 4 Prescribed Fixes ordered P0 A first then P0 B then P1 A P1 B P2, revision_plan, Revision Plan  NSF SaTC 20 RES Toward Secure and Robust Generalist Robotic Models, Core Principle, Planner (+1 more)

### Community 4 - "auditor_feasibility"
Cohesion: 0.11
Nodes (18): 1 Executive Audit Summary, 2 Problem Validation, 3 Logic Audit, Adversarial Feasibility  Methodological Audit, auditor_feasibility, NSF SaTC 20 RES Toward Secure and Robust Generalist Robotic Models, NSF SaTC 20 RES  Research Plan and 4-Year Timeline, Part 1  Executive Research Program (+10 more)

### Community 5 - "context_report"
Cohesion: 0.33
Nodes (6): 01_v2tex  Project Description front half, 1 Executive Summary  mustfix items, 2 Filebyfile checklist, context_report, main_v2tex  wiring, SaTC 20 RES NSF 25-515 Compliance Checklist  CAREERRES  5yr4yr

### Community 6 - "integrity_review_final"
Cohesion: 0.33
Nodes (6): 1 Structural Integrity, 2 Logical Consistency, 3 Cross-Agent Consistency, Executive Summary, integrity_review_final, Integrity Review  Final Revision Pass Validation

### Community 7 - "novelty_assessment"
Cohesion: 0.33
Nodes (6): 1 Executive Assessment, 2 Novelty Classification, 3 Technical Novelty, 4 Methodological Novelty, novelty_assessment, Novelty  Differentiation Assessment

### Community 9 - "researcher_report"
Cohesion: 0.33
Nodes (6): 1 Adversarial Attacks on VLA  Embodied Policies, 2 Defenses Relevant to VLA Robustness, 3 Safety  Trustworthiness Benchmarks, Executive Research Overview, Methods Coverage Report Security and Trustworthiness of VLA Robot Foundation Models, researcher_report

### Community 11 - "writer_changelog"
Cohesion: 0.33
Nodes (6): Applied Fixes, R1  Duplicate section label P0 editorial, R4  Embodiment count consistency P1 editorial, R5  Dataset count clarity P1 editorial, writer_changelog, Writer Changelog  A-type Editorial Revisions

### Community 12 - "research-writing-instructions"
Cohesion: 0.33
Nodes (6): Banned Vocabulary MUST AVOID, Core Writing Style MUST, Data and Results MUST, Prohibited Elements NEVER, Research Writing and Title Instructions, research-writing-instructions

### Community 13 - "SKILL"
Cohesion: 0.33
Nodes (6): Agent Skills File Guidelines, Directory Structure, Frontmatter Required, Required SKILLmd Format, SKILL, What Are Agent Skills

### Community 14 - "verification-report-template"
Cohesion: 0.33
Nodes (6): All Claims, C -- Brief description of the claim, Flagged Items Review These First, Summary, Verification Report, verification-report-template

### Community 15 - "prompt-boost"
Cohesion: 0.33
Nodes (6): 1 Task Clarification, 2 Effectiveness Evaluation, 3 Performance Optimization, Analysis Framework, prompt-boost, Your Mission

### Community 16 - "proposal-review-boost"
Cohesion: 0.33
Nodes (6): Gotchas, Interrogation Checklist, Process, proposal-review-boost, Proposal Review Prompt Booster, When to Use This Skill

### Community 17 - "writer-academic-writing-cs"
Cohesion: 0.33
Nodes (6): 1 Precision, 2 Constraint-Driven Clarity, 3 Conciseness, Computer Science Research Proposal Writing Guide, Core Principles for CS Research Writing, writer-academic-writing-cs

### Community 18 - "writing-introduction"
Cohesion: 0.33
Nodes (6): 1 Establishing a Knowledge Territory, 2 Identifying a research gap or niche, 3 Addressing the research gap or niche, Essential Components and Best Practices, writing-introduction, Your Mission

### Community 19 - "writing-quality-check"
Cohesion: 0.09
Nodes (22): burstiness, Burstiness Sentence Length Variation, How to Fix, If Sentences Are All Long 30 words, If Sentences Are All Short 10 words, Quick Detection, Exception Rule, Flagged Terms 25 (+14 more)

### Community 20 - "punctuation-patterns"
Cohesion: 0.33
Nodes (6): Em Dash, How to Fix, Limit, Punctuation Pattern Control, punctuation-patterns, Why Its Flagged

### Community 21 - "structure-patterns"
Cohesion: 0.33
Nodes (6): 1 Rule-of-Three Compulsion, Fix, Structural Tics, structure-patterns, The Pattern, Why Its a Problem

### Community 23 - "doublecheck"
Cohesion: 0.40
Nodes (5): Activation, Active Mode, Deactivation, doublecheck, One-Shot Mode

### Community 27 - "writing-abstract"
Cohesion: 0.50
Nodes (4): Core Elements of a Perfect Abstract, Formatting and Style Guidelines, writing-abstract, Your Mission

## Knowledge Gaps
- **165 isolated node(s):** `Workflow graphify`, `Core Principle`, `Primary Questions`, `Audit Framework`, `Core Principle` (+160 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 165 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Orchestrator` connect `Orchestrator` to `academic_review`, `Visualization Agent`, `revision_plan`?**
  _High betweenness centrality (0.104) - this node is a cross-community bridge._
- **Why does `Visualization Agent` connect `Visualization Agent` to `Orchestrator`?**
  _High betweenness centrality (0.028) - this node is a cross-community bridge._
- **Why does `Planner` connect `revision_plan` to `Orchestrator`?**
  _High betweenness centrality (0.025) - this node is a cross-community bridge._
- **Are the 7 inferred relationships involving `Visualization Agent` (e.g. with `Robot Example Figure 1` and `Robot Example Figure 2`) actually correct?**
  _`Visualization Agent` has 7 INFERRED edges - model-reasoned connections that need verification._
- **What connects `Workflow graphify`, `Core Principle`, `Primary Questions` to the rest of the system?**
  _165 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Orchestrator` be split into smaller, more focused modules?**
  _Cohesion score 0.058823529411764705 - nodes in this community are weakly interconnected._
- **Should `academic_review` be split into smaller, more focused modules?**
  _Cohesion score 0.11764705882352941 - nodes in this community are weakly interconnected._