---
name: ats-resume-evaluator
description: Structural parsing, ATS formatting compliance auditing, action-verb analysis, and readability scoring for resumes.
---

# ATS Resume Evaluator Skill

## Overview
The `ats-resume-evaluator` skill parses uploaded candidate resumes (PDF/DOCX), simulates Applicant Tracking System (ATS) extraction behaviors, audits section completeness, and calculates structural readability and action-verb impact scores.

## Core Capabilities
- **Section Completeness Verification**: Checks for essential ATS sections: Contact Information, Summary, Work Experience, Education, and Skills.
- **Action-Verb & Metric Quantification**: Evaluates bullet points for strong active verbs and measurable outcomes ($X\% \text{ improvement}$, $\$Y\text{ impact}$).
- **Layout & Readability Auditing**: Flags unsearchable graphic elements, multi-column tables, non-standard fonts, and computes Flesch-Kincaid readability indices.
- **ATS Score Computation**: Generates a composite ATS Parsability Score ($0-100$).

## Inputs
- `resume_text`: Parsed raw text stream from candidate document.
- `file_format`: Format of the uploaded file (`pdf`, `docx`).
- `layout_metadata`: Structural observations regarding columns, tables, and images.

## Outputs
- `ats_score`: Composite numerical score ($0-100$).
- `section_breakdown`: Scores across completeness, impact, formatting, and readability.
- `prioritized_feedback`: Ranked list of actionable improvements to boost ATS compatibility.
