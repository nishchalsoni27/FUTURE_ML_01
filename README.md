# Future Interns — Machine Learning Internship

Detailed documentation of the Machine Learning portfolio projects developed during my Machine Learning Internship Fellowship at **Future Interns** (Duration: 10/05/2026 – 10/06/2026). 

**Intern Name:** Nishchal Soni  
**Candidate ID (CIN):** FIT/MAY26/ML7655  
**Track Code:** ML  

---

## 📌 Overview

This repository serves as a centralized portfolio showcasing the end-to-end implementation of three core Machine Learning and Data Science tasks assigned during the internship. Each system has been designed, modeled, and packed into interactive web interfaces utilizing client-side evaluation engines.

---

## 🛠️ Task 1: Sales & Demand Forecasting System

### 📋 Project Overview
A comprehensive statistical and predictive modeling platform designed to evaluate historical retail data, forecast future demand cycles, and compute safety margins using confidence intervals.

### 🧠 Core Features & Methodologies
* **Time Series Modeling:** Offers comparative execution across multiple techniques:
    * *Simple Moving Average (SMA)* for localized baseline trends.
    * *Exponential Smoothing (ETS)* to weigh recent demand accurately.
    * *Linear Regression Trends* for long-term historical trajectories.
* **Confidence Metrics:** Mathematical derivation of a 90% confidence envelope around future projection arrays ($lo$ and $hi$ bounds).
* **Statistical Validation:** Computes real-time dynamic error evaluation over the final 6 months of historical metrics to gauge performance.

### 📂 Deliverables Included
* **Interactive Engine:** `Sales_Forecasting_Nishchal.html` — Includes historical canvas renderings, user-adjustable parameters, and dynamic metric summaries.

---

## 🛠️ Task 2: TicketSense — Support Ticket Classifier

### 📋 Project Overview
An automated Natural Language Processing (NLP) pipeline built to ingest unstructured user complaints, identify critical business intent, extract dynamic keywords, and tag prioritization levels instantly.

### 🧠 Core Features & Methodologies
* **Text Preprocessing:** Automated tokenization pipeline that filters raw input, maps relevant stop words, and standardizes casing.
* **Heuristic Intent Extraction & Classification:** Structural keyword scanning maps input logs directly into target functional buckets (e.g., Technical, Billing, Account).
* **Dynamic Priority Matrix:** Evaluates urgency structures based on high-impact keywords to output categorical operational metadata tags (`HIGH`, `MEDIUM`, `LOW`).
* **Session Audit Logging:** Appends dynamic rows to a localized execution ledger complete with real-time performance tracking tables.

### 📂 Deliverables Included
* **Interactive Engine:** `Support_Ticket_Classifier.html` — Featuring a fully responsive, modern dark-cyberpunk UI dashboard, interactive input panels, and session log monitors.

---

## 🛠️ Task 3: Resume / Candidate Screening System

### 📋 Project Overview
An intelligent algorithmic recruitment engine engineered to parse candidate profiles, cross-examine skills against formal job descriptions, and calculate a normalized suitability score for automated hiring pipelines.

### 🧠 Core Features & Methodologies
* **Text Cleaning & Parsing:** Normalizes structural strings extracted from plain text resumes and comprehensive multi-paragraph job briefs.
* **Skill Vectorization & Matching:** Parses tokenized data arrays to check for presence or absence of required professional skills.
* **Candidate Rank Scoring:** Implements a mathematical ranking matrix evaluating experience tiers and exact skill overlaps to sort candidates by structural alignment.
* **Skill Gap Identification:** Compares candidate profiles directly against target specs to flag exact missing competencies, helping recruiters identify areas for growth or upskilling.

### 📂 Deliverables Included
* **Interactive Engine:** `Resume_Screening_Gow.html` — Featuring a classical, high-contrast decorative UI framework complete with preloaded sample positions, bulk candidate matching modules, and real-time skill-tag generation.

---

## 🚀 How to Run the Applications Localized

Since these systems are bundled into optimized, highly reactive frontend environments that execute the mathematical logic on the client side, they require no external complex Python environments or server infrastructure to preview:

1. Clone this repository to your local system:
   ```bash
   git clone [https://github.com/nishchalsoni27/FUTURE_ML_01](https://github.com/nishchalsoni27/FUTURE_ML_01)
