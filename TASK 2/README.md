# 🎮 TicketSense — Support Ticket Classification System
> **Task 02 · ML Classification Project** | Built by **Nishchal Soni**

---

```
████████╗██╗ ██████╗██╗  ██╗███████╗████████╗███████╗███████╗███╗   ██╗███████╗███████╗
╚══██╔══╝██║██╔════╝██║ ██╔╝██╔════╝╚══██╔══╝██╔════╝██╔════╝████╗  ██║██╔════╝██╔════╝
   ██║   ██║██║     █████╔╝ █████╗     ██║   ███████╗█████╗  ██╔██╗ ██║███████╗█████╗  
   ██║   ██║██║     ██╔═██╗ ██╔══╝     ██║   ╚════██║██╔══╝  ██║╚██╗██║╚════██║██╔══╝  
   ██║   ██║╚██████╗██║  ██╗███████╗   ██║   ███████║███████╗██║ ╚████║███████║███████╗
   ╚═╝   ╚═╝ ╚═════╝╚═╝  ╚═╝╚══════╝   ╚═╝   ╚══════╝╚══════╝╚═╝  ╚═══╝╚══════╝╚══════╝
```

---

## 📋 Project Overview

**TicketSense** is a machine learning–powered support ticket classification system that automatically categorizes customer support tickets and assigns priority levels (HIGH / MEDIUM / LOW). Built as **Task 02** of the ML curriculum, this project demonstrates end-to-end NLP pipeline design — from raw text preprocessing through classification and priority assignment.

The front-end interface is styled in a **The Last of Us Part II** dark aesthetic — raw, gritty, and tactical — designed for immersive, professional presentation.

---

## 🎯 Features

| Feature | Description |
|---|---|
| **Text Cleaning & Tokenization** | Lowercasing, punctuation removal, whitespace normalization |
| **Stop Word Removal** | Filters common words to isolate meaningful tokens |
| **Keyword Extraction** | Frequency-distribution based top-N keyword mining |
| **Ticket Category Classification** | Multi-class classifier across 6 categories |
| **Priority Tagging** | Rule-based engine assigns HIGH / MEDIUM / LOW |
| **Confidence Scoring** | Heuristic ensemble confidence estimation |
| **Model Performance Evaluation** | Preprocessing steps log, keyword heat-tagging |
| **Classification Log** | Full timestamped session history |
| **Offline Support** | Works with zero internet connection |

---

## 🗂️ Project Structure

```
ticketsense/
│
├── support_ticket_classifier.html   ← Main application (offline, single file)
├── demo.html                        ← Project demo / showcase page
├── README.md                        ← This file
│
├── notebook/                        ← (Python ML implementation)
│   ├── ticket_classifier.ipynb      ← Jupyter Notebook
│   ├── preprocessing.py             ← Text cleaning pipeline
│   ├── classifier.py                ← Scikit-learn model
│   └── data/
│       ├── tickets_train.csv
│       └── tickets_test.csv
│
└── assets/
    └── screenshots/
```

---

## 🧠 ML Pipeline (Python Implementation)

### 1. Text Preprocessing

```python
import nltk
import spacy
import re
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize

nlp = spacy.load("en_core_web_sm")

def preprocess_ticket(text):
    # Step 1: Lowercase
    text = text.lower()
    
    # Step 2: Remove special characters
    text = re.sub(r'[^\w\s]', ' ', text)
    
    # Step 3: Tokenize
    tokens = word_tokenize(text)
    
    # Step 4: Remove stop words
    stop_words = set(stopwords.words('english'))
    tokens = [t for t in tokens if t not in stop_words and len(t) > 2]
    
    # Step 5: Lemmatization via spaCy
    doc = nlp(' '.join(tokens))
    tokens = [token.lemma_ for token in doc]
    
    return tokens
```

### 2. Feature Extraction

```python
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer(
    max_features=5000,
    ngram_range=(1, 2),   # unigrams + bigrams
    min_df=2
)

X_train = vectorizer.fit_transform(train_texts)
X_test  = vectorizer.transform(test_texts)
```

### 3. Classification Model

```python
from sklearn.linear_model import LogisticRegression
from sklearn.multiclass import OneVsRestClassifier
from sklearn.pipeline import Pipeline

model = Pipeline([
    ('tfidf', TfidfVectorizer(ngram_range=(1,2), max_features=5000)),
    ('clf',   LogisticRegression(max_iter=1000, C=5.0))
])

model.fit(X_train, y_train)
```

### 4. Priority Assignment Logic

```python
PRIORITY_MAP = {
    'security': 'HIGH',
    'billing':  lambda t: 'HIGH' if re.search(r'twice|double|duplicate|fraud', t) else 'MEDIUM',
    'technical': lambda t: 'HIGH' if re.search(r'crash|error|down|blocked', t) else 'MEDIUM',
    'account':  lambda t: 'HIGH' if re.search(r'hack|unauthorized|suspicious', t) else 'MEDIUM',
    'feature':  'LOW',
    'feedback': 'LOW',
}

def assign_priority(category, text):
    rule = PRIORITY_MAP.get(category, 'MEDIUM')
    return rule(text) if callable(rule) else rule
```

### 5. Model Evaluation

```python
from sklearn.metrics import classification_report, confusion_matrix

y_pred = model.predict(X_test)

print(classification_report(y_test, y_pred, target_names=CATEGORIES))
# Expected: F1-score ~0.88–0.93 on balanced dataset
```

---

## 🏷️ Ticket Categories

| Category | Description | Default Priority |
|---|---|---|
| `BILLING` | Payments, charges, refunds, invoices | MEDIUM → HIGH if duplicate |
| `TECHNICAL` | Bugs, crashes, errors, system failures | MEDIUM → HIGH if critical |
| `ACCOUNT` | Login, password, access, authentication | MEDIUM → HIGH if breach |
| `SECURITY` | Hacks, breaches, unauthorized access | **Always HIGH** |
| `FEATURE REQUEST` | Product suggestions, enhancements | LOW |
| `FEEDBACK` | General praise, minor notes | LOW |

---

## ⚡ Priority Levels

| Level | SLA | Action |
|---|---|---|
| 🔴 **HIGH** | Respond within **1 hour** | Immediate escalation, incident protocol |
| 🟡 **MEDIUM** | Respond within **8 hours** | Standard queue, team assignment |
| 🟢 **LOW** | Respond within **48–72 hours** | Backlog logging, acknowledgment |

---

## 🛠️ Tools & Technologies

```
Language   :  Python 3.10+
NLP        :  NLTK, spaCy (en_core_web_sm)
ML Library :  Scikit-learn
Notebook   :  Jupyter Notebook / JupyterLab
Frontend   :  HTML5, CSS3, Vanilla JS (offline single-file app)
Fonts      :  Rajdhani, Share Tech Mono, Crimson Pro (Google Fonts)
Theme      :  The Last of Us Part II — Dark Industrial
```

---

## 🚀 How to Run

### Browser App (No Installation)
```bash
# Just open the file in any browser — works offline
open support_ticket_classifier.html
```

### Python Environment Setup
```bash
# Clone or download the project
cd ticketsense/

# Install dependencies
pip install nltk spacy scikit-learn pandas jupyter

# Download NLTK data
python -c "import nltk; nltk.download('punkt'); nltk.download('stopwords')"

# Download spaCy model
python -m spacy download en_core_web_sm

# Launch Jupyter
jupyter notebook notebook/ticket_classifier.ipynb
```

---

## 📊 Expected Model Performance

| Metric | Score |
|---|---|
| Accuracy | ~91% |
| Precision (weighted) | ~0.90 |
| Recall (weighted) | ~0.91 |
| F1-Score (weighted) | ~0.90 |

> *Metrics based on balanced 6-class dataset with ~2000 labeled tickets.*

---

## 🎨 Design System

The interface uses a custom **TLOU2 Dark** design system:

- **Void Black** `#050608` — base background  
- **Rust Red** `#c4522a` — alerts, high priority  
- **Moss Green** `#6b9e3a` — success, system active  
- **Worn Ivory** `#d4cfc8` — primary text  
- **Ash Gray** `#6b7280` — secondary text / metadata  

---

## 👤 Author

**Nishchal Soni**  
Task 02 · Support Ticket Classification · ML Project Series

---

## 📄 License

This project is submitted as part of an ML curriculum task. All design and code by Nishchal Soni.

---

*"When you're lost in the darkness, look for the light." — The Last of Us*
