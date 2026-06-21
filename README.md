# 🚀 End-to-End Product Analytics Data Pipeline (Meta-Style)

## 📌 Project Overview
This project simulates the daily workflow of a **Data Engineer (Product Analytics)**. It features an end-to-end data pipeline that ingests simulated social media event logs, processes them into a scalable star-schema data warehouse, enforces data quality SLAs through statistical anomaly detection, and serves a product analytics dashboard to evaluate an A/B feature rollout.

**Tech Stack:** Python, SQLite, Pandas, Streamlit, JSONL

## 🏗️ Architecture & Pipeline Phases

### 1. Data Generation (Simulated Datalake)
*   **Script:** `generate_logs.py`
*   **Action:** Generates 15,000+ synthetic JSONL event logs mimicking social app interactions (views, likes, shares) and assigns 30% of users to an experimental "New Feature" group.

### 2. ETL Process (Extract, Transform, Load)
*   **Script:** `etl_pipeline.py`
*   **Action:** Ingests raw JSONL logs, standardizes ISO-8601 UTC timestamps into SQL `DATETIME` formats, handles boolean casting, and performs highly efficient bulk inserts (`executemany`) into a relational database.

### 3. Data Modeling (Star Schema)
*   **Script:** `data_models.py`
*   **Action:** Transforms raw data into a query-optimized Star Schema. Separates dimension tables (Users, Devices) from the central Fact table. Aggregates data into a daily summary table using advanced SQL (`CASE WHEN`, `COUNT DISTINCT`) to rapidly serve product metrics.

### 4. Data Quality & SLA Monitoring
*   **Script:** `sla_monitor.py`
*   **Action:** Protects pipeline integrity by automatically calculating rolling statistical variances. Triggers alerts if Daily Active Users (DAU) or Session Durations experience a >15% volume drop, ensuring proactive SLA management before data reaches product managers.

### 5. Product Storytelling (Visualization)
*   **Script:** `dashboard.py`
*   **Action:** A Streamlit web application that connects directly to the analytical summary tables. It visualizes the A/B test rollout, comparing retention and engagement metrics between the Test and Control groups to drive product decisions.

## ⚙️ How to Run Locally

1. Clone the repository:
```bash
   git clone [https://github.com/yourusername/meta-product-analytics-pipeline.git](https://github.com/yourusername/meta-product-analytics-pipeline.git)
   cd meta-product-analytics-pipeline
Install dependencies:

Bash
   pip install pandas streamlit faker
Execute the pipeline in order:

Bash
   python generate_logs.py
   python etl_pipeline.py
   python data_models.py
   python sla_monitor.py
Launch the Product Dashboard:

Bash
   streamlit run dashboard.py
🎯 Business Value
This project demonstrates the ability to not only move data but to model data for product impact. By decoupling the raw ingestion from the analytical tables, and layering automated SLA checks on top, this architecture ensures that Data Scientists and Product Managers are making decisions on highly reliable, highly available data.
