# ML Pipeline – Sentiment \& Emotion Analysis

This module handles sentiment and emotion classification on Silver-layer

data using batch-based ML processing executed in Google Colab.

GPU acceleration is used to optimize performance.

---

## 📥 Input Assumptions


This ML pipeline assumes:

- Silver-layer data is already cleaned and deduplicated

- Required volumes are pre-created (see setup prerequisites)

- Data is exported from Databricks to Google Drive before processing

---

## 📊 ML Dataset Preparation Strategies

Two dataset preparation strategies are implemented to support different scales and experimentation needs.

---

### Option 1: Single Parquet Dataset (PoC / Small Scale)


**Flow**

```

Silver Table → Single Parquet → Google Drive → Colab


```

**Characteristics**
- Entire dataset stored in one Parquet file
- Simple and easy to manage
- Suitable for small datasets or quick experiments

**Limitations**
- Limited parallelism
- Potential memory constraints
- Not ideal for large-scale inference

---

### Option 2: Partitioned Parquet Datasets (Preferred / Production-Scale)

**Flow**

```

Silver Table → 100 Parquet Partitions → Google Drive → Colab (Batch ML)


```

**Characteristics**

- Dataset split into fixed-size partitions

- Each batch processed independently

- Optimized for GPU execution


**Advantages**

- Improved scalability

- Better memory utilization

- Faster execution

- Production-style batch ML workflow

---

## ✅ Final Approach Used

The **partitioned Parquet strategy** is used for all final ML runs that feed the Gold layer.


The single-file approach is retained for:

- Prototyping

- Validation

- Debugging

---

## 📤 Output Handling

- ML outputs are written back to Google Drive

- Batch outputs land in `ml_output_batch`

- Consolidated outputs land in `ml_output_single`

- Databricks ingests outputs to create Gold tables

---

## 🧠 Design Rationale

This approach:

- Decouples ML from Databricks compute limits

- Leverages GPU acceleration efficiently

- Mimics real-world ML batch inference pipelines

- Maintains clean data contracts between layers

---

## ⚠️ Important Notes

- ML notebooks do not create schemas or volumes

- ML jobs must be restart-safe and idempotent

- Only Gold tables are exposed to downstream analytics

