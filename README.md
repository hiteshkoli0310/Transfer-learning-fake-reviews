# Cross-Domain-Fake-Review-Detection#  Cross-Domain Fake Review Detection using Metadata (Amazon & Yelp)

This project investigates fake review detection using classical machine learning models trained on metadata features rather than text. By evaluating performance across two different domains — **Amazon** and **Yelp** — it demonstrates the challenge of **domain shift** and shows how a small portion of target domain data can improve model adaptability through **fine-tuning**.

---
## Overview

- Models were trained using the **Amazon Review** dataset and tested on the **Yelp Review** dataset.
- Only **metadata features** and TF-IDF representations of titles and content were used — no deep linguistic analysis.
- The project assesses:
  - In-domain performance
  - Cross-domain performance (zero-shot)
  - Cross-domain performance with limited fine-tuning (5–10% Yelp data)

---

## Tech Stack

- Python 3.9+
- Jupyter Notebook
- scikit-learn
- XGBoost
- Pandas / NumPy / Matplotlib
- TF-IDF (via `sklearn.feature_extraction.text`)

---

## Models Used

- Logistic Regression
- Random Forest
- XGBoost
- Support Vector Machine (SVM)
- K-Nearest Neighbors (KNN)

---

## Dataset Info

### Amazon Dataset
- Columns used: `REVIEW_TITLE`, `REVIEW_TEXT`, `RATING`, `VERIFIED_PURCHASE`, `LABEL`
- Preprocessing:
  - Lowercasing and punctuation removal
  - Label encoding: `__label1__` as fake (0), `__label2__` as real (1)

### Yelp Dataset
- Columns used: `Review`, `Rating`, `Label`
- Balanced via downsampling
  - Only real reviews were downsampled to match the count of fake ones

> Datasets were stored locally. Ensure you have them in the `/data` folder or update the notebook path accordingly.

---


## Experiments

- **In-Domain Evaluation**
  - Trained on 80% of Amazon reviews
  - Validated on remaining 20%

- **Cross-Domain (Zero-Shot)**
  - Trained on Amazon only
  - Tested on Yelp (without adaptation)

- **Cross-Domain (Fine-Tuned)**
  - Amazon + 5–10% Yelp added to training set
  - Retrained and evaluated on Yelp test data

---

## Results

| Model                | In-Domain (Amazon) | Cross-Domain (Yelp) | Fine-Tuned (Yelp) |
|---------------------|--------------------|----------------------|--------------------|
| Logistic Regression | 91.00%             | 62.00%               | 71.00%             |
| Random Forest       | 88.50%             | 60.00%               | 69.20%             |
| XGBoost             | 89.00%             | 61.80%               | 70.10%             |
| SVM                 | 87.40%             | 58.90%               | 68.40%             |
| KNN                 | 85.30%             | 55.60%               | 66.50%             |

---

##  Learnings

- **Domain Shift** significantly impacts accuracy — models trained on Amazon perform poorly on Yelp.
- **Metadata-based models** can generalize better across domains than content-heavy models.
- Incorporating just **5–10% target-domain data** improves cross-domain performance meaningfully.
- Classical models remain competitive for explainability and performance in constrained environments.

---

## Contributing

If you want to improve this project — e.g., by adding more metadata features, extending to other domains, or comparing deep learning — feel free to fork it and open a pull request!

---

