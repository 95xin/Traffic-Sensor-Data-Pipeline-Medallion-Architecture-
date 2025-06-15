# 🚦 Traffic Sensor Data Pipeline (Medallion Architecture)

This project is a PySpark-based data pipeline that I customized and executed to process traffic sensor data using the **Medallion Architecture** (Bronze → Silver → Gold). It transforms raw CSV files into clean, analytical Delta tables and supports downstream visualization in BI tools like Power BI or Looker Studio.

---

## 🔧 Project Structure

The pipeline follows the industry-standard **three-layer structure**:

### 1️⃣ Bronze Layer - Raw Data Ingestion
- **Script**: `build_bronze.py`
- **Input**: Raw traffic CSV files
- **Output Table**: `raw_traffic_<date>`
- **Purpose**: Load raw data as-is into Delta format for durability and traceability

### 2️⃣ Silver Layer - Data Cleaning & Modeling
- **Script**: `build_silver.py`
- **Output Tables**:
  - `traffic_silver_fact`
  - `dim_region`
  - `dim_site`
  - `dim_time`
  - `dim_detector`
- **Purpose**: Normalize, clean, and enrich data to build a star schema model

### 3️⃣ Gold Layer - Aggregation & Business Insights
- **Script**: `build_gold.py`
- **Output Tables**:
  - `traffic_gold_region_hourly`
  - `traffic_gold_detector_hourly`
  - `traffic_gold_region_monthly`
  - `traffic_gold_congestion_flags`
- **Purpose**: Aggregate data for performance reporting, dashboards, and business KPIs

---

## ✅ Testing

To ensure data quality and schema integrity, tests are included at each layer:

| Layer  | Script                  | What it tests                        |
|--------|-------------------------|--------------------------------------|
| Bronze | `build_bronze_test.py`  | Raw data load success and row counts |
| Silver | `build_silver_test.py`  | Dimension/Fact schema correctness    |
| Gold   | `build_gold_test.py`    | Aggregation validity and table checks|

---

## 📊 Sample Insights from Gold Layer

Here are some meaningful insights generated after building the full pipeline:

- **Hourly traffic peaks** around 16:00–17:00 in congested regions (e.g., `GE2`, `GR2`)
- **Detector-level breakdown** helps identify high-volume lanes and potential bottlenecks
- **Monthly trends** reveal seasonality and long-term traffic growth
- **Congestion flags** highlight critical intervals and locations prone to traffic jams

These insights were visualized using Power BI connected directly to Delta Lake.

---

## 📁 Folder Layout

```bash
traffic_pipeline/
├── build_bronze.py
├── build_silver.py
├── build_gold.py
├── build_bronze_test.py
├── build_silver_test.py
├── build_gold_test.py
├── /data/       # Raw input files
└── README.md    # This document
