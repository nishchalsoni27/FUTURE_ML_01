# ⚔ Resume / Candidate Screening System
### Task 3 — Machine Learning Project
**Made by Nishchal Soni** · God of War 2018 Dark Theme

---

## 📌 Overview

A fully offline, browser-based **ML-powered Resume Screening System** that automatically ranks candidates against a job role using Natural Language Processing and similarity scoring — no server, no backend, no internet required.

Open `resume_screening_gow.html` in any modern browser and it works instantly.

---

## 🎯 Features

| Feature | Description |
|---|---|
| **Resume Text Cleaning & Parsing** | Tokenizes, lowercases, and normalizes raw resume text |
| **Skill Extraction & Matching** | Regex-based keyword matching against required skills list |
| **TF-IDF Cosine Similarity** | Vectorizes JD and resume, measures semantic closeness |
| **Candidate Ranking** | Sorts all candidates by weighted composite score (0–100) |
| **Skill Gap Identification** | Highlights matched skills (✓ green) and missing skills (✗ red) |
| **Experience Fit Scoring** | Matches candidate years of experience to the selected level |
| **CSV / JSON Export** | Download results for use in spreadsheets or pipelines |
| **Sample Data Auto-Load** | Comes pre-loaded with ML Engineer job + 4 sample candidates |

---

## 🧠 How the ML Scoring Works

The scoring engine is a weighted combination of four signals:

```
Final Score (0–100) =
  Skill Match Score   (50%)  — matched skills / total required skills
+ TF-IDF Similarity   (30%)  — cosine similarity between JD and resume vectors
+ Experience Fit      (10%)  — years of experience vs selected level
+ Keyword Density     (10%)  — job keywords found in resume tokens
```

### Step-by-Step Pipeline

**1. Tokenization**
```
resume text → lowercase → remove punctuation → split into word tokens
```

**2. Skill Extraction (NLP keyword matching)**
```
For each required skill:
  regex pattern = \b<skill>\b  (word boundary match)
  if pattern found in resume → matched
  else → missing (skill gap)
```

**3. TF-IDF Vectorization**
```
TF (term frequency)  = occurrences of term / total tokens in document
IDF (inverse doc freq) = log( (N+1) / (df+1) ) + 1
TF-IDF weight = TF × IDF
```
Applied to both the Job Description and each Resume to produce sparse vectors.

**4. Cosine Similarity**
```
similarity = (JD_vector · Resume_vector) / (|JD_vector| × |Resume_vector|)
Range: 0 (no overlap) → 1 (identical)  →  scaled to 0–30 points
```

**5. Final Ranking**
Candidates are sorted descending by total score and labeled:

| Score | Label |
|---|---|
| ≥ 75 | 🥇 CHAMPION |
| ≥ 60 | ✅ WORTHY |
| ≥ 40 | ⚔ CONTENDER |
| < 40 | ✗ UNWORTHY |

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| **Language** | Python *(production)* · Vanilla JS *(this demo)* |
| **NLP** | spaCy / NLTK (tokenization, lemmatization, keyword extraction) |
| **ML Library** | Scikit-learn (TfidfVectorizer, cosine_similarity) |
| **Frontend** | Pure HTML5 + CSS3 + JavaScript — zero dependencies |
| **Fonts** | Google Fonts: Cinzel Decorative, Cinzel, Rajdhani |
| **Environment** | Jupyter Notebook (prototyping) → Browser (deployment) |

---

## 🚀 Getting Started

### Run the Demo (Instant)
```
1. Download resume_screening_gow.html
2. Double-click to open in any browser (Chrome, Firefox, Edge, Safari)
3. Click "SCREEN & RANK CANDIDATES"
```
No installation. No internet. No backend.

### Python Production Version (Scikit-learn)
```bash
pip install scikit-learn spacy nltk pandas
python -m spacy download en_core_web_sm

# Then run:
python resume_screener.py --job "ML Engineer" --resumes ./resumes/
```

---

## 📁 Project Structure

```
resume-screening-system/
│
├── resume_screening_gow.html   ← Full working demo (open in browser)
├── demo.html                   ← Project showcase / presentation page
├── README.md                   ← This file
│
├── src/                        ← Python production code (extend here)
│   ├── screener.py             ← Main screening pipeline
│   ├── nlp_utils.py            ← Tokenization, skill extraction
│   ├── tfidf_engine.py         ← TF-IDF + cosine similarity
│   └── ranker.py               ← Scoring weights + sorting
│
├── data/
│   ├── sample_resumes/         ← Test resume text files
│   └── job_descriptions/       ← Sample JD files
│
└── notebooks/
    └── Resume_Screening.ipynb  ← Jupyter notebook walkthrough
```

---

## 📊 Skills Gained

- Text preprocessing and cleaning (NLP pipeline)
- Feature extraction from unstructured text
- TF-IDF vectorization and cosine similarity
- Weighted scoring and ranking models
- Resume parsing and keyword matching
- Skill gap identification and analysis
- Offline web application development

---

## 👤 Author

**Nishchal Soni**
Task 3 — Resume / Candidate Screening System
Machine Learning · NLP · Python · Scikit-learn

---

*"The measure of a true warrior is not in brute force, but in the precision of every strike."*
*— God of War, 2018*
