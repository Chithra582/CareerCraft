# CareerCraft — Resume Evaluator & Job Match Assistant

<p align="left">
  <a href="agent.yaml"><img src="https://img.shields.io/badge/OpenGAP-0.1.0-blue.svg" alt="OpenGAP Spec"></a>
  <a href="https://app.hidevs.xyz/passport/submit"><img src="https://img.shields.io/badge/GitAgent%20Passport-Ready-green.svg" alt="GitAgent Passport Ready"></a>
  <a href="agent.yaml"><img src="https://img.shields.io/badge/Category-Education-purple.svg" alt="Category Education"></a>
  <a href="EXPLAINABILITY.md"><img src="https://img.shields.io/badge/Compliance-FERPA%20%7C%20GDPR-orange.svg" alt="Compliance FERPA | GDPR"></a>
</p>

CareerCraft is an **AI-powered career enhancement platform** designed to help job seekers optimize their resumes, evaluate job-fit, and generate tailored cover letters.  
It uses modern **AI, NLP, and web technologies** to simulate real-world Applicant Tracking Systems (ATS) and hiring workflows.

The platform provides actionable insights that improve resume quality, skill alignment, and overall job readiness.

---

## 🚀 Key Features

### 📝 Resume Analyzer (ATS Optimization)
- Upload **PDF / DOCX** resumes
- ATS-style scoring based on:
  - Keyword alignment
  - Resume structure & formatting
  - Readability
  - Section completeness
- Detailed improvement suggestions

---

### 🎯 Skill Match & Job Fit Scoring
- Paste or select a **target job description**
- Get:
  - Job match percentage
  - Identified missing skills
  - Role-specific improvement tips
- Personalized upskilling recommendations with learning resources

---

### ✍️ AI Cover Letter Generator
- Generates **professionally tailored cover letters**
- Uses:
  - Resume content
  - Job description insights
- Supports tone customization:
  - Formal
  - Confident
  - Friendly
- One-click **PDF export**

---

### 📊 User Dashboard & History Tracking
- Secure user authentication
- Store:
  - Resumes
  - Generated cover letters
  - Job match results
- Track progress across multiple applications
- Manage multiple resume versions

---

## 🧠 System Architecture

CareerCraft follows a **microservice-based architecture**:

CareerCraft/
├── frontend/ # User Interface (Next.js)  
├── backend/ # API & Authentication (Node.js / Express)  
└── ml-service/ # AI & NLP Engine (FastAPI)  

### Architecture Flow

Frontend → Backend → ML Service → Backend → Frontend


---

## 🛠️ Tech Stack

### Frontend
- Next.js 
- Tailwind CSS
- Axios

### Backend
- Node.js
- Express.js
- MongoDB
- JWT Authentication

### ML Service
- Python
- FastAPI
- NLP-based keyword & role matching
- Rule-based + AI-expandable models

---

## ⚙️ Setup & Installation

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/your-username/CareerCraft.git
cd CareerCraft
```

2️⃣ Start ML Service

```bash
cd ml-service
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload --port 8001
```

3️⃣ Start Backend

```bash
cd backend
npm install
npm run dev
```

4️⃣ Start Frontend

```bash
cd frontend
npm install
npm run dev
```

---

## 🤖 GitAgent Passport Qualification

This repository is compliant with the **OpenGAP Spec 0.1.0** standard and qualified for the [HiDevs GitAgent Passport](https://app.hidevs.xyz/passport/submit).

### Clearance Checkpoints Summary

| Checkpoint | Status | Focus Area | Artifact |
| :--- | :--- | :--- | :--- |
| **Checkpoint 1: Validate** | `PASSED` | Schema, Soul, Skills, Tools | [`agent.yaml`](agent.yaml), [`SOUL.md`](SOUL.md), [`skills/`](skills/), [`tools/`](tools/) |
| **Checkpoint 2: Explain** | `PASSED` | Decision Logic, Data Usage, Limitations | [`EXPLAINABILITY.md`](EXPLAINABILITY.md) |
| **Checkpoint 3: Export** | `PASSED` | Interoperability & Tool Schemas | [`tools/`](tools/), [`RULES.md`](RULES.md), [`DUTIES.md`](DUTIES.md) |

### Agent Architecture Overview

- **Identity & Ethics**: [`SOUL.md`](SOUL.md) defines core behavioral traits, candidate empowerment ethos, anti-bias principles, and truthful representation.
- **Operational Rules**: [`RULES.md`](RULES.md) establishes absolute constraints against credential fabrication, prohibits deceptive ATS keyword stuffing, and enforces FERPA/GDPR candidate privacy.
- **Role Duties**: [`DUTIES.md`](DUTIES.md) defines step-by-step responsibilities across multi-format resume ingestion, ATS layout auditing, semantic skill-gap matching, and tailored cover letter generation.
- **Transparent Reasoning**: [`EXPLAINABILITY.md`](EXPLAINABILITY.md) documents step-by-step rationale, deterministic ATS scoring models, skill fit algorithms, and operational boundaries.
- **Modular Skills**: Located in [`skills/`](skills/) for ATS evaluation, job-fit matching, cover letter synthesis, and career readiness advisory.
- **Tool Schemas**: Standardized JSON schemas located in [`tools/`](tools/) for document parsing, ATS score calculation, skill-gap analysis, and cover letter generation.

---

## 👨‍💻 Contributors

See CONTRIBUTORS for the full list of contributors.

---

## 📄 License

This project is licensed under the MIT License.

---

## ⭐ Acknowledgements

Inspired by real-world ATS systems and modern hiring workflows.  
Built for learning, experimentation, and real-world impact.
