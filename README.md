# 📊 Social Media Sentiment Analysis Platform  
**End-to-End Data Engineering & ML Pipeline**

---

## 🔍 Overview

This project implements an **end-to-end sentiment analytics platform** for social media data using **Apache Spark, NLP, and ML models**, following an **industry-grade medallion architecture**.

The pipeline ingests raw data, performs scalable transformations, applies **sentiment and emotion analysis**, and exposes **business-ready insights** through interactive dashboards.

---

## 🏗️ Architecture

![Architecture Diagram](Architecture\architecture_diagram.png)

**High-level flow:**

```

Raw → Bronze → Silver → ML → Gold → Dashboard


```

---

## 🧱 Medallion Architecture

### 🥉 Bronze Layer – Raw Ingestion
- Stores raw social media data
- Enforced schema, no transformations
- Mirrors source structure

**Purpose:** Traceability & replayability

---

### 🥈 Silver Layer – Cleaned & Enriched
- Deduplication
- Language filtering (English)
- Timestamp normalization
- Text cleaning
- Feature engineering:
  - Word count
  - Hashtag / mention flags

**Purpose:** Analytics & ML-ready dataset

---

### 🤖 ML Processing Layer

ML inference is **decoupled from Spark ETL**, following industry best practices.

#### Sentiment Analysis
- Spark NLP
- Scalable batch inference

#### Emotion Classification
- HuggingFace Transformers
- GPU-accelerated (T4)
- Batched inference for efficiency

**Outputs:**
- `sentiment_label`
- `emotion_label`

---

### 🥇 Gold Layer – Analytics

Business-ready aggregated tables:
- Monthy Tweet Counts
- Daily sentiment trends
- Daily emotion trends
- Overall sentiment distribution
- Overall emotion distribution
- Net sentiment score
- Trending Hashtags

Optimized for dashboard performance.

---

## 📊 Dashboard (Databricks SQL)

**Key Insights:**
- Daily sentiment trend (positive vs negative)
- Emotion distribution
- Net sentiment KPI
- Overall sentiment & emotion share

**Design Principles:**
- KPIs separated from trends
- Time-series optimized aggregations
- Business-readable visuals

---

## ⚙️ Tech Stack

|     Category    |       Technology         |
|-----------------|--------------------------|
|    Processing   |       Apache Spark       |
|     Storage     |   Parquet / Delta Lake   |
|    Sentiment    |        Spark NLP         |
|     Emotion     | HuggingFace Transformers |
| ML Acceleration |       NVIDIA T4 GPU      |
|    Analytics    |      Databricks SQL      |
|  Visualization  |   Databricks Dashboards  |

---

## 🚀 Performance Highlights

- GPU inference reduced batch runtime from **minutes to seconds**
- Batched ML inference maximized GPU utilization
- Optimized Gold tables for fast dashboard queries

---

## 🧠 Key Design Decisions

- Medallion architecture for data quality
- Batch ML inference instead of row-level Spark UDFs
- Spark for ETL, Transformers for ML
- Materialized Gold tables for analytics

---

## 📁 Repository Structure

```
.
├── Notebooks/
│       └── Bronze
│    	       └─ bronze_notebook
│       └── Silver
│   	       └─ silver_notebook
│       └── Machine Learning
│   	       └─ ml_flow_notebook
│   	       └─ mlflow_dataset_preparation_notebook
│   	       └─ README.md
│       └── Gold
│   	       └─ gold_notebook
│   	       └─ gold_views_notebook
│
├── Source_Data/
│       └── README.md
│
├── Docs/
│       └── setup_prerequisites.md
│
├── Data_sample/
│       └── source_sample.csv
│       └── bronze_sample.csv
│       └── silver_sample.csv
│       └── gold_sample.csv
│       └── gold_ml_core_sample.csv
│
├── Dashboard/
│       └── Sentiment_Analysis_Dashboard.Ivdash
│       └── README.md
│
├── Visualization/
│       └── Count_of_records_by_month.png
│       └── Daily_Net_Sentiment.png
│       └── Daily_Sentiment_Trend.png
│       └── Overall_Sentiment_Distribution.png
│       └── Weekly_Emotion_Trend.png
│       └── Overall_Emotion_Distribution.png
│       └── Trending_Hashtags.png
│
├── Architecture/
│       └── architecture_diagram.md
│       └── architecture_diagram.png
│
└── README.md
```

---

## Prerequisites

Before running the pipelines, ensure that the required Unity Catalog,
schemas, and volumes are created.

📄 Refer to: `Docs/setup_prerequisites.md`

---

## 🏁 Conclusion

This project demonstrates:
- Strong **data engineering fundamentals**
- Practical **ML integration at scale**
- Clean **analytics & visualization design**
- Production-style thinking

