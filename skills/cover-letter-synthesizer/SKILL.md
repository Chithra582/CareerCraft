---
name: cover-letter-synthesizer
description: Tailored cover letter synthesis grounded in verified candidate achievements, calibrated to user-selected tones and target roles.
---

# Cover Letter Synthesizer Skill

## Overview
The `cover-letter-synthesizer` skill generates customized, high-impact professional cover letters that align a candidate's genuine career accomplishments with the target company's objectives, without hallucinating false credentials.

## Core Capabilities
- **Factual Accomplishment Grounding**: Draws exclusively from verified resume experiences and user-highlighted milestones.
- **Tone & Voice Customization**: Calibrates prose according to user preference: *Formal* (corporate/executive), *Confident* (growth-stage/impact-focused), or *Friendly* (collaborative/startup).
- **Structure Optimization**: Follows proven recruitment storytelling frameworks: Hook, Value Proposition, Technical Alignment, and Call to Action.
- **Export Packaging**: Formats outputs for clean copy-pasting or rendering into styled PDF documents.

## Inputs
- `resume_summary`: Extracted highlights from candidate profile.
- `job_description`: Target role title, company name, and key objectives.
- `tone`: Selected stylistic voice (`formal`, `confident`, `friendly`).

## Outputs
- `cover_letter_markdown`: Formatted cover letter draft.
- `word_count`: Total word length of the generated correspondence.
- `customization_notes`: Specific candidate achievements highlighted in the text.
