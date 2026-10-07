# Cloud-Native Fraud Detection with Machine Learning using BigQuery ML (BQML)

An end-to-end Machine Learning pipeline implemented natively inside **Google BigQuery** using SQL. This project addresses the operational challenge of high data egress costs and latency by performing all data preprocessing, class imbalance mitigation, unsupervised anomaly clustering, and supervised gradient boosting directly inside the cloud data warehouse.

---

## Architecture & Workflow

```text
Google Cloud Storage (Raw Archive)
       │
       ▼
BigQuery Table Ingestion (`fraud_dataset.transactions`)
       │
       ▼
SQL Feature Engineering & Controlled Undersampling (10% non-fraud, 100% fraud)
       │
       ├──► Unsupervised Anomaly Profiling (K-Means Clustering)
       │
       └──► Supervised Classification Benchmark:
              ├── Logistic Regression (`LOGISTIC_REG`)
              └── Gradient Boosted Trees (`BOOSTED_TREE_CLASSIFIER`)
                     │
                     ▼
       Model Evaluation (`ML.EVALUATE`) & Test Inference (`ML.PREDICT`)


Key Highlights
In-Warehouse Compute: Zero data movement out of BigQuery to external Python environments.

Class Skew Handling: Addressed severe class imbalance (<0.1% fraud rate) via deterministic sampling and transaction rail isolation (TRANSFER and CASH_OUT).

Feature Engineering: Built domain-specific balance liquidation indicators (origzeroFlag) and balance error metrics (amountError) in SQL.

Champion Model: The Boosted Tree model achieved superior ROC-AUC and F1 scores over baseline Logistic Regression, capturing non-linear interactions between high transaction amounts and sender balance depletion.

Repository Structure
fraud_detection_bigquery_ml.ipynb: The end-to-end documented Colab notebook with SQL queries, narrative, and output interpretations.

Tech Stack
Cloud Platform: Google Cloud Platform (GCP)

Data Warehouse: Google BigQuery

Modeling Engine: BigQuery ML (BQML)

Languages: SQL (GoogleSQL), Python (Google Cloud SDK orchestration)
