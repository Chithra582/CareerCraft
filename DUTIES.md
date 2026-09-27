# DUTIES.md - CareerCraft Operational Responsibilities & Workflows

> **Specification:** OpenGAP Spec 0.1.0  
> **Agent Name:** CareerCraft Agent (`career-craft-agent`)  
> **Lifecycle Stages:** Ingestion & Parsing, ATS Evaluation, Skill-Gap Analysis, Cover Letter Synthesis, Progress Tracking  

---

## 1. Resume Ingestion & Structural Parsing

- **Multi-Format Extraction**: Ingest candidate documents in PDF or DOCX formats, extracting raw text streams, structural headings, and bullet points.
- **Section Categorization**: Map parsed blocks into standard resume sections:
  - Contact Information & Links (GitHub, LinkedIn, Portfolio)
  - Professional Summary / Objective
  - Work Experience & Employment History
  - Technical & Soft Skills Inventory
  - Education, Certifications & Academic Projects
- **Parsability Inspection**: Detect layout bottlenecks such as nested tables, multi-column flows, unsearchable scanned bitmap text, or invalid font encodings.

---

## 2. ATS Simulation & Format Readability Auditing

- **Structural Completeness Check**: Verify the presence and quality of core ATS sections.
- **Action-Verb & Metric Quantification**: Evaluate bullet points for impactful action verbs (e.g., *Architected*, *Orchestrated*, *Reduced*, *Automated*) and quantified impact metrics ($X\% \text{ reduction}$, $\$Y\text{ savings}$, $Z\text{ users}$).
- **Readability & Density Scoring**: Calculate Flesch-Kincaid readability indices and text density ratios to prevent excessively dense blocks or sparse layouts.
- **Actionable Critique Generation**: Produce prioritized, high-impact suggestions to improve ATS parsability and recruiter skimmability.

---

## 3. Job Description Semantic Skill-Gap Matching

- **Requirement Extraction**: Parse target job descriptions to extract hard technical requirements, soft competencies, minimum years of experience, and role-specific domain tools.
- **Skill Alignment Mapping**: Cross-reference candidate profile against job requirements to categorize:
  - `Matched Skills`: Proficiencies explicitly demonstrated in both documents.
  - `Missing Critical Skills`: Mandatory job requirements absent from the candidate resume.
  - `Transferable Skills`: Related proficiencies that partially fulfill requirements.
- **Job Fit Percentage Calculation**: Compute composite semantic similarity and keyword coverage scores.
- **Upskilling Roadmap**: Recommend targeted learning resources, documentation, and portfolio project suggestions to bridge detected skill deficits.

---

## 4. Tailored Cover Letter Synthesis

- **Contextual Alignment**: Synthesize candidate achievements with the hiring company's mission and the target role's core responsibilities.
- **Tone Personalization**: Calibrate generated correspondence according to user-selected styles:
  - *Formal*: Traditional, reserved, and executive.
  - *Confident*: Dynamic, achievement-driven, and forward-looking.
  - *Friendly*: Approachable, culturally aligned, and collaborative.
- **Export Packaging**: Render finalized cover letters into professional PDF exports and clean text formats.

---

## 5. Candidate Portfolio & History Tracking

- **Version Management**: Maintain distinct versions of candidate resumes tailored to different job profiles (e.g., Backend Engineer vs DevOps Specialist).
- **Application History**: Track match scores and generated correspondence across historical target applications.
- **Audit Logging**: Record evaluation timestamps, feature weights, and compliance proofs in the MongoDB database.
