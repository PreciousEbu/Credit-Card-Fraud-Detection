---

# 💳 Credit Card Fraud Detection

## 📌 Overview

This project builds a **production-oriented machine learning system** to detect fraudulent credit card transactions. It focuses not only on model performance, but also on **handling class imbalance, preventing data leakage, optimizing decision thresholds, and ensuring explainability and deployability**.

---

## 🧠 Problem Statement

As far as identity theft goes, credit card fraud is the most prevalent. It's hardly surprising that millions of people become victims each year given that there are an estimated 1.5 billion credit cards in the United States alone. $24.26 Billion was lost in 2018 due to payment card fraud worldwide. 

Financial institutions process millions of transactions daily, making it increasingly difficult to distinguish between legitimate and fraudulent activity in real time. Fraudulent transactions are rare, adaptive, and often designed to mimic normal behavior, creating significant detection challenges.

This introduces a critical trade-off:

* **Missed fraud (false negatives)** → financial loss and risk exposure
* **False alarms (false positives)** → poor user experience and reduced trust
  
---

### Methodology
TThis project frames fraud detection as a **highly imbalanced binary classification problem**, with the goal of maximizing fraud detection (recall) while maintaining acceptable precision. 
Using algorithms like logistic regression, random forests, support vector machines (SVMs), deep neural networks combined with autoencoders, long short-term memory (LSTM) networks, and convolutional neural networks (CNNs), it is possible to classify credit card transactions as genuine or fraudulent. 

Another way is through credit card profiling where it can be determined if someone is using a credit card legitimately or fraudulently
Also, by using techniques for outlier identification to spot transactions that are noticeably different from typical credit card transactions (or "outliers") can help uncover credit card fraud. In this project, the approach used was machine learning algorithms.

#### What are the benefits of using machine learning for credit card fraud detection
- ##### Performance
One major advantage of applying machine learning to the detection of credit card fraud is that ML models outperform traditional fraud detection models by a wide margin. From vast databases, they can recognize thousands of patterns. By studying consumers' app usage, payments, and transaction methods, ML provides insight into how they behave. 

- ##### A quicker detection
A machine learning model is able to swiftly spot any deviations from normal user behavior and transactional patterns. ML algorithms can reduce the risk of fraud and enable more secure transactions by identifying anomalies, such as a sudden spike in transactional amount or geographical change.

- ##### Greater precision
Traditional fraud detection methods result in errors at the payment gateways, which may lead to the blocking of real clients. The accuracy and precision of ML models can be increased with enough training data and insights, which also cuts down on errors and the time needed for manual analysis.

- ##### Increased effectiveness with more data
An algorithm can effectively work with enormous datasets to distinguish between legitimate payments and fraudulent ones after it learns various transactional patterns and behaviors. The models can quickly analyze enormous volumes of data and provide real-time insights for better decision-making.

---

## 🎯 Objectives

* Build a robust fraud detection model
* Handle extreme class imbalance effectively
* Optimize for **ROC-AUC and recall-sensitive metrics**
* Prevent data leakage using pipelines
* Provide **model explainability (SHAP)**
* Deploy the model for real-time inference
* Design an **A/B testing strategy** for validation

---

## ⚙️ Approach

### 1. Data Processing

* Dataset consists of anonymized PCA-transformed features (`V1–V28`)
* Scaled features using **RobustScaler**
* Performed **stratified train-test split** to preserve class distribution

---

### 2. Handling Class Imbalance

* Applied **SMOTEENN** (hybrid over- and under-sampling)
* Integrated into pipeline to avoid data leakage

---

### 3. Modeling

Trained and evaluated:

* Logistic Regression
* Random Forest
* XGBoost

Each model was evaluated using:

* **ROC-AUC (primary metric for model selection)**
* **F1-score (threshold-dependent evaluation)**

---

## 📊 Results

### Model Comparison

| Model               | ROC-AUC    | F1 Score (0.5 Threshold) |
| ------------------- | ---------- | ------------------------ |
| Logistic Regression | **0.9657** | 0.1147                   |
| XGBoost             | 0.9647     | 0.6340                   |
| Random Forest       | 0.9580     | **0.7986**               |

### Key Insight

* **Logistic Regression achieved the highest ROC-AUC**, indicating strong ability to separate fraudulent and non-fraudulent transactions.
* However, **Random Forest significantly outperformed in F1-score**, suggesting better real-world classification performance at the default threshold.

> ⚠️ This highlights a critical nuance:
> **The best model depends on whether you prioritize ranking (ROC-AUC) or classification performance (F1/Recall).**

---

## 🧪 Threshold Optimization

Rather than relying on a fixed threshold (0.5), the final model includes **threshold tuning** to optimize F1-score and balance precision-recall trade-offs.

This step ensures the model aligns with **real-world business constraints**.

---

## 🔍 Explainability (SHAP)

To improve transparency and trust:

* Used **SHAP (SHapley Additive Explanations)**
* Identified features contributing most to fraud predictions
* Enabled both global and local interpretability

---

## 📈 Evaluation Metrics

Due to class imbalance, accuracy was not used.

Primary metrics:

* **ROC-AUC** → model ranking ability
* **Recall** → fraud detection rate
* **Precision** → false positive control
* **F1-score** → balance between precision and recall

---

## 🚀 Deployment

### Model Export

```python
joblib.dump(best_model, "fraud_model.pkl")
```

### FastAPI Inference API

```python
@app.post("/predict")
def predict(data: dict):
    df = pd.DataFrame([data])
    pred = model.predict(df)[0]
    prob = model.predict_proba(df)[0][1]
    return {"prediction": int(pred), "probability": float(prob)}
```

### Run API

```bash
uvicorn app:app --reload
```

---

## 🧪 A/B Testing Strategy

### Goal

Compare performance of the new model against an existing baseline system.

### Design

* 50/50 traffic split (Control vs Treatment)
* User routing based on hashing

### Metrics

* Fraud detection rate (Recall)
* False positive rate
* Revenue impact
* Customer experience (false declines)

---

## 🛠️ Tech Stack

* Python (Pandas, NumPy)
* Scikit-learn
* Imbalanced-learn (SMOTEENN)
* XGBoost
* SHAP
* Matplotlib / Seaborn
* FastAPI

---

## ⚠️ Challenges & Solutions

| Challenge              | Solution                             |
| ---------------------- | ------------------------------------ |
| Severe class imbalance | SMOTEENN + class weighting           |
| Data leakage risk      | Pipeline-based architecture          |
| Metric misalignment    | Used ROC-AUC + F1 + threshold tuning |
| Model interpretability | SHAP explainability                  |

---

## 🔮 Future Improvements

* Hyperparameter tuning with **Optuna**
* Upgrade to **LightGBM** for performance gains
* Implement **real-time streaming (Kafka)**
* Add **model monitoring & drift detection**
* Business-driven threshold optimization

---

## 📎 How to Run

```bash
git clone <repo-url>
cd fraud-detection
pip install -r requirements.txt
python main.py
```

---

## ⭐ Key Takeaway

This project demonstrates how to move beyond basic modeling into **production-aware machine learning**, combining:

* Proper evaluation for imbalanced data
* Data leakage prevention
* Model explainability
* Deployment readiness
* Business-aligned decision making

---

## 📬 Contact

Feel free to reach out for collaboration or discussion.

