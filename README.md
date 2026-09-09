# Transfer Learning for Fake Reviews Across Domain Boundaries

Detecting AI-generated fake reviews across domain boundaries (Amazon & Yelp) using classical ML and transformer-based transfer learning.

---

## Key Results at a Glance

| Metric | Value |
|---|---|
| **DistilBERT in-domain accuracy (Amazon)** | **98.37%** |
| **Best classical ML accuracy (Linear SVM)** | **91.64%** |
| **Cross-domain zero-shot accuracy** | **~51%** (near random) |
| **Cross-domain with transfer learning** | **67.79%** |
| **Improvement via transfer learning** | **+16.3%** absolute gain |
| **Total reviews analyzed** | **399,484** (40K Amazon + 359K Yelp) |

> **The core challenge**: A model trained on Amazon reviews achieves 98% accuracy in-domain, but collapses to 51% (random chance) when tested on Yelp — a 47% accuracy drop due to domain shift. Transfer learning recovers 16% of this gap.

---

## Problem Statement

Fake reviews erode trust in online platforms. While detection models perform well within a single domain, they fail catastrophically when applied to a different platform due to differences in writing style, product categories, and user behavior. This project quantifies this **domain shift problem** and evaluates how much transfer learning can recover.

---

## Approach

1. **Data Preprocessing** — Standardize labels, clean text (HTML, URLs, encoding artifacts), remove duplicates
2. **Feature Engineering** — Extract linguistic features: text length, word count, sentence count, vocabulary richness, average word length
3. **Exploratory Analysis** — Identify domain-specific patterns (vocabulary richness, word distributions, n-gram frequencies)
4. **Classical ML Baseline** — Train Logistic Regression, SVM, Random Forest, XGBoost on source domain
5. **Deep Learning** — Fine-tune DistilBERT for sequence classification
6. **Cross-Domain Evaluation** — Test zero-shot transfer (Amazon → Yelp, Yelp → Amazon)
7. **Transfer Learning** — Incrementally add 5–75% target domain data to measure adaptation

---

## Dataset Overview

| Dataset | Reviews | Domain | Label Distribution |
|---|---|---|---|
| Amazon | 40,432 | Product reviews (Home & Kitchen) | ~50/50 genuine vs AI-generated |
| Yelp | 359,052 | Restaurant reviews | ~90% genuine, ~10% fake (balanced to 50K for experiments) |

- **Amazon labels**: CG (computer-generated) → fake, OR (original) → genuine
- **Yelp labels**: -1 (fake), 1 (genuine)
- Both datasets cleaned: duplicates removed, reviews < 20 chars filtered, HTML/URLs stripped

---

## Models Evaluated

### Classical ML
- Logistic Regression
- Linear SVM
- Random Forest
- XGBoost

### Deep Learning
- **DistilBERT** — Pre-trained transformer fine-tuned for sequence classification

---

## Results

### In-Domain Performance

*Train and test on the same domain.*

| Model | Amazon Accuracy | Yelp Accuracy |
|---|---|---|
| DistilBERT | **98.37%** | — |
| Linear SVM | 91.64% | 62.61% |
| Logistic Regression | 90.91% | **66.38%** |
| Random Forest | 90.67% | 65.40% |
| XGBoost | 90.84% | 66.09% |

> **Finding**: Amazon in-domain accuracy reaches 98% with DistilBERT and 91% with classical ML. Yelp is significantly harder — best in-domain accuracy is only 66%, likely due to noisier labels and more diverse writing styles.

### Cross-Domain Zero-Shot Transfer

*Train on one domain, test on the other — no target domain data used.*

| Model | Amazon → Yelp | Yelp → Amazon |
|---|---|---|
| XGBoost | 51.45% | **54.58%** |
| Linear SVM | 51.38% | 53.33% |
| Logistic Regression | 51.38% | 52.95% |
| Random Forest | 51.17% | 53.67% |
| DistilBERT | **50.63%** | — |

> **Critical finding**: All models collapse to ~51% accuracy (near random) in the Amazon → Yelp direction. F1 scores drop to 0.02–0.09 — models essentially predict "genuine" for every review. The Yelp → Amazon direction is slightly better (~54%) but still unusable.

### Domain Adaptation via Transfer Learning

*Adding increasing percentages of Yelp data to the Amazon training set, tested on held-out Yelp data.*

#### Classical ML

| Yelp % Added | Logistic Reg. | Linear SVM | Random Forest | XGBoost |
|---|---|---|---|---|
| 5% | 56.86% | 56.74% | 53.42% | 56.32% |
| 10% | 57.90% | 58.15% | 55.64% | 58.15% |
| 25% | 59.67% | 59.09% | 59.79% | 59.70% |
| 50% | 61.31% | 60.57% | 61.46% | 61.35% |
| **75%** | **62.48%** | **61.72%** | **62.54%** | **62.63%** |

#### DistilBERT (Transfer Learning)

| Yelp % Added | Accuracy | F1 Score |
|---|---|---|
| 0% (zero-shot) | 50.75% | 0.043 |
| 5% | 62.28% | 0.621 |
| 10% | 63.44% | 0.634 |
| 25% | 65.68% | 0.657 |
| 50% | 67.03% | 0.668 |
| **75%** | **67.79%** | **0.678** |

> **Key result**: Transfer learning improves cross-domain accuracy from **51% → 67.8%** (+16.3% absolute gain) with DistilBERT, and from 51% → 62.6% with classical ML. Even adding just 5% target data provides a significant boost.

---

## Key Insights

1. **Domain shift is severe** — Models trained on Amazon lose ~47% accuracy when applied to Yelp (98% → 51%). This demonstrates that fake review detectors are not inherently portable across platforms.

2. **Transfer learning works** — Adding 5–75% target domain data recovers 10–16% of lost accuracy. The improvement is consistent and monotonic with more data.

3. **DistilBERT outperforms classical ML** — The transformer model achieves 98% in-domain (vs 91% classical) and 67.8% cross-domain with adaptation (vs 62.6% classical).

4. **Vocabulary richness is a strong discriminator** — AI-generated reviews show consistently lower vocabulary richness (0.77 vs 0.84 on Amazon), providing a robust cross-domain signal.

5. **Yelp → Amazon transfer is easier than Amazon → Yelp** — Classical ML models achieve ~54% in the Yelp → Amazon direction vs ~51% in reverse, suggesting Yelp's diverse patterns capture more generalizable features.

6. **Classical ML remains competitive** — With 91% in-domain accuracy and fast inference, classical models are viable for resource-constrained deployments where transformer inference is too expensive.

---

## Tech Stack

- Python 3.9+
- Jupyter Notebook
- **scikit-learn** — Classical ML models, TF-IDF vectorization, evaluation metrics
- **XGBoost** — Gradient boosting classifier
- **Transformers (HuggingFace)** — DistilBERT fine-tuning
- **PyTorch** — Deep learning backend
- **NLTK** — Tokenization, stopwords, stemming
- **Pandas / NumPy** — Data manipulation
- **Matplotlib / WordCloud** — Visualization

---

## Repository Structure

```
Transfer Learning for Fake Reviews Across Domain Boundaries/
├── Transfer Learning for Fake Reviews Across Domain Boundaries.ipynb  # Main notebook
├── experiments/
│   ├── classical-ml-fake-reviews.ipynb   # Classical ML experiments
│   ├── cross-domain-V2.ipynb             # Cross-domain evaluation v2
│   ├── cross-domain_under_no_distil.ipynb # Ablation without DistilBERT
│   └── transfer-learning-test.ipynb      # Transfer learning tests
├── data/                                  # Dataset files (not included)
└── README.md
```

---

## How to Run

1. Clone the repository
2. Place datasets in the `data/` folder:
   - `fake reviews dataset.csv` (Amazon)
   - `Labelled Yelp Dataset.csv` (Yelp)
3. Install dependencies:
   ```bash
   pip install scikit-learn xgboost transformers torch nltk pandas numpy matplotlib wordcloud
   ```
4. Open and run the main notebook:
   ```bash
   jupyter notebook "Transfer Learning for Fake Reviews Across Domain Boundaries.ipynb"
   ```

---

## Contributing

Contributions welcome — extending to more domains, adding deep learning baselines, or improving feature engineering. Fork and open a PR.
