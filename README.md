# Patient Lifestyle Similarity Model (KNN)  
**Healthcare-Focused Machine Learning Project**

---

## 1. Project Overview

### What this project is about
This project builds a **Patient Lifestyle Similarity Model** using **K-Nearest Neighbors (KNN)** to classify obesity categories based on lifestyle habits and physical attributes.

Rather than optimizing for maximum accuracy, the primary goal is to **demonstrate deep understanding of distance-based learning and its implications in healthcare decision-support systems**, including interpretability, failure modes, and ethical limitations.

### Industry Context
- **Industry:** Healthcare / Health Analytics
- **Use Case:** Decision-support, population health analysis, lifestyle similarity modeling  
- **Not a medical diagnostic tool**

### Machine Learning Model Used
- **Model:** K-Nearest Neighbors (KNN)
- **Distance Metrics:** Euclidean (L2) and Manhattan (L1)
- **Validation Strategy:** Stratified cross-validation
- **Interpretability:** Similar-patient (neighbor-based) reasoning

### Project Goal
To answer the question:

> *"How does patient similarity based on lifestyle behaviors compare to similarity dominated by weight-based proxies, and what are the risks of each approach in healthcare ML?"*

---

## 2. Dataset

### Dataset Origin
- **Source:** UCI Machine Learning Repository  
- **Dataset:** *Estimation of Obesity Levels Based on Eating Habits and Physical Condition*  
- **Link:**  
  https://archive.ics.uci.edu/dataset/544/estimation+of+obesity+levels+based+on+eating+habits+and+physical+condition

### Target Variable
- `NObeyesdad` — Multi-class obesity categories

### Important Dataset Limitation
The dataset **does not contain body composition metrics**, such as:
- Body fat percentage
- Muscle mass
- Lean mass
- Bone density
- Waist circumference

As a result, obesity labels are **largely correlated with weight/height proxies**, not true physiological health.

---

## 3. Project Structure

```
healthcare-knn-project/
│
├── data/
│   ├── raw/                      # Original dataset
│   ├── processed/                # KNN-ready feature matrices
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_distance_metrics.ipynb
│   ├── 03_knn_training.ipynb
│   ├── 04_cross_validation.ipynb
│
├── results/
│   ├── metrics.json              # Cross-validation results
│   ├── demo_predictions.json     # Interactive demo outputs
│
├── README.md
```

---

## 4. Notebook Breakdown (What Was Done)

### Notebook 01 — Data Exploration
**Purpose:** Understand the dataset in a healthcare context.

**Key work:**
- Identified numerical vs categorical features
- Examined target class distribution
- Checked realistic value ranges
- Framed features as *lifestyle behaviors* vs *physical proxies*

**Outcome:**
- Established that similarity must be defined carefully in healthcare ML.

---

### Notebook 02 — Distance Metrics & Preprocessing
**Purpose:** Define what "similarity" means for KNN.

**Key work:**
- Binary encoding (yes/no, gender)
- Ordinal encoding (e.g., eating habits, alcohol frequency)
- One-hot encoding for transportation
- Feature scaling (critical for KNN)
- Created two datasets:
  - **Lifestyle-only**
  - **Lifestyle + Weight**

**Outputs:**
- `X_features.csv` (lifestyle only)
- `X_features_with_weight.csv` (with weight)
- `y_target.csv`

---

### Notebook 03 — KNN Training (Single Split)
**Purpose:** Sanity check and intuition building.

**Key work:**
- Train/test split evaluation
- Compared Euclidean vs Manhattan distance
- Observed overfitting risk via training accuracy
- Demonstrated why test accuracy alone is misleading

**Outcome:**
- Manhattan distance consistently performed better for lifestyle data.

---

### Notebook 04 — Cross-Validation, Model Selection & Interpretability
**Purpose:** Robust validation and healthcare-appropriate model selection.

**Key work:**
- Stratified 5-fold cross-validation
- Swept K values across a range
- Compared Euclidean vs Manhattan across K
- Stability-aware K selection:
  - Within 1% of best mean accuracy
  - Lowest standard deviation
  - Smaller K preferred for interpretability
- Conducted **ablation study**
- Built **interactive patient input demo**
- Implemented similar-patient explanations

**Outputs:**
- `metrics.json` — full CV results
- `demo_predictions.json` — interactive inference examples

---

## 5. Key Machine Learning Concepts Demonstrated

### Distance Metric Choice
- **Euclidean (L2):** Penalizes large deviations, more sensitive to outliers
- **Manhattan (L1):** Captures additive lifestyle differences more robustly

**Result:**
- Manhattan distance was more stable and interpretable for behavioral similarity.

---

### Feature Scaling (Why It Matters)
KNN is distance-based. Without scaling:
- Weight or height would dominate similarity
- Lifestyle features would be ignored

Scaling ensures:
- All features contribute meaningfully
- Distance reflects *behavioral similarity*, not raw magnitude

---

## 6. Ablation Study: Lifestyle vs Lifestyle + Weight

Two experiments were intentionally compared:

### Phase 1 — Lifestyle-Only Similarity
- Focuses on diet, activity, hydration, habits
- More interpretable
- Better aligned with behavioral health questions

### Phase 2 — Lifestyle + Weight Similarity
- Higher accuracy due to label correlation
- Weight dominates neighbor selection
- Can misclassify muscular or healthy individuals as overweight

**Key Insight:**  
Higher accuracy ≠ better healthcare model.

---

## 7. Similar-Patient Interpretability

For any new input, the model returns:
- Predicted obesity category
- Nearest neighbors
- Neighbor labels and distances
- Vote breakdown

This enables explanations like:
> "Your classification is based on the most similar patients in the dataset, and their majority outcome."

This interpretability is essential for healthcare-adjacent ML systems.

---

## 8. Limitations & Failure Modes (Healthcare Framing)

### Known Limitations
- Cannot distinguish fat mass vs muscle mass
- Obesity labels are proxy-based
- No physiological or clinical measurements
- KNN always predicts, even for unrealistic inputs

### Ethical Considerations
- Predictions are **not medical diagnoses**
- Results should not guide treatment
- Demonstrates risks of over-reliance on proxy features

---

## 9. How to Run the Project (Recruiter-Friendly)

1. Clone the repository
2. Download the dataset from UCI and place it in:
   ```
   data/raw/
   ```
3. Run notebooks in order:
   ```
   01_data_exploration.ipynb
   02_distance_metrics.ipynb
   03_knn_training.ipynb
   04_cross_validation.ipynb
   ```
4. Try the **interactive demo** in Notebook 04:
   - Input lifestyle values
   - Compare predictions **with and without weight**
5. Review saved outputs:
   - `results/metrics.json`
   - `results/demo_predictions.json`

---

## 10. Why This Project Matters

This project demonstrates:
- Correct use of KNN
- Thoughtful validation practices
- Healthcare-aware feature reasoning
- Interpretability over blind accuracy
- Honest discussion of failure modes

It is designed to show **how ML should be built when decisions affect people**, not just metrics.

---

## 11. Disclaimer

This project is for **educational and portfolio purposes only**.  
It is **not a medical diagnostic system** and should not be used for clinical decision-making.

---
