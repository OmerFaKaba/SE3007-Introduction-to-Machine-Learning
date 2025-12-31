# 🤖 AI Impact on Jobs  
### Predicting Job Risk, Resilience & Future Career Alternatives

This project analyzes how **Artificial Intelligence (AI) impacts different professions** and presents a **fully reproducible, end-to-end machine learning pipeline**.

Rather than focusing only on job loss, the project answers:

> **Which jobs are at risk, how resilient they are to AI, and which safer alternatives exist.**

---

## 📌 Problem Description

Artificial Intelligence is rapidly transforming the labor market. While some jobs are highly automatable, others remain resilient or evolve alongside AI.

The objectives of this project are:

- Predict the **degree of AI impact** on professions
- Classify jobs into **risk categories**
- Quantify **job resilience** against AI
- Recommend **lower-risk alternative jobs** for high-risk professions

---

## 📂 Dataset Description

The dataset contains job-level information with the following attributes:

- **Job titiles** – Job name  
- **Domain** – Professional field  
- **Tasks** – Number of core tasks  
- **AI models** – Relevant AI tools/models  
- **AI_Workload_Ratio** – Share of tasks automatable by AI  
- **AI Impact** – Ground-truth AI impact percentage  

---

## 🧹 Data Preprocessing

The following preprocessing steps are applied:

- Removal of percentage symbols from `AI Impact`
- Conversion to numeric format
- Handling missing and infinite values
- Feature scaling using **StandardScaler**
- One-hot encoding for categorical variables
- Post-processing of regression outputs using value clipping (`0–100`)

---

## 🧠 Model Details & Methodology

### 1️⃣ AI Impact Prediction (Regression)

**Model:** Random Forest Regressor  
**Goal:** Predict AI impact as a continuous value (0–100%)

**Why Random Forest?**
- Handles non-linear relationships
- Robust to noise and outliers
- Performs well on mixed feature types

**Output:**
- `Predicted_AI_Impact`

---

### 2️⃣ Risk Classification

**Model:** Random Forest Classifier  
**Goal:** Convert predicted AI impact into interpretable risk categories

| AI Impact (%) | Risk Category |
|--------------|--------------|
| 0–50         | Low          |
| 50–70        | Medium       |
| 70–100       | High         |

**Output:**
- `Model_Prediction` → Low / Medium / High

---

### 3️⃣ Hybrid Job Recommendation System

**Goal:** Recommend safer alternatives for high-risk jobs

**Hybrid similarity combines:**

| Component | Method | Weight |
|--------|--------|--------|
| Job title semantics | Sentence-BERT (MiniLM) | 0.45 |
| Domain similarity | One-hot + cosine | 0.35 |
| Workload similarity | Scaled numeric cosine | 0.20 |

Only **Low and Medium risk jobs** are suggested as alternatives.

---

### 4️⃣ Job Resilience Index

A final, interpretable metric is computed:

Job Resilience Score = 100 − Model_AI_Impact


| Score Range | Interpretation |
|-----------|---------------|
| 0–40      | Low Resilience |
| 40–70     | Medium Resilience |
| 70–100   | High Resilience |

This score enables direct comparison between professions.

---



## Install dependencies

`pip install -r requirements.txt`




## 📊 Model Results

### Regression Metrics
The performance of the AI Impact prediction model is evaluated using:

- **MAE (Mean Absolute Error)**
- **RMSE (Root Mean Squared Error)**
- **R² Score (Coefficient of Determination)**

### Classification Metrics
The job risk classification model is evaluated using:

- **Accuracy**
- **Precision**
- **Recall**
- **F1-score**

### Visual Results
The following visual analyses are generated from the test data and included in the repository:

- **Actual vs Predicted AI Impact**
- **Job Resilience Score Distribution**
- **Top-10 Most AI-Resilient Jobs**

All visualizations are generated exclusively from the test set and reflect the true performance of the models.


📁 Output Files

| File                               | Description                |
| ---------------------------------- | -------------------------- |
| `regression_output.csv`            | Predicted AI impact values |
| `final_risk_predictions.csv`       | Job risk categories        |
| `final_hybrid_recommendations.csv` | Safer job alternatives     |
| `job_model_resilience_index.csv`   | Final resilience scores    |


## 🛠 Environment Specification

All required libraries and dependencies for running the project are listed in:
requirements.txt


This ensures that the project can be fully reproduced in a consistent environment.

---

## 📄 Project Presentation

The repository includes a **final presentation PDF** summarizing:

- Problem motivation  
- Methodology  
- Experimental results  

All experiments and results presented in the PDF **exactly correspond to the code and outputs implemented in this repository**, ensuring full reproducibility and transparency.

---

## 🧠 Why This Project Stands Out

- End-to-end AI pipeline covering the full analysis workflow  
- Combines **regression, classification, NLP, and recommender systems**  
- Produces **actionable insights**, not just raw predictions  
- Fully reproducible, well-documented, and evaluation-driven

