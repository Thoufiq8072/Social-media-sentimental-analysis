# Project Setup Prerequisites

This document outlines the mandatory setup required before running
any ingestion, transformation, ML, or dashboard workloads.

---

## 1. Unity Catalog Setup

### Catalog

```

%sql
create catalog if not exists sentimental_analysis


```

### Schemas

```

%sql
create schema if not exists sentimental_analysis.raw;
create schema if not exists sentimental_analysis.bronze;
create schema if not exists sentimental_analysis.silver;
create schema if not exists sentimental_analysis.gold;


```

All tables and volumes in this project are created under this catalog.

---

## 2. Volume Structure (Raw Layer)

The following volumes must be created under the `raw` schema:


```

%sql
create volume if not exists sentimental_analysis.raw.social_media_volume;
create volume if not exists sentimental_analysis.raw.ml_source_single;
create volume if not exists sentimental_analysis.raw.ml_output_single;
create volume if not exists sentimental_analysis.raw.ml_source_batch;
create volume if not exists sentimental_analysis.raw.ml_output_batch;


```

### Purpose
| Volume | Description |
|-----|------------|
social_media_volume | Landing zone for raw social media data |
ml_source_batch | Partitioned silver data for ML processing |
ml_source_single | Consolidated silver dataset for ML |
ml_output_batch | ML output batches |
ml_output_single | ML output single file |

---

## 3. Data Flow Expectations

1. Raw source files land in `sentiment_analysis.raw.social_media_volume`
2. Bronze & Silver tables are created in Databricks
3. Silver data is exported to Google Drive via volumes
4. ML processing occurs in Google Colab (GPU-enabled)
5. ML outputs are written back to `sentiment_analysis.raw.ml_output_*` volumes
6. Gold tables are created from ML outputs
7. Dashboards consume only Gold tables

---

## 4. Access & Governance Guidelines

- ML pipelines **read-only** access to Silver volumes
- Gold tables must be written **only** from validated ML outputs
- Dashboards must **never** read from Silver or ML volumes directly

---

## 5. Environment Assumptions

- Databricks Free Edition (Serverless)
- Unity Catalog enabled
- Google Colab used for ML execution
- External storage via Google Drive

---

## 6. Important Notes

- No pipelines should auto-create schemas or volumes
- Setup must be idempotent and manually verified
- Volume naming must remain consistent across teams

Failure to complete this setup will result in pipeline failures.
