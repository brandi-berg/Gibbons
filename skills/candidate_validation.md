# Command: `/validate` (Candidate Validation Engine)

This file contains the core prompt engineering logic and system instructions for the `/validate` execution step in Phase 2[cite: 1].

---

## 🎯 Operational Objective
Evaluate an unstructured candidate profile (Resume, LinkedIn PDF, or raw text) against an Enhanced Job Description and the Ideal Candidate Profile (ICP)[cite: 1]. The output must strip out subjective bias and deliver a highly analytical calibration assessment based *solely* on verifiable evidence[cite: 1].

---

## ⚙️ System Instructions & Prompt Logic

When the user executes `/validate [Candidate Profile]`, run the following protocol:

### 1. Context Extraction
* Load and bind constraints from `config/Section_A_Technical_Guardrails.md`[cite: 1].
* Scan the candidate profile *only* for explicit facts, years of experience, scope of responsibilities, and specific tools mentioned[cite: 1].

### 2. Analytical Evaluation Matrix
Evaluate the profile across four dimensions, applying a **Signal Strength Rating (1-5)**:
* **Score 5:** Exceeds all core criteria with explicit, measurable historical data (e.g., scale managed, concrete outcomes).
* **Score 4:** Meets all core criteria with verifiable execution experience.
* **Score 3:** Meets majority of criteria but relies on generalized statements or has minor skill/tooling gaps.
* **Score 2:** Significant core capability gaps; background is adjacent rather than aligned.
* **Score 1:** No alignment; profile fails fundamental criteria thresholds.

---

## 📋 Expected Output Template

The system must output the assessment using this rigid Markdown format:

### 📊 Calibration Summary
* **Candidate Identifier:** [Name or Current Title]
* **Signal Strength Rating:** [1-5]
* **Core Recommendation:** [PROCEED TO OUTREACH / CONDITIONAL PROCEED / SKIP][cite: 1]

### 🔍 Hard Evidence Mapping
*(Map 3-5 key job requirements directly to the candidate's exact experience profile. Cite the exact team scale, numbers, or tooling mentioned)[cite: 1].*
* **Requirement X:** [What the JD requires] 
  * `Evidence Found:` [Verbatim or exact factual summary from profile]

### ⚠️ Gaps, Risks & "Not Stated" Flags
*(Enforce the Zero-Inference Protocol. Highlight missing metrics or missing tooling alignments exactly as they appear—or don't appear)[cite: 1].*
* **Identified Gaps:** [List explicit misalignments]
* **Not Stated:** [List core JD requirements completely missing from the profile text][cite: 1].

### 📦 CARRY FORWARD — Candidate Validation Block
*(Generate this condensed snippet to act as state persistence for the `/outreach` command. This ensures context carries over to the next session without duplicate processing)[cite: 1].*
```text
[START_CARRY_FORWARD: VALIDATE]
Role: [Title]
Candidate: [Identifier]
Rating: [Score]/5
Core Signals: [Key technical anchors found]
Hook Hooks: [1-2 high-signal data points to anchor outreach personalization]
[END_CARRY_FORWARD]
