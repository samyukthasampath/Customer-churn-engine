# Customer-churn-engine
# Customer Retention Engine — Churn Prediction & Revenue Risk Analysis

**University of Colorado Boulder · Leeds School of Business · Spring 2026 · Group 5**

![PySpark](https://img.shields.io/badge/PySpark-3.x-orange) ![AWS EMR](https://img.shields.io/badge/AWS-EMR-yellow) ![Random Forest](https://img.shields.io/badge/Model-Random%20Forest-green)

## Overview
A scalable churn prediction and financial risk pipeline built with PySpark on AWS EMR.
Using the IBM Telco Customer Churn dataset, the engine predicts which customers are
likely to churn, quantifies revenue at risk, and compares retention campaign strategies
by ROI to support data-driven decision making.

## Key Results
| Metric | Value |
|--------|-------|
| AUC-ROC | 0.8435 |
| Accuracy | 79.78% |
| F1-Score | 78.57% |
| High-risk customers identified | 381 |
| Revenue at risk (high-risk) | $861,967 |
| Targeted campaign ROI | 2,162% vs. 622% (broad) |

## Methodology
- **Model:** Random Forest Classifier (Spark MLlib), tuned via 5-fold
  cross-validation across 8 hyperparameter combinations (trees, depth,
  min instances per node)
- **Features:** 60-dimensional feature vector engineered from 21 raw
  attributes using StringIndexer, OneHotEncoder, and VectorAssembler
- **Business metrics:** Historical CLV, Projected CLV, Revenue at Risk,
  Retention ROI
- **Risk segmentation:**
  - High risk: ≥ 70% churn probability → 381 customers
  - Medium risk: 30–70% → 2,106 customers
  - Low risk: < 30% → 4,556 customers

## Key Churn Drivers
| Feature | Importance |
|---------|------------|
| Tenure | 15.5% |
| Month-to-month contract | 14.0% |
| Total charges | 9.6% |

Month-to-month customers churn at **42.7%** vs. just **2.8%** for two-year contracts.

## Retention Campaign Comparison
| Strategy | Cost | ROI | Net Benefit |
|----------|------|-----|-------------|
| Targeted (381 customers) | $50/customer | 2,162% | $411,933 |
| Broad (7,043 customers) | $50/customer | 622% | $2,190,598 |

Targeted approach delivers **3.5x higher ROI per dollar spent.**

## Deployment
- Deployed on **AWS EMR** (5 executors, 3GB memory each)
- Notebook executed via JupyterHub using sparkmagic
- Scored output saved to **Amazon S3** in Parquet and CSV formats

## Data
- IBM Telco Customer Churn Dataset (7,043 customers, 21 attributes)
- Train/test split: 80% training (5,698 records) / 20% testing (1,345 records)
- Baseline churn rate: 26.54%

## Tech Stack
`Python` `PySpark` `AWS EMR` `Amazon S3` `Spark MLlib` `JupyterHub`
