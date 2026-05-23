# 📦 Omni-Channel Supply Chain Diagnostics & Logistics Pipeline

👉 [**View the Live Interactive Tableau Dashboard Here**](https://public.tableau.com/views/End-to-EndSupplyChainOptimizationPipeline/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

## 📌 Project Overview
This project delivers an end-to-end data engineering and business intelligence solution designed to audit and optimize warehousing and multi-channel fulfillment operations. Using a dataset of **307,000+ operational records**, the pipeline ingests raw multi-channel ledger entries, performs schema standardization, executes programmatic data cleansing, and isolates critical operational metrics to flag supply chain vulnerabilities.

The downstream analysis surfaces systematic bottlenecks, structural dependencies, and operational inefficiencies, translating raw transactional data into high-impact boardroom insights.

---

## 📈 Strategic Business Insights

### 1. Just-In-Time (JIT) Supply Chain Vulnerability
* **Metric Discovered:** $\text{Replenishment Factor} = \frac{\sum \text{Retail Transfers}}{\sum \text{Retail Sales}} = 0.9875$
* **Operational Risk:** Retail storefronts carry a razor-thin safety inventory margin of less than $1.3\%$. Retail transfers (replenishment) tightly trace active consumer demand with zero buffer room. A transit or fulfillment delay exceeding 48 hours results in immediate store-wide stockouts.

### 2. Supplier Concentration Risk (The 80/20 Bottleneck)
* **Metric Discovered:** Three primary distribution networks dominate the entire logistical footprint.
* **Top 3 Volumetric Footprints:**
  1. **Crown Imports:** $1,651,871.51$ units
  2. **Miller Brewing Company:** $1,425,448.21$ units
  3. **Anheuser Busch Inc:** $1,399,261.25$ units
* **Operational Risk:** High systemic exposure. Any labor strikes, material shortages, or freight challenges within these three specific supplier networks could halt more than half of the company's total product throughput.

### 3. Reverse Logistics & Waste Volume Segmentation
* **Metric Discovered:** Isolated reverse logistics loops from forward distribution channels.
  * **Forward Logistics (Active Sales):** $7,925,508.87$ units ($98.2\%$)
  * **Reverse Logistics (Returns / Waste Material):** $143,752.59$ units ($1.8\%$)
* **Operational Insight:** While $1.8\%$ seems small, it represents over $143,000$ physical items moving backward through the warehouse network annually, directly consuming labor, storage capacity, and freight costs without generating forward revenue.

---

## 🛠️ Data Pipeline Architecture (ETL)

The core data pipeline was engineered using **Python, Pandas, and NumPy** to automate data cleansing and state reconstruction. The pipeline processes data through six distinct phases:

1. **Ingestion & Parsing:** Dynamically loads multi-channel ledgers from a local environment.
2. **Schema Standardization:** Strips whitespace and forces a strict uppercase layout across all transactional columns to eliminate duplicate categories caused by manual entry.
3. **Null-Value Rectification:** Implements robust fallbacks (`UNKNOWN SUPPLIER`, `UNKNOWN TYPE`) and zeroes out missing numeric metrics to preserve ledger structural integrity.
4. **Feature Engineering (Reverse Logistics Isolation):** Employs mathematical conditions to isolate reverse freight metrics:
   * Categorizes transactions into `FORWARD_LOGISTICS` or `REVERSE_LOGISTICS`.
   * Maps negative warehouse volumes directly into a absolute-value metric (`RETURNS_VOLUME`).
5. **Temporal Reconstruction:** Builds a synchronized, clean `DATE` timestamp metric by joining independent `YEAR` and `MONTH` values to allow continuous line-chart mapping over time.
6. **Deduplication & Target Export:** Drops duplicate records to prevent skewed distributions and exports the clean file as `processed_supply_chain_data.csv`.

### Core Pipeline Snippet
```python
import pandas as pd
import numpy as np

# Feature Engineering: Isolating Reverse Logistics
df['TRANSACTION_TYPE'] = np.where(df['WAREHOUSE SALES'] >= 0, 'FORWARD_LOGISTICS', 'REVERSE_LOGISTICS')
df['RETURNS_VOLUME'] = np.where(df['WAREHOUSE SALES'] < 0, abs(df['WAREHOUSE SALES']), 0.0)
df['NET_WAREHOUSE_SALES'] = np.where(df['WAREHOUSE SALES'] > 0, df['WAREHOUSE SALES'], 0.0)

# Temporal Reconstruction
df['DATE'] = pd.to_datetime(df['YEAR'].astype(str) + '-' + df['MONTH'].astype(str) + '-01')
