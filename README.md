# 💳 Credit Card Fraud Detection

![Credit Card Fraud Detection](https://img.shields.io/badge/💳-Credit%20Card%20Fraud%20Detection-E64626?style=for-the-badge&labelColor=2C91B8)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Machine%20Learning-F7931E?logo=scikitlearn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-Model%20Training-189CAB)
![SHAP](https://img.shields.io/badge/SHAP-Explainability-8A2BE2)
![FastAPI](https://img.shields.io/badge/FastAPI-API%20Development-009688?logo=fastapi&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📌 Overview

This project develops a **machine learning system for credit card fraud detection**, focusing on class imbalance, data leakage prevention, decision-threshold optimization, model explainability, and deployment readiness.

Using anonymized transaction data, the project evaluates machine learning models to distinguish fraudulent from legitimate transactions. The final evaluation emphasizes not only ranking performance but also the operational trade-off between detecting fraud and minimizing false alarms.

The final model achieved a **ROC-AUC of 0.9490 and Average Precision of 0.8184**, with 93.97% precision and 73.65% recall at the selected classification threshold.

---

## 🧠 Problem Statement

As far as identity theft goes, credit card fraud is a significant financial challenge. Financial institutions process millions of transactions daily, making it increasingly difficult to distinguish legitimate activity from fraudulent transactions in real time. Fraudulent transactions are rare and can closely resemble normal customer behavior, creating significant detection challenges.

This introduces a critical trade-off:

* **Missed fraud (false negatives)** → potential financial losses and risk exposure.
* **False alarms (false positives)** → unnecessary transaction reviews, customer friction, and reduced trust.

Because fraudulent transactions represent only a small proportion of transactions, a model can achieve high overall accuracy while still missing a substantial proportion of fraud. This project therefore emphasizes precision, recall, F1-score, ROC-AUC, and Average Precision rather than accuracy alone.

---

### Methodology

This project frames fraud detection as a **highly imbalanced binary classification problem**, aiming to identify fraudulent transactions while controlling false positives.

Machine learning approaches can learn patterns in historical transaction data and assign fraud probabilities to new transactions. These predictions can support fraud screening and investigation, although their effectiveness depends on data quality, model performance, and the classification threshold.

#### What are the benefits of using machine learning for credit card fraud detection?

- **Pattern recognition:** Models can identify complex relationships in transaction features that may be difficult to capture with simple rules.
- **Faster screening:** Automated predictions can help prioritize suspicious transactions for further review.
- **Controlled false alarms:** Precision-recall analysis and threshold optimization help balance fraud detection against unnecessary alerts.
- **Scalability:** Trained models can process large volumes of transaction records, subject to the infrastructure and latency requirements of the deployment environment.

---

## 🎯 Objectives

* Build a robust fraud detection model.
* Address severe class imbalance.
* Evaluate model discrimination and fraud detection performance using ROC-AUC, Average Precision, precision, recall, and F1-score.
* Prevent data leakage through appropriate preprocessing and modelling workflows.
* Provide model explainability using SHAP.
* Prepare a model for API-based inference.
* Develop an A/B testing strategy for future controlled evaluation.

---

## ⚙️ Approach

### 1. Data Processing

* Used anonymized credit card transaction data containing **284,807 transactions and 31 columns**.
* Worked with PCA-transformed features (`V1–V28`), transaction time (`Time`), transaction amount (`Amount`), and the target variable (`Class`).
* Explored class distribution and transaction amounts through visualizations.
* Used stratified data splitting to preserve the rare fraud class across evaluation subsets.
* Applied preprocessing within the modelling workflow to reduce the risk of data leakage.

### 2. Handling Class Imbalance

Credit card fraud represented approximately **0.173% of the original dataset**, making class imbalance a central modelling challenge.

The modelling workflow considered class imbalance when training and evaluating classifiers. Model selection and threshold tuning were separated from final test evaluation to prevent the test set from influencing these decisions.

### 3. Modeling

Evaluated the following machine learning algorithms:

* Logistic Regression
* Random Forest
* XGBoost

Models were assessed using metrics suited to imbalanced binary classification, including:

* **ROC-AUC:** ability to rank fraudulent transactions above legitimate ones.
* **Average Precision:** precision-recall performance across different thresholds.
* **Precision, recall, and F1-score:** classification performance at the selected threshold.

The final results below reflect the selected model's performance on the held-out test set.

---

## 📊 Results

### Model Comparison

The models were evaluated on the validation set using ROC-AUC and Average Precision to compare their ability to distinguish fraudulent transactions and identify fraud under severe class imbalance.

| Model | ROC-AUC | Average Precision |
|---|---:|---:|
| Random Forest | 0.9684 | **0.8884** |
| XGBoost | 0.9855 | 0.8780 |
| Logistic Regression | **0.9943** | 0.7620 |

**Selected model: Random Forest**

Although Logistic Regression achieved the highest validation ROC-AUC (0.9943), Random Forest achieved the highest Average Precision (0.8884). Random Forest was selected based on its stronger precision-recall performance, which is particularly relevant for fraud detection under severe class imbalance.

The selected Random Forest model was subsequently evaluated on a separate, held-out test set. The results below represent its final test performance and provide an estimate of how well it generalizes to unseen transactions.

### Final Test Performance

| Metric | Score |
|---|---:|
| ROC-AUC | **0.9490** |
| Average Precision | **0.8184** |
| Precision | **0.9397** |
| Recall | **0.7365** |
| F1-score | **0.8258** |

The results demonstrate strong ranking performance and high precision on the held-out test data. At the selected classification threshold, the model identified approximately 74% of fraudulent transactions while maintaining precision of approximately 94%.

### Classification Report

| Class | Precision | Recall | F1-score | Support |
|---|---:|---:|---:|---:|
| Non-Fraud | 1.00 | 1.00 | 1.00 | 85,295 |
| Fraud | 0.94 | 0.74 | 0.83 | 148 |
| Macro Average | 0.97 | 0.87 | 0.91 | 85,443 |
| Weighted Average | 1.00 | 1.00 | 1.00 | 85,443 |

*Note: Non-fraud metrics and overall accuracy are rounded. The rounded values should not be interpreted as evidence of perfect classification.*

### Test-Set Transaction Outcomes

| Outcome | Transactions |
|---|---:|
| Fraud detected (true positives) | **109** |
| Fraud missed (false negatives) | **39** |
| Legitimate transactions flagged (false positives) | **7** |
| Legitimate transactions correctly cleared (true negatives) | **85,288** |
| Total test transactions | **85,443** |

### Key Insights

* **Strong discrimination:** ROC-AUC of 0.9490 indicates that the model distinguishes between fraudulent and legitimate transactions effectively across classification thresholds.
* **High precision:** Of the transactions flagged as fraudulent, approximately 94% were genuinely fraudulent in the test set.
* **Meaningful fraud detection:** The model detected 109 of the 148 fraudulent transactions in the test set.
* **Low false-positive count:** Only 7 legitimate transactions were incorrectly flagged, limiting unnecessary alerts in this evaluation.
* **Remaining detection gap:** The model missed 39 fraudulent transactions, highlighting the need to balance precision with fraud detection coverage.

---

## 🧪 Threshold Optimization

A fixed probability threshold of 0.5 is not always appropriate for imbalanced fraud detection. The classification threshold affects the balance between precision and recall.

The project uses threshold optimization to select a decision threshold based on validation performance rather than relying solely on the default threshold. The final test metrics are then used to evaluate the selected model and threshold on unseen data.

The reported F1-score of **0.8258** reflects the balance between precision and recall at the selected threshold.

In a production financial environment, the threshold should also account for the relative costs of missed fraud, false alerts, manual reviews, and customer friction.

---

## 🔍 Explainability (SHAP)

To improve model transparency:

* Used SHAP (SHapley Additive Explanations) to investigate feature contributions to model predictions.
* Examined feature importance to understand which input variables influence predictions.
* Used explainability analysis to support model inspection and communicate model behavior.

**Interpretation note:** The `V1–V28` variables are anonymized PCA-transformed features. Their contributions can be assessed statistically, but they cannot be directly interpreted as specific customer or transaction attributes without additional information about the original features.

---

## 📈 Evaluation Metrics

Due to severe class imbalance, accuracy alone is insufficient for assessing fraud detection performance.

The project uses the following metrics:

* **ROC-AUC:** measures ranking discrimination across thresholds.
* **Average Precision:** summarizes precision-recall performance, particularly useful when the positive class is rare.
* **Precision:** measures the proportion of flagged transactions that are fraudulent.
* **Recall:** measures the proportion of actual fraud cases detected.
* **F1-score:** balances precision and recall at a particular threshold.
* **Confusion matrix:** quantifies detected fraud, missed fraud, false alarms, and correctly cleared legitimate transactions.

The held-out test set contained 148 fraudulent transactions among 85,443 transactions, giving a fraud prevalence of approximately **0.173%**.

---

## 💼 Business Impact

The test-set results illustrate how a fraud detection model can support transaction screening while controlling false alarms.

* **109 fraudulent transactions detected:** the model identified approximately 73.65% of the fraud cases in the test set.
* **39 fraudulent transactions missed:** these cases represent potential exposure that a production workflow would need to address through further model improvements, complementary rules, or additional review.
* **Only 7 legitimate transactions flagged:** the low false-positive count suggests limited unnecessary intervention at the selected threshold on this test set.
* **94% precision:** flagged transactions were highly concentrated among actual fraud cases, potentially helping investigation teams prioritize alerts.

These are test-set findings, not verified financial savings. Actual monetary impact would depend on transaction values, recoverability, investigation costs, fraud losses prevented, and the consequences of incorrectly flagging legitimate transactions.

---

## 🚀 Deployment

### Model Export

The selected fitted model can be serialized for reuse with `joblib`:

```python
import joblib

joblib.dump(best_model, "fraud_model.pkl")
```

The deployed artifact should include the fitted preprocessing steps, model, selected decision threshold, and expected input feature schema where applicable.

### FastAPI Inference API

A FastAPI endpoint can expose the model for prediction. A production implementation should validate incoming fields, enforce the expected feature schema, and return both the predicted class and fraud probability.

Illustrative endpoint structure:

```python
@app.post("/predict")
def predict(data: dict):
    df = pd.DataFrame([data])
    probability = model.predict_proba(df)[0][1]
    prediction = int(probability >= threshold)

    return {
        "prediction": prediction,
        "probability": float(probability)
    }
```

Here, `model` represents the loaded fitted model and `threshold` is the decision threshold selected during validation. Input validation and error handling should be added before production use.

### Run API

```bash
uvicorn app:app --reload
```

*The command starts the development server; production deployment requires appropriate server configuration, monitoring, security, and operational testing.*

---

## 🧪 A/B Testing Strategy

### Goal

Evaluate whether the fraud detection model improves performance compared with an existing baseline system.

### Proposed Design

* Compare the current baseline with the candidate model in a controlled evaluation.
* Begin with offline evaluation or shadow-mode predictions before allowing model outputs to affect live transaction decisions.
* If live testing is approved, define a safe routing strategy and risk controls before allocating traffic.

### Metrics

* Fraud detection rate (recall).
* Precision and false-positive rate.
* Fraud losses and recoveries.
* Manual investigation workload.
* Customer experience, including unnecessary declines or review delays.
* Prediction latency and system reliability.

A 50/50 split should not be applied automatically to live financial transactions. The experiment design must account for financial risk, operational constraints, and customer protection.

---

## 🛠️ Tech Stack

* **Python:** data processing and modelling.
* **Pandas and NumPy:** data manipulation and numerical analysis.
* **Scikit-learn:** preprocessing, classification, and evaluation.
* **Imbalanced-learn:** tools for imbalanced classification experiments, where applicable.
* **XGBoost:** gradient-boosted tree modelling.
* **SHAP:** model explainability.
* **Matplotlib and Seaborn:** exploratory data analysis and visualization.
* **FastAPI:** API-based inference.
* **Joblib:** model serialization.

---

## ⚠️ Challenges & Solutions

| Challenge | Approach |
|---|---|
| Severe class imbalance | Used imbalance-aware modelling and precision-recall evaluation. |
| Data leakage risk | Kept model selection and threshold tuning separate from final test evaluation. |
| Misleading accuracy | Prioritized ROC-AUC, Average Precision, precision, recall, F1-score, and confusion-matrix counts. |
| Precision-recall trade-off | Selected a decision threshold using validation performance. |
| Model interpretability | Used SHAP to investigate feature contributions. |
| Deployment readiness | Structured the project around model serialization and API-based inference. |

---

## 🔮 Future Improvements

* Conduct further hyperparameter tuning and compare candidate models using validation data.
* Evaluate business-cost-sensitive threshold selection.
* Assess model performance across transaction amounts and other available segments.
* Implement model monitoring, data-quality checks, and drift detection.
* Explore real-time streaming infrastructure such as Kafka if required by deployment needs.
* Evaluate complementary fraud rules or human-review workflows for missed fraud.
* Conduct controlled shadow-mode and production testing before relying on predictions for live transaction decisions.

---

## 📎 How to Run

```bash
git clone <repo-url>
cd fraud-detection
pip install -r requirements.txt
```

Run the notebook or project entry point appropriate to your repository structure. If `main.py` is configured as the executable entry point:

```bash
python main.py
```

To start the API in development mode, if `app.py` contains the FastAPI application:

```bash
uvicorn app:app --reload
```

---

## 📬 Contact

Feel free to reach out for collaboration or discussion.
