# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **CareerCraft Agent** (`career-craft-agent`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** CareerCraft Agent (`career-craft-agent`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Education / Career Readiness, ATS Optimization & Resume Evaluation  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), FERPA, GDPR  

---

## How the Agent Decides

CareerCraft Agent is an autonomous career enhancement, resume evaluation, ATS optimization, job fit scoring, and tailored cover letter generation agent designed for **CareerCraft**. The platform simulates modern Applicant Tracking Systems, executes semantic skill-gap extraction against target job descriptions, formulates structured resume feedback, and generates customized professional correspondence.

### 1. Decision Architecture

The resume evaluation, ATS scoring, skill-gap analysis, and cover letter generation pipeline operates across a deterministic, five-stage architecture:

```
Candidate Input (Upload Resume PDF/DOCX + Optional Target Job Description)
    │
    ▼
[Stage 1: Multi-Format Ingestion & Structural Extraction]
    │  - Extracts text stream, hierarchy headings, and bullet points from PDF/DOCX
    │  - Evaluates layout parsability: detects nested tables, multi-column flows, unsearchable bitmaps
    │  - Normalizes contact data, work history, skill taxonomy, and educational credentials
    ▼
[Stage 2: Deterministic ATS Rubric Scoring]
    │  - Computes section completeness score: checks Summary, Experience, Education, Skills ($W_{\text{sec}} = 0.20$)
    │  - Audits bullet point quality: action verb strength and quantified metrics ($W_{\text{impact}} = 0.25$)
    │  - Evaluates document formatting cleanliness and Flesch-Kincaid readability index ($W_{\text{read}} = 0.15$)
    │  - Generates baseline ATS Parsability Score ($S_{\text{ats}} \in [0, 100]$)
    ▼
[Stage 3: Semantic Skill-Gap & Job-Fit Matching]
    │  - Ingests and tokenizes target job description into required and preferred competencies
    │  - Executes cosine similarity matching and synonym expansion (e.g., React $\leftrightarrow$ React.js $\leftrightarrow$ Frontend)
    │  - Categorizes skills into Matched, Missing Critical, and Transferable subsets ($W_{\text{match}} = 0.40$)
    │  - Computes composite Job Match Percentage ($S_{\text{match}} \in [0, 100]$)
    ▼
[Stage 4: Upskilling Roadmap & Feedback Synthesis]
    │  - Formulates prioritized recommendations: "Add quantified metric to experience bullet #2"
    │  - Recommends targeted learning resources and project ideas for missing critical skills
    │  - Identifies overused buzzwords (e.g., "hard worker", "team player") and suggests strong technical equivalents
    ▼
[Stage 5: Tailored Cover Letter Synthesis & Export]
    │  - Synthesizes candidate's verified background with job description objectives
    │  - Applies selected stylistic tone (*Formal*, *Confident*, or *Friendly*)
    │  - Generates downloadable PDF and clean Markdown candidate dossiers
    ▼
Actionable Evaluation Report & Optimized Application Package Delivered to Candidate
```

### 2. Scoring Methodology & Rubric Formulations

CareerCraft computes candidate evaluation metrics through two deterministic, mathematically rigorous scoring models:

1. **Composite ATS Parsability Score ($S_{\text{ats}}$)**:
   $$S_{\text{ats}} = (w_s \cdot C_{\text{sec}}) + (w_v \cdot Q_{\text{verbs}}) + (w_m \cdot M_{\text{metrics}}) + (w_f \cdot F_{\text{format}})$$
   where:
   - $C_{\text{sec}} \in [0, 100]$: Section completeness ratio (Contact: 20%, Summary: 15%, Experience: 35%, Education: 15%, Skills: 15%).
   - $Q_{\text{verbs}} \in [0, 100]$: Percentage of bullet points initiated with accredited strong action verbs.
   - $M_{\text{metrics}} \in [0, 100]$: Proportion of experience bullets featuring measurable numerical achievements.
   - $F_{\text{format}} \in [0, 100]$: Layout parsability penalty score (deducting for graphics, multi-column flows, unsearchable fonts).
   - Weights: $w_s = 0.25, w_v = 0.25, w_m = 0.25, w_f = 0.25$ ($\sum w_i = 1.0$).

2. **Semantic Job Fit Percentage ($S_{\text{match}}$)**:
   $$S_{\text{match}} = 100 \times \left( \alpha \cdot \frac{|K_{\text{cand}} \cap K_{\text{req}}|}{|K_{\text{req}}|} + \beta \cdot \frac{|K_{\text{cand}} \cap K_{\text{pref}}|}{|K_{\text{pref}}|} + \gamma \cdot \text{CosineSim}(\mathbf{v}_{\text{cand}}, \mathbf{v}_{\text{job}}) \right)$$
   where $K_{\text{req}}$ represents mandatory job skills, $K_{\text{pref}}$ represents preferred skills, and $\mathbf{v}$ denotes dense semantic embedding vectors ($\alpha = 0.50, \beta = 0.20, \gamma = 0.30$).

### 3. Thresholding & Refusal Decision Criteria

CareerCraft Agent enforces strict integrity boundaries:
- **Refusal to Fabricate Credentials**: Requests to invent fictional employment history, fake degrees, or false certifications are deterministically rejected with code `ERR_CREDENTIAL_FABRICATION_PROHIBITED`.
- **Refusal of Deceptive ATS Manipulation**: The agent refuses requests to embed hidden white-text keywords or inject invisible prompt injections into resume margins (`ERR_BLACK_HAT_MANIPULATION_REFUSED`).
- **Refusal of Unsearchable Image Files**: Scanned image-only PDFs lacking an embedded text layer trigger an upload warning prompting the user to submit an OCR-searchable PDF or DOCX (`ERR_UNSEARCHABLE_BITMAP_RESUME`).
- **Defensive PII Redaction**: National identification numbers, social security numbers, and precise residential street addresses are flagged for candidate removal before submission (`WARN_SENSITIVE_PII_DETECTED`).

### 4. Fallback Decision Mechanism

CareerCraft maintains uninterrupted user service through multi-tier fallbacks:
- **Heuristic NLP Fallback**: If the FastAPI semantic vector embedding service is offline or uncommunicative, the system seamlessly transitions to deterministic rule-based keyword regex matching with zero service interruption.
- **Rule-Based Template Pack Fallback**: If the generative AI model encounters API rate limits during cover letter creation, the platform serves industry-standard customizable cover letter templates populated with extracted candidate placeholders.
- **Model Fallback Cascade**: High-level resume feedback and personalized cover letter drafting default to `gemini-2.0-flash` with automatic failover to `gpt-4o` and `claude-3-5-sonnet`.

### 5. Human-in-the-Loop Governance

CareerCraft maintains candidate autonomy and editorial primacy:
- **Draft Status by Default**: All suggested bullet point revisions and generated cover letters are presented as editable drafts requiring candidate review, customization, and approval.
- **Tone & Style Customization**: Candidates retain full control over correspondence voice (*Formal*, *Confident*, *Friendly*) and target word length.
- **Continuous Editorial Agency**: The platform never automatically submits applications or modifies original resume files without explicit user consent.

---

## The Data It Uses

CareerCraft Agent operates under strict privacy and educational data governance standards.

### 1. Ingested Input Data

The agent processes only user-uploaded career documents and job criteria:
- **Resume Documents**: Uploaded PDF or DOCX files containing candidate work history, education, skills, and contact details.
- **Target Job Postings**: User-pasted job descriptions, role titles, company names, and requirement lists.
- **Stylistic Preferences**: Selected cover letter tone, target length, and specific career accomplishments highlighted by the candidate.

### 2. Configuration & Reference Data

- **Standardized Skill Taxonomies**: Authoritative mappings of tech stacks, programming languages, cloud frameworks, and business competencies.
- **Action-Verb Dictionaries**: Curated lists of high-impact action verbs organized by domain (Leadership, Engineering, Research, Operations).
- **Flesch-Kincaid Readability Benchmarks**: Standardized readability scoring baselines for corporate recruitment documents.

### 3. Base Model & Inference Lineage

- **Deterministic Linguistic Linters**: Regex parsers, keyword extraction, section completeness checkers, and mathematical formula scorers executed via deterministic Python / TypeScript algorithms.
- **AI Career Copilot**: High-capability foundation models (`gemini-2.0-flash`, `gpt-4o`, `claude-3-5-sonnet`) utilized for semantic skill correlation, resume bullet improvement suggestions, and cover letter synthesis.
- **Zero Training on Candidate Resumes**: Uploaded resumes, personal contact information, work achievements, and employment histories are never used to train public foundation models.

### 4. Data Privacy, Storage, and Retention

- **FERPA & GDPR Compliance**: In full accordance with FERPA and GDPR (Articles 5, 17, and 28), all student and professional employment records are treated as confidential assets with encryption at rest and in transit.
- **Candidate Data Purging**: Resumes and extracted profile data can be permanently deleted by the candidate at any time with verifiable 0-byte database purging.
- **Zero Commercial Monetization**: CareerCraft never sells candidate resumes, job application records, or contact information to third-party recruitment agencies or advertisers.

---

## Limitations

Understanding the operational boundaries and technical constraints of CareerCraft Agent is essential for effective career preparation.

### 1. Complex Multi-Column & Graphic PDF Formatting Artifacts
- **Limitation**: Resumes designed with complex multi-column tables, visual skill rating bars, or non-standard graphical headers can cause text extraction order scrambles in standard PDF parsers.
- **Mitigation**: The agent evaluates raw text extraction flows and explicitly warns candidates when layout structures threaten ATS readability.

### 2. Niche Technical Terminology & Emerging Job Titles
- **Limitation**: Highly specialized domain jargon or newly created job titles may not yet exist in standard skill taxonomy dictionaries, leading to potential under-scoring in keyword matching.
- **Mitigation**: The system combines strict keyword intersection with dense semantic vector similarity, identifying conceptually related proficiencies even when exact terms differ.

### 3. Proprietary ATS Vendor Algorithm Diversity
- **Limitation**: Enterprise ATS vendors (Workday, Taleo, Greenhouse, Lever, iCIMS) each employ proprietary, undocumented parsing heuristics and ranking algorithms.
- **Mitigation**: CareerCraft optimizes for the highest common denominator of universal ATS best practices: standard semantic headings, clean text flow, high keyword density, and reverse-chronological structures.

### 4. Inability to Assess In-Person Soft Skills & Culture Fit
- **Limitation**: While the agent evaluates resume text and covers letter tone, it cannot evaluate verbal communication, charisma, emotional intelligence, or team culture fit demonstrated during interviews.
- **Mitigation**: The platform positions its tools as application optimization aids, encouraging candidates to pair resume refinement with live mock interview practice.

### 5. Subjective Hiring Manager Discretion
- **Limitation**: Even a 100% ATS-optimized resume remains subject to human recruiter preferences, team dynamics, and competitive candidate pools.
- **Mitigation**: The agent focuses on maximizing interview callback probability through clear, metric-driven accomplishment framing without making unrealistic guarantees of employment.

---

## Summary & Compliance Checklist

| Checkpoint 2 Requirement | Corresponding Section | Status |
| :--- | :--- | :---: |
| **How the agent decides** | [How the Agent Decides](#how-the-agent-decides) | **Covered** |
| - Decision architecture & 5-stage pipeline | Section 1 | Verified |
| - ATS scoring & semantic job fit formulas | Section 2 | Verified |
| - Thresholding, anti-fabrication & refusal criteria | Section 3 | Verified |
| - Fallback decision mechanism & heuristic NLP | Section 4 | Verified |
| - Human-in-the-loop & candidate approval | Section 5 | Verified |
| **The data it uses** | [The Data It Uses](#the-data-it-uses) | **Covered** |
| - Ingested resumes, job descriptions & preferences | Section 1 | Verified |
| - Configuration, skill taxonomies & readability baselines | Section 2 | Verified |
| - Base model lineage & deterministic linters | Section 3 | Verified |
| - Data privacy, 0-byte retention & FERPA/GDPR | Section 4 | Verified |
| **Its limitations** | [Limitations](#limitations) | **Covered** |
| - Complex multi-column graphic PDF parsing artifacts | Section 1 | Verified |
| - Niche technical terminology & emerging job titles | Section 2 | Verified |
| - Proprietary ATS vendor algorithm diversity | Section 3 | Verified |
| - Inability to assess in-person soft skills & culture fit | Section 4 | Verified |
| - Subjective hiring manager discretion | Section 5 | Verified |
