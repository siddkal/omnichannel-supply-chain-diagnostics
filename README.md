# omnichannel-supply-chain-diagnostics
An end-to-end data pipelines and operations analysis project optimizing a 300k+ row warehouse and retail sales distribution dataset.
👉 [**View the Live Interactive Tableau Dashboard Here**](https://public.tableau.com/views/End-to-EndSupplyChainOptimizationPipeline/JITVulnerabilitymap?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
# Omni-Channel Supply Chain Diagnostics & Logistics Optimization

An operational optimization project acting as a Data/BI Analyst for a regional multi-channel distributor. This project builds an automated ETL data pipeline to process and analyze a 300,000+ row supply chain ledger tracking B2B Wholesale (`WAREHOUSE SALES`), B2C `RETAIL SALES`, and store replenishment (`RETAIL TRANSFERS`).

---

## 🛠️ Project Architecture & Tech Stack
* **Language:** Python 3.x (Pandas, NumPy)
* **Visualizations:** Tableau Public
* **IE Frameworks:** Pareto Principle (80/20 Rule), Just-In-Time (JIT) Supply Chain Constraints, Reverse Logistics Waste Isolation.

---

## 📋 Key Operations Insights & Engineering Analysis

### 1. High-Velocity Just-In-Time (JIT) Replenishment Risk
* **Insight:** Calculating the ratio of `Retail Transfers` relative to active `Retail Sales` across core product segments (Wine, Beer, Liquor) reveals a tight operational distribution factor of **0.98 to 0.99**. 
* **Operational Impact:** This confirms an aggressive cross-docking or tight JIT replenishment framework. While this minimizes warehouse inventory holding costs, retail storefronts operate without a safety stock buffer, rendering the retail channel exceptionally vulnerable to upstream logistics or carrier delays.

### 2. Supplier Concentration & Systemic Vulnerability
* **Insight:** Applying the Pareto Principle to the wholesale distribution matrix reveals immense supplier network concentration. Three strategic entities (*Crown Imports, Miller Brewing Company, and Anheuser Busch*) command over **65%** of total outgoing warehouse freight volume.
* **Operational Impact:** Strategic procurement diversification is recommended to buffer the distributor's B2B ecosystem from localized labor actions, supply constraints, or factory-level logistics disruptions.

### 3. Data Cleansing & Reverse Logistics Segmentation 
* **Insight:** Isolated significant negative vectors buried inside `WAREHOUSE SALES`—specifically impacting logistical support assets like `DUNNAGE` (protective material) and `REF` (refrigerated storage containers). 
* **Data Fix:** Created an automated Python pipeline to cleanly segment forward-moving commercial revenue from absolute reverse logistics return loops, preventing downstream forecasting distortion.

---

## 📂 Repository Structure
* `data/`: Placeholder directory for raw supply chain CSV inputs.
* `scripts/data_cleaning.py`: Production-grade Python script handling structural schema reinforcement, missing variable imputation, datetime reconstruction, and data integrity checks.
