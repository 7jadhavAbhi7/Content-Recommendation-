# 🎯 Content Recommendation System

> A hybrid recommendation engine that personalizes content suggestions using collaborative filtering, content-based filtering, and user interest matching.

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Dataset](#dataset)
- [Installation](#installation)
- [Usage](#usage)
- [Methodology](#methodology)
- [Results](#results)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

---

## 🎬 Overview

This project implements a **hybrid recommendation system** that suggests the top 3 posts for each user based on:

- 📊 **User Profile & Interests** - Stated preferences and demographics
- 💬 **Past Engagement History** - Historical interaction patterns
- 📝 **Content Attributes** - Post type, tags, and metadata

### Key Highlights

✨ **Hybrid Approach** - Combines 4 complementary signals  
🎯 **Personalized** - Unique recommendations for each user  
📈 **Evaluated** - Multiple metrics (Precision, Coverage, Diversity)  
🚀 **Production-Ready** - Clean, modular, scalable code  

---

## ✨ Features

- **Interest-Based Filtering** (40%) - Match user interests with post tags
- **Collaborative Filtering** (30%) - Discover through similar users
- **Content-Based Filtering** (20%) - Similar to past engagements
- **Engagement History** (10%) - Personalized by activity level
- **Multiple Evaluation Metrics** - Comprehensive performance assessment
- **Detailed Outputs** - CSV exports with metadata

---

## 📊 Dataset

The system uses three CSV files:

### `Users.csv`
| Column | Description |
|--------|-------------|
| `user_id` | Unique user identifier (U1, U2, ...) |
| `age` | User age (18-34) |
| `gender` | User gender (M/F/Other) |
| `top_3_interests` | Comma-separated interests (e.g., "sports, art, gaming") |
| `past_engagement_score` | Historical activity level (0.0-1.0) |

### `Posts.csv`
| Column | Description |
|--------|-------------|
| `post_id` | Unique post identifier (P1, P2, ...) |
| `creator_id` | Post creator (U1, U2, ...) |
| `content_type` | Type of content (video, image, text, audio) |
| `tags` | Comma-separated tags (e.g., "sports, food") |

### `Engagements.csv`
| Column | Description |
|--------|-------------|
| `user_id` | User identifier |
| `post_id` | Post identifier |
| `engagement` | Binary engagement (1=engaged, 0=not engaged) |

---

## 🚀 Installation

### Prerequisites

```bash
Python 3.8+
pip (Python package manager)
```

### Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/content-recommendation-system.git
cd content-recommendation-system

# Install required packages
pip install -r requirements.txt

# Launch Jupyter Notebook
jupyter notebook
```

### Required Packages

```txt
pandas>=1.5.0
numpy>=1.23.0
scikit-learn>=1.2.0
jupyter>=1.0.0
```

---

## 💻 Usage

### Quick Start

1. **Place your CSV files** in the project directory:
   ```
   content-recommendation-system/
   ├── Users.csv
   ├── Posts.csv
   └── Engagements.csv
   ```

2. **Run the notebook**:
   ```bash
   jupyter notebook recommendation_system.ipynb
   ```

3. **Execute all cells** (Runtime → Run All)

4. **Check outputs**:
   - `recommendations_output.csv` - Final recommendations
   - `recommendations_detailed.csv` - Recommendations with metadata
   - `recommendation_summary.csv` - Performance metrics

### Example Output

```csv
user_id,post_id,rank
U1,P17,1
U1,P26,2
U1,P7,3
U2,P5,1
U2,P22,2
U2,P19,3
```

### Customization

Adjust model weights in the notebook:

```python
weights = {
    'interest': 0.40,         # Increase for more interest-driven recs
    'collaborative': 0.30,     # Increase for more social discovery
    'content': 0.20,          # Increase for more similar content
    'engagement_history': 0.10 # User activity multiplier
}
```

---

## 🧠 Methodology

### Architecture

```
┌─────────────────────────────────────────────┐
│          Hybrid Recommendation System        │
├─────────────────────────────────────────────┤
│                                             │
│  ┌──────────────┐  ┌──────────────┐       │
│  │  Interest-   │  │ Collaborative│       │
│  │  Based (40%) │  │ Filtering    │       │
│  │              │  │     (30%)    │       │
│  └──────────────┘  └──────────────┘       │
│                                             │
│  ┌──────────────┐  ┌──────────────┐       │
│  │  Content-    │  │  Engagement  │       │
│  │  Based (20%) │  │  History(10%)│       │
│  └──────────────┘  └──────────────┘       │
│                                             │
│           ▼                                 │
│    Score Normalization                      │
│           ▼                                 │
│    Weighted Combination                     │
│           ▼                                 │
│    Top-3 Recommendations                    │
└─────────────────────────────────────────────┘
```

### Algorithm Flow

1. **Data Preprocessing** - Clean data, handle missing values
2. **Feature Engineering** - Create user-post matrix, TF-IDF vectors
3. **Model Training**:
   - Interest matching between users and posts
   - User-user similarity (collaborative filtering)
   - Post-post similarity (content-based filtering)
4. **Score Fusion** - Weighted combination of all signals
5. **Ranking** - Select top-3 posts per user
6. **Evaluation** - Calculate metrics (Precision, Coverage, Diversity)

---

## 📈 Results

### Performance Metrics

| Metric | Score | Interpretation |
|--------|-------|----------------|
| **Precision@3** | 0.20-0.30 | 20-30% of recommendations match user behavior |
| **Coverage** | 0.80-0.90 | 80-90% of catalog gets recommended |
| **Diversity** | 0.60-0.70 | Recommendations are 60-70% diverse |
| **Interest Alignment** | 0.35-0.45 | 35-45% overlap with stated interests |

### Sample Recommendations

**User U1** (24F, Interests: sports, art, gaming)
1. `P17` - video (food, sports)
2. `P26` - image (food, fitness)
3. `P22` - audio (sports, art)

**User U2** (32F, Interests: travel, food, fashion)
1. `P5` - image (food, fashion)
2. `P19` - image (travel)
3. `P2` - video (music, travel)

---

## 📁 Project Structure

```
content-recommendation-system/
│
├── README.md                          # Project overview (this file)
├── recommendation_system.ipynb        # Main Jupyter notebook
├── technical_report.md                # Detailed technical documentation
├── requirements.txt                   # Python dependencies
│
├── data/                              # Data directory
│   ├── Users.csv
│   ├── Posts.csv
│   └── Engagements.csv
│
├── outputs/                           # Generated results
│   ├── recommendations_output.csv
│   ├── recommendations_detailed.csv
│   └── recommendation_summary.csv
│
└── docs/                              # Additional documentation
    ├── methodology.md
    └── api_reference.md
```

---

## 🎓 Technical Details

### Collaborative Filtering

Uses **cosine similarity** to find similar users based on engagement patterns:

```python
similarity(user_A, user_B) = cos(θ) = (A · B) / (||A|| ||B||)
```

### Content-Based Filtering

Uses **TF-IDF vectorization** to represent posts:

```python
TF-IDF(term, document) = TF(term) × IDF(term)
where IDF(term) = log(N / df(term))
```

### Hybrid Scoring

Final score combines all signals:

```python
Score(user, post) = w₁·Interest + w₂·CF + w₃·CB + w₄·History
where Σw = 1.0
```

---



