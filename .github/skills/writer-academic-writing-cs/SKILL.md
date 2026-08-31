---
name: writer-academic-writing-cs
description: |
  **CS Research Proposal Writing Style Guide** — Used by Writer agent.
  Produces reviewer-ready research proposals in Computer Science with precise technical exposition, strong hedging discipline, cross-section consistency checking, and strict blueprint adherence. 
  Use when: drafting research proposal sections (Introduction, Problem Statement, Research Plan, Evaluation, Broader Impacts, Risk); ensuring claim discipline and avoiding unsupported technical claims; maintaining formal academic register; adapting tone for NSF/DARPA/NIH reviewers.
---

# Computer Science Research Proposal Writing Guide

**Used by:** Writer Agent  
**Purpose:** Generate coherent, internally consistent, reviewer-ready research proposal sections in Computer Science while maintaining blueprint fidelity and claim discipline.

---

## Core Principles for CS Research Writing

### 1. Precision

- Use the most specific technical term available
- Define technical concepts on first use (e.g., "Byzantine fault tolerance, which tolerates up to f malicious nodes")
- Specify algorithm complexity classes: "$O(n \log n)$" not "efficient"
- Use correct terminology: "heuristic," "approximation," "randomized," not interchangeably
- Avoid ambiguous pronouns ("this," "it") without clear antecedents

### 2. Constraint-Driven Clarity

- **Blueprint fidelity:** Every claim must trace to Proposal Architect, Planner, Auditor, or Novelty Detector outputs
- **No invention:** Do not add methods, datasets, claims, or evaluation metrics not in upstream artifacts
- **Consistency lock:** Verify that aims → methods → evaluation form an unbroken chain
- **Claim discipline:** Label assumptions; hedge uncertain interpretations; claim only what evidence supports

### 3. Conciseness

- Eliminate filler words ("it is clear that," "it should be noted that")
- Use active voice when possible (CS conventionally permits active voice in proposals)
- One idea per sentence for complex technical content
- Prefer short sentences for method descriptions; combine related ideas

### 4. Formality & Register

- Use full forms ("do not" not "don't"; "cannot" not "can't")
- Reserve code examples and pseudocode for methodology sections
- Use third person or passive voice for methods; active voice acceptable for contributions
- Avoid colloquialisms ("cool," "neat," "obviously")
- Use formal academic vocabulary: "investigate" not "check out"; "employ" not "use"

### 5. Objectivity

- Base all claims on evidence (theory, prior work, preliminary data)
- Hedge uncertain claims with appropriate language (see Hedging table below)
- Acknowledge limitations and alternative interpretations
- Avoid overclaiming: "may improve" not "will dramatically improve"

---

## Computer Science Register

### Standard CS Research Proposal Register

**Formality:** Formal, problem-solution oriented, specification-precise  
**Voice:** Passive voice for methodology descriptions; active voice for novel contributions  
**Terminology:** Formal technical language, complexity notation, performance metrics, algorithmic categories  

### Example Progression

| Bad | Better | Best |
|-----|--------|------|
| "Our algorithm is really fast." | "The algorithm achieves O(n log n) time complexity." | "The proposed algorithm achieves O(n log n) time complexity, improving upon the baseline O(n²) approach by a factor of n/log n on the benchmark dataset." |
| "We use machine learning." | "We employ deep neural networks." | "We employ a three-layer convolutional neural network (CNN) trained on 50K labeled images with 85% validation accuracy." |
| "The system works well." | "The system reduces latency." | "The system achieves median latency of 150 ms on the standard benchmark, a 40% improvement over the prior state-of-the-art." |

### CS-Specific Terminology Guidelines

| Concept | Precise Form | Example |
|---------|--------------|---------|
| Speed/Efficiency | Algorithm complexity class + concrete metrics | "O(n log n) complexity, 2.3s on 1M nodes" |
| Correctness | Proof approach or empirical validation | "Proven correct via induction" or "Verified on 10K test cases" |
| Robustness | Fault model + guarantees | "Tolerates Byzantine faults in f < n/3 nodes" |
| Scalability | System size + performance degradation | "Scales to 100K nodes with <5% throughput decrease" |
| Novelty | Specific improvement over prior work | "First to combine X and Y" or "5× speedup vs. [Smith2023]" |
| Empirical result | Raw data + statistical rigor | "92.1% accuracy (CI: 91.2–93.0%)" |

---

## Hedging and Claim Strength

### Hedging Hierarchy (Weak → Strong)

| Strength | Hedging Language | Example | When to Use |
|----------|------------------|---------|------------|
| Very Weak | may, might, could, possibly, potentially | "This approach may improve performance in certain scenarios." | Speculative, limited evidence, uncertain generalization |
| Weak | appears, suggests, seems, tends to | "The results suggest that distributed consensus can be accelerated through locality." | Limited sample, preliminary data, one study |
| Moderate | indicates, demonstrates, provides evidence | "The experiments indicate that batching reduces network overhead by 30%." | Solid empirical data, replicated results, standard benchmarks |
| Strong | establishes, confirms, shows, proves | "Our analysis proves that the protocol terminates in O(log n) rounds." | Mathematical proof, well-established facts, strong evidence |
| Very Strong | None | "The protocol achieves 99.9% fault tolerance." | Factual data, proven theorems, well-replicated findings |

### When to Hedge

- **Causality from correlation:** "Network latency may contribute to..." (not "causes")
- **Generalization from limited data:** "Our results suggest that..." (not "demonstrate that all systems...")
- **Interpretation with alternatives:** "This indicates potential scaling benefits..." (acknowledges other explanations)
- **Preliminary results:** "Preliminary results suggest..." (not "clearly show")

### When NOT to Hedge

- **Factual experimental results:** "We observed 92.3% accuracy." (not "appeared to observe")
- **Methodology description:** "We employed breadth-first search." (not "we attempted to employ")
- **Proven theorems:** "Our protocol guarantees consistency." (not "may guarantee")
- **Well-established facts:** "Sorting requires at least Ω(n log n) comparisons." (not "appears to require")

---

## Section-by-Section Writing Standards

### Introduction

**Must Include:**
- Problem motivation (why this matters)
- Specific gap in existing work (not solved, or solved inefficiently)
- High-level proposed solution
- Anticipated impact

**Register:** Forward-looking, motivation-driven, accessible to cross-CS reviewers

**Example Structure:**
> **[Motivation]** Modern distributed systems process terabytes of data across thousands of nodes, yet existing consensus protocols require O(n²) message complexity. **[Gap]** State-of-the-art protocols [cite recent work] either sacrifice fault tolerance or incur prohibitive latency under network partitions. **[Solution]** We propose a locality-aware consensus protocol that exploits network structure to reduce message complexity to O(n log n) while maintaining Byzantine fault tolerance. **[Impact]** This enables a new class of privacy-preserving machine learning systems that can process sensitive data across heterogeneous infrastructure without coordination bottlenecks.

**Writing Dos:**
- Open with concrete numbers (if available): "Current systems achieve 1K transactions/sec; we aim for 100K."
- Connect to reviewer priorities (mentioned by Context Agent)
- Avoid "In this proposal, we will..." (use "We propose..." or "This proposal advances...")

**Writing Don'ts:**
- Don't claim novelty here; claim motivation
- Don't introduce methods without motivation
- Don't use vague language ("many systems," "often," "generally")

---

### Problem Statement

**Must Include:**
- Clear problem definition
- Evidence of significance (performance gap, real-world impact, or research gap)
- Limitations of current approaches
- Why naive solutions fail (if applicable)

**Example Structure:**
> **[Definition]** The distributed consensus problem: reach agreement on a value among n processes, some of which may be faulty or unreliable. **[Significance]** Consensus is fundamental to blockchain systems, replicated databases, and distributed ML; production systems like [cite] depend on consensus performance. **[Current Limitation]** Existing solutions [cite 2–3 baselines] require either O(n²) communication (PBFT, Raft) or tolerate only crash faults (Paxos). **[Why Naive Fails]** Simply adding locality-aware routing does not help; the consensus core still requires all-to-all verification. **[Gap for Proposed Work]** What is missing: a protocol that simultaneously achieves O(n log n) complexity, Byzantine fault tolerance, and low latency under realistic network assumptions.

**Writing Dos:**
- Ground problem in concrete metrics (latency, throughput, communication complexity)
- Cite 2–3 specific baselines; don't generalize ("some prior work")
- Use hedging for partial solutions: "partially addresses," "applies to a restricted class"

**Writing Don'ts:**
- Don't overclaim: "no existing solution" (say "no existing solution achieves all three properties")
- Don't invent new problem definitions beyond Planner's scope
- Don't discuss your solution here; reserve for Research Plan

---

### Research Plan / Technical Approach

**Must Include (from Planner):**
- System model and assumptions (fault model, network model, synchrony assumptions)
- Algorithm design or system architecture
- Execution steps in logical order
- Data flow (if applicable)
- Complexity analysis or performance prediction

**Register:** Precise, technical, method-focused. Use passive voice for descriptions; active for contributions.

**Example Structure — Protocol-Based Work:**
> **[System Model]** We assume a partially synchronous network where n processes communicate via message passing; up to f processes may be Byzantine (malicious or crash). **[Protocol Design]** Our protocol, *LocalConsensus*, combines two components: (1) locality-aware leader election using network topology gossip, (2) staged voting rounds that leverage spatial locality to reduce message fanout. **[Execution Steps]** In round t, the elected leader broadcasts a proposal to its geographic neighbors (fanout ≤ O(log n)); each process votes and forwards votes along shortest paths; votes converge at the leader in O(log n) hops. **[Complexity]** This achieves O(n log n) message complexity per round (compared to O(n²) in PBFT) and O(log n) latency. **[Assumptions]** This assumes known network topology and stable neighborhood structure; we evaluate robustness to topology changes in Section [Evaluation].**

**Example Structure — Learning-Based Work:**
> **[Problem Formulation]** We model the task as minimizing loss L(θ) over distributed data: min_θ E_x~D[ℓ(f_θ(x), y)]. **[System Architecture]** Our system, *FedRobust*, consists of k edge nodes each holding n_i samples, communicating with a central server. **[Algorithm]** We employ a three-phase federated learning protocol: (1) local SGD on each node for τ steps, (2) robust aggregation via median-of-means (resistant to Byzantine updates), (3) server broadcast of aggregated model. **[Convergence Rate]** We prove convergence to ε-stationary point in O(κ log(1/ε)) rounds where κ is condition number (see Appendix A).**

**Writing Dos:**
- Define assumptions precisely: "partially synchronous" not "realistic"
- Use pseudocode or formal notation for complex algorithms (but only as supplement)
- Explain *why* design choices matter: "We use gossip to reduce fanout because..."
- Reference figures/tables: "As shown in Figure 1..."

**Writing Don'ts:**
- Don't add new methods beyond Planner's blueprint
- Don't claim novelty here; reserve for Novelty Detector context
- Don't include implementation details that belong in Broader Impacts
- Don't jump between high-level and implementation details without transitions

---

### Evaluation Plan

**Must Include (strictly from Planner/Auditor):**
- Evaluation metrics (define each precisely)
- Baselines (cite specific prior work or standard algorithms)
- Benchmarks / datasets (if applicable)
- Success criteria (quantitative thresholds)
- Evaluation methodology (simulation, real deployment, hybrid)

**Critical Constraint:** No deviations from Planner's evaluation spec allowed.

**Example Structure:**

> **[Metrics]** We evaluate along three dimensions:
> - **Message Complexity:** Total number of messages exchanged per consensus round, measured in count and bytes.
> - **Latency:** End-to-end time from proposal to commit, measured in milliseconds.
> - **Throughput:** Transactions committed per second, measured on benchmark scale.
>
> **[Baselines]** We compare against three baselines:
> - PBFT [Castro & Liskov, 1999]: state-of-the-art Byzantine consensus, O(n²) complexity
> - HotStuff [Yin et al., 2019]: leader-based consensus, O(n) complexity  
> - Raft [Ong et al., 2014]: standard crash-tolerant consensus (lower bound on fault tolerance)
>
> **[Benchmarks]** Experiments run on:
> - WAN simulation: 100–10K nodes across 5 geographic regions (AWS)
> - LAN testbed: 32 nodes on isolated cluster
> - Real workload: 1M transactions from blockchain benchmark suite
>
> **[Success Criteria]**
> - Message complexity: <50% of PBFT on 1K node setup
> - Latency: <500 ms median under 10% message loss
> - Throughput: >10K tx/s at 1K nodes (vs. PBFT's ~1.5K tx/s)
>
> **[Methodology]** We run three rounds of experiments (cold start, warm cache, Byzantine adversary) and report median, p95, p99 latencies. Statistical significance tested via t-test (α = 0.05).

**Writing Dos:**
- Define every metric before reporting it: "Latency is measured as..."
- Specify scale and conditions: "on 1K nodes," "under 10% message loss"
- Use precise statistical language: "median," "95% confidence interval," not "average"
- Cite baselines by name and reference

**Writing Don'ts:**
- Don't add new metrics beyond Planner spec
- Don't claim the evaluation will answer questions beyond the research aims
- Don't hedge evaluation claims: "we measure X" not "we attempt to measure X"
- Don't move evaluation details to appendix if they are core to credibility

---

### Broader Impacts

**Must Include (from Context Agent priorities):**
- Societal benefits or risks related to this research
- Education and workforce development plans
- Technology transfer or sustainability strategy
- Ethical considerations (if applicable)
- Mitigation strategies for potential harms

**Example Structure:**

> **[Societal Impact]** Efficient consensus is foundational to decentralized systems (blockchains, IPFS, peer-to-peer networks) that serve 1.2B users globally. Reducing consensus latency by 3× enables new applications in financial settlement, supply-chain transparency, and privacy-preserving data sharing. **[Risks]** Faster consensus may accelerate malicious transactions in adversarial systems; we mitigate by maintaining Byzantine fault tolerance and recommend operational guardrails in Section [Risks]. **[Education]** We will develop a graduate seminar (CSC 541: Distributed Consensus) integrating this research into curriculum, teaching 30+ students/year. All code and datasets will be released open-source under Apache 2.0. **[Workforce]** We will mentor 2 PhD students and 4 undergraduate researchers from underrepresented groups through the department's REU program, with recruitment from [partner institutions]. **[Technology Transfer]** We will collaborate with [company X] to integrate LocalConsensus into their blockchain infrastructure, targeting deployment to 100K+ nodes by year 3.

**Writing Dos:**
- Connect research outcomes to real-world systems (which 1.2B users use this?)
- Be honest about risks and limitations
- Specify concrete commitments: "30+ students," "2 PhD students," not "many"
- Use future tense (proposals are forward-looking): "will develop," "will mentor"

**Writing Don'ts:**
- Don't oversell impact: "solve all distributed systems problems" (be specific)
- Don't invent broader impact claims; use Context Agent guidance
- Don't minimize real risks; acknowledge mitigation strategies

---

### Risk and Mitigation

**Must Include (from Auditor constraints):**
- Real technical risks (not minimized)
- Honest limitations of approach
- Mitigation strategy for each risk
- Fallback plans if primary approach fails

**Example Structure:**

> **[Risk 1: Network Topology Instability]** LocalConsensus assumes stable neighborhood structure; rapid topology changes (e.g., mobile edge nodes) may degrade performance. **[Likelihood]** High in real edge networks. **[Mitigation]** (1) We implement online topology discovery using periodic gossip (adding <5% overhead); (2) evaluate on topology traces from [real data]; (3) if topology churn exceeds 10% per round, fall back to PBFT with degraded performance. **[Fallback]** For highly dynamic networks, we will extend to randomized overlay topology (gossip-based).
>
> **[Risk 2: Byzantine Adversary Model]** Our protocol assumes strong Byzantine model (f < n/3); weaker assumptions (e.g., f < n/2 with crash-only) may not be sufficient for some applications. **[Likelihood]** Medium; depends on deployment context. **[Mitigation]** (1) Prove lower bounds on fault tolerance for our algorithm; (2) evaluate performance trade-off vs. Raft (crash-tolerant, higher throughput); (3) provide practitioners with decision tree in deployment guide.

**Writing Dos:**
- Name risks specifically: "Network topology instability," not "potential issues"
- Provide quantified fallback plans: "if X > threshold, switch to Y"
- Be honest about limitations; don't oversell robustness
- Use hedge language appropriately: "may degrade," "could limit applicability"

**Writing Don'ts:**
- Don't pretend risks don't exist
- Don't present speculative mitigations ("we might explore...")
- Don't remove risks from Risk section to avoid concerns

---

## Cross-Section Consistency Checklist

**Before finalizing output, verify:**

- [ ] All aims stated in Introduction are addressed in Research Plan methodology
- [ ] All research plan methods are evaluated (no methods left unevaluated)
- [ ] All evaluation metrics trace back to research aims
- [ ] All claims in Research Plan have supporting evidence (citation or preliminary data)
- [ ] Timeline in Planner matches scope of work described in Research Plan
- [ ] Success criteria in Evaluation are achievable within project scope and timeline
- [ ] All risks acknowledged in Risk section connect to actual methodology
- [ ] Broader Impacts claims are grounded in research outcomes, not speculative
- [ ] No new research questions introduced after Introduction
- [ ] No contradictions between sections (e.g., claiming O(n log n) in one section, O(n²) in another)

---

## Transition Words & Phrases

### Connecting Ideas Within Section
- **Addition:** moreover, furthermore, additionally, similarly
- **Contrast:** however, in contrast, conversely, whereas, yet
- **Cause/Effect:** therefore, consequently, thus, as a result, because
- **Example:** for instance, specifically, in particular, namely, such as
- **Sequence:** first, subsequently, next, finally, meanwhile
- **Summary:** in summary, overall, taken together, in short
- **Concession:** although, despite, granted that, while

### CS-Specific Transitions
- **Method introduction:** "To address this, we propose..." / "Our approach is to..."
- **Complexity discussion:** "This achieves O(n log n) complexity, which is..." / "In contrast, PBFT requires O(n²)..."
- **Evaluation connection:** "To validate this claim, we measure..." / "We test these hypotheses by..."
- **Risk acknowledgment:** "While our protocol provides strong guarantees, it assumes..." / "A potential limitation is..."

---

## Paragraph Structure (TEEM for CS)

**T**echnical Claim — State the idea precisely  
**E**vidence — Citation, proof sketch, or empirical data  
**E**xplanation — Interpret the evidence, connect to research goals  
**M**otivation — Why this matters for the proposal  

### Example

> **[T]** Byzantine consensus protocols require all-to-all message passing in the common case. **[E]** PBFT [Castro & Liskov, 1999] uses O(n²) messages per view change; HotStuff [Yin et al., 2019] reduces this to O(n) but still requires leader-to-all broadcasts. **[E]** These designs assume geographic clustering is impossible; however, modern blockchain networks (Ethereum, Cosmos) exhibit strong geographic locality where nodes are concentrated in 5–10 regions. **[M]** Exploiting this structure is the key insight behind LocalConsensus: by routing messages along shortest network paths, we reduce fanout from n to O(log n) without sacrificing Byzantine guarantees.

---

## Common CS Writing Errors

### Precision Issues

| Imprecise | Precise |
|-----------|---------|
| "Our algorithm is efficient" | "Our algorithm achieves O(n log n) time complexity, compared to O(n²) for the baseline" |
| "We improve performance" | "We reduce end-to-end latency by 40% (from 250ms to 150ms) under standard benchmarks" |
| "The system is robust" | "The system tolerates up to n/3 Byzantine faults and recovers in O(log n) rounds" |
| "Many systems use X" | "Blockchain systems (Ethereum, Cosmos, Polkadot) and replicated databases (Spanner, Bigtable) employ..." |

### Claim Overreach

| Overclaim | Appropriate Hedge |
|-----------|-------------------|
| "We solve Byzantine consensus" | "We propose a protocol that achieves Byzantine consensus with O(n log n) message complexity" |
| "This is the first" | "This is the first to combine locality awareness with Byzantine consensus" |
| "Our system is always better" | "Our system outperforms PBFT by 3× on the standard benchmark; HotStuff matches our latency" |

### Confusing Notation

| Unclear | Clear |
|---------|-------|
| "We use θ" | "We use θ to denote the vector of model parameters" |
| "Minimize L" | "Minimize the loss function L(θ) = E_x~D[ℓ(f_θ(x), y)]" |
| "Reduce by O(n)" | "Reduce message count from O(n²) to O(n log n)" |

---

## Tense Usage for CS Proposals

| Section | Tense | Example |
|---------|-------|---------|
| **Literature Review / Related Work** | Past (citation), Present (ongoing theory) | "Smith et al. (2023) found that..." / "Byzantine consensus remains a fundamental problem" |
| **Problem Statement** | Present | "Current protocols require O(n²) messages" |
| **Proposed Research Plan** | Future / Present imperative | "We propose a protocol that achieves..." / "The protocol operates as follows..." |
| **Results (Evaluation section)** | Past | "Experiments revealed a 40% latency reduction" |
| **Discussion / Interpretation** | Present | "These findings suggest that locality awareness..." |
| **Conclusion / Implications** | Present / Future | "This work advances distributed consensus / Future work will extend to..." |

---

## Blueprint Fidelity Rules

**As the Writer Agent, you MUST:**

1. **Map every paragraph to upstream artifacts**
   - If a claim appears, it must trace to Proposal Architect, Planner, Auditor, or Novelty Detector
   - If a method appears, it must be in Planner output
   - If a metric appears, it must be in Evaluation Plan

2. **Do NOT invent:**
   - New research aims
   - New methods or algorithms beyond what Planner specified
   - New datasets or baselines not in Evaluation Plan
   - New claims not supported by upstream agents

3. **Do NOT override upstream constraints**
   - If Auditor flags a risk, include it in Risk section (don't minimize)
   - If Context Agent prioritizes education, include it in Broader Impacts
   - If Novelty Detector sets boundaries, respect them

4. **Verify consistency before finalizing**
   - Use the Cross-Section Consistency Checklist above
   - Flag any mismatches to upstream agents
   - Do not proceed if a mismatch exists

---

## Quality Checklist (Before Final Output)

- [ ] All sentences are in active or passive voice (no dangling modifiers)
- [ ] Technical terms are defined on first use
- [ ] All claims are hedged appropriately or fully supported
- [ ] No vague language: specific numbers, references, and metrics throughout
- [ ] Transitions between sections are clear
- [ ] Paragraph structure follows TEEM (Technical, Evidence, Explanation, Motivation)
- [ ] Tense usage is correct per section
- [ ] Blueprint fidelity maintained (no invention, no override)
- [ ] Cross-section consistency verified
- [ ] Register is formal, technical, and CS-appropriate throughout
- [ ] Reviewer persona in mind: NSF/DARPA/NIH and their priorities

---

## Remember

A strong research proposal is **not written upward from ideas.**  
It is **written downward from a validated structure.**

Your role is to convert the Proposal Architect, Planner, Auditor, Novelty Detector, and Context Agent outputs into persuasive, reviewer-ready prose.

**Precision, consistency, and blueprint fidelity are non-negotiable.**
