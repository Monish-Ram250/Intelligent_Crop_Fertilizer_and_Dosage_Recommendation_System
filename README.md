# Intelligent Crop Fertilizer and Dosage Recommendation System

## Project Overview

A multi-output machine learning pipeline that simultaneously recommends a suitable **crop** (37 classes), **fertilizer** (8 types), and **dosage** (in kg/hectare) from a single set of soil and climate inputs. The system merges datasets from Kaggle and government agricultural repositories and is optimized using RandomizedSearchCV with cross-validation.

---

## Dataset

**Sources:** Kaggle + Government agricultural repositories (merged)  
**Features:** 14 soil and climate parameters  
**Targets:** 3 simultaneous outputs — crop class, fertilizer type, dosage

### Input Features

| Category | Features |
|---|---|
| Soil Nutrients | N, P, K, OC, S, Zn, Fe, Cu, Mn, B |
| Soil Properties | pH |
| Climate | Temperature, Humidity, Rainfall |

### Output Targets

| Output | Type | Classes |
|---|---|---|
| Crop | Multi-class Classification | **37 crop types** |
| Fertilizer | Multi-class Classification | 8 fertilizer types |
| Dosage | Regression | kg/hectare (continuous) |

---

## Model Architecture

Three separate XGBoost models trained in sequence:

```
Soil + Climate Inputs
    → XGBoost Classifier  →  Crop Recommendation (37 classes)
    → XGBoost Classifier  →  Fertilizer Recommendation (8 types)
    → XGBoost Regressor   →  Dosage per Hectare (kg)
                          →  Total Dosage = Dosage/ha × Land Area
```

All three models tuned with **RandomizedSearchCV** (10-fold CV, 20–25 candidates).

---

## Results

### Crop Classifier — 37 Classes

| Metric | Score |
|---|---|
| **Accuracy** | **70.57%** |
| Macro Precision | 0.71 |
| Macro Recall | 0.68 |
| **Macro F1** | **0.69** |
| Weighted F1 | 0.71 |

Notable class-level performance:

| Crop | Precision | Recall | F1 |
|---|---|---|---|
| Kidney Beans | 0.98 | 0.79 | 0.87 |
| Apple | 0.90 | 0.85 | 0.87 |
| Papaya | 0.89 | 0.81 | 0.85 |
| Potato | 0.81 | 0.90 | 0.85 |
| Ragi | 0.87 | 0.82 | 0.85 |
| Rice | 0.52 | 0.58 | 0.55 (hardest) |
| Tur | 0.52 | 0.46 | 0.49 (hardest) |

> 70.57% accuracy across 37 crop classes with heavily overlapping soil profiles is a meaningful result — many crops share similar nutrient requirements, making the classification boundary inherently ambiguous.

### Fertilizer Classifier — 8 Types

| Metric | Score |
|---|---|
| **Accuracy** | **85.26%** |
| Macro Precision | 0.86 |
| Macro Recall | 0.71 |
| **Macro F1** | **0.77** |
| Weighted F1 | 0.84 |

Notable class-level performance:

| Fertilizer | Precision | Recall | F1 |
|---|---|---|---|
| Compound NPK / Urea | 1.00 | 0.88 | 0.94 |
| Urea | 0.86 | 0.94 | 0.90 |
| Urea/Ammonium Sources | 0.95 | 0.72 | 0.82 |
| FYM/Compost | 0.71 | 0.42 | 0.53 (hardest) |

### Dosage Regressor

| Metric | Score |
|---|---|
| MAE | 104.43 kg/ha |
| RMSE | 203.51 kg/ha |
| **R² Score** | **0.719** |

> R² of 0.719 indicates the model explains ~72% of dosage variance from soil and climate inputs alone.

---

## Pipeline

```
Multi-source Datasets (Kaggle + Government)
    → Merge & Deduplicate
    → Handle Missing Values (median imputation)
    → Encode Labels (LabelEncoder)
    → Train-Test Split (80:20)
    → RandomizedSearchCV (10-fold CV)
    → XGBoost Crop Classifier     → Accuracy: 70.57%
    → XGBoost Fertilizer Classifier → Accuracy: 85.26%
    → XGBoost Dosage Regressor    → R²: 0.719
    → User Input Prediction
    → Visualizations
```

---

## Visualizations

The notebook includes four custom visualizations:

**1. Nutrient & Climate Radar Chart** — compares user's soil/climate values against the dataset median across all 14 features simultaneously.

**2. N-P-K Dosage Pie Chart** — breaks down the total recommended dosage into Nitrogen, Phosphorus (P₂O₅), and Potassium (K₂O) proportions.

**3. Top-3 Crop Probability Bar Chart** — shows the model's confidence scores for the top 3 predicted crops, giving farmers alternatives if the top suggestion isn't feasible.

**4. Nutrient Deficiency Map** — color-coded bar chart (green/yellow/red) showing which soil nutrients are optimal, slightly deficient, or critically low relative to dataset thresholds.

---

## Sample Output

For a given set of soil and climate values, the system outputs:

- Recommended crop (with top-3 probability breakdown)
- Recommended fertilizer type
- Dosage per hectare (kg/ha)
- Total dosage based on entered land area (kg)
- All four visualizations

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python | Core language |
| Pandas, NumPy | Data merging and preprocessing |
| Scikit-learn | Encoding, splitting, RandomizedSearchCV |
| XGBoost | All three prediction models |
| Matplotlib, Seaborn | Visualizations |
| Jupyter Notebook | Development environment |

---

## Limitations

- Based on static historical data — no real-time weather API integration
- May carry regional bias from source datasets
- Should be used as a decision-support tool, not a replacement for agronomist advice

---

## Author

**Akula Monish Ram**  
B.Tech CSE — Lovely Professional University  
Minor in AI — IIT Ropar
