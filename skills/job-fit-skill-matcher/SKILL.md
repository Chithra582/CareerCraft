---
name: job-fit-skill-matcher
description: Semantic skill-gap analysis, keyword coverage evaluation, and job-fit percentage matching against target job descriptions.
---

# Job-Fit Skill Matcher Skill

## Overview
The `job-fit-skill-matcher` skill extracts technical proficiencies, soft skills, and domain tools from target job descriptions, compares them against the candidate's profile, and computes a multi-factor job fit percentage.

## Core Capabilities
- **Job Description Parsing**: Automatically extracts mandatory qualifications, preferred skills, and experience benchmarks from raw job postings.
- **Semantic Skill Mapping**: Utilizes semantic embeddings and taxonomy synonym expansion to recognize equivalent competencies (e.g., Docker $\leftrightarrow$ Containerization).
- **Skill-Gap Categorization**: Segregates skills into `Matched`, `Missing Critical`, and `Transferable`.
- **Match Percentage Calculation**: Generates a normalized fit score ($0-100\%$) weighting mandatory versus preferred requirements.

## Inputs
- `candidate_skills`: Array of verified candidate skills and competencies.
- `job_description_text`: Raw text of the target job posting.

## Outputs
- `match_percentage`: Normalized alignment metric ($0-100\%$).
- `matched_skills`: Proficiencies satisfied by candidate experience.
- `missing_critical_skills`: Essential job requirements absent from candidate resume.
- `upskilling_recommendations`: Suggested courses, certifications, or portfolio project concepts to bridge gaps.
