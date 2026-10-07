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
