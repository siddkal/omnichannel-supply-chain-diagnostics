# End-to-End Supply Chain Optimization Pipeline (Interactive Tableau Dashboard)

📊 **[View the Live Interactive Dashboard on Tableau Public](https://public.tableau.com/views/End-to-EndSupplyChainOptimizationPipeline/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)**

---

## 📌 Project Overview
In modern supply chain management, balancing lean inventory operations with resilience is a critical executive challenge. This project delivers a comprehensive, interactive business intelligence solution designed to audit and diagnose operational vulnerabilities across supply chain pipelines. 

By integrating three critical operational perspectives—**Just-In-Time (JIT) volatility, vendor dependency, and logistics distribution flows**—this dashboard equips supply chain managers and directors with the macro-level insights needed to mitigate supplier risks, evaluate inventory holding strategies, and monitor reverse logistics overhead.

---

## 🛠️ Key Analytical Features

### 1. JIT Vulnerability Map (Dual-Axis Timeline Analysis)
* **Objective:** Audit the structural resilience of a Just-In-Time (JIT) operational strategy over a multi-year horizon.
* **Implementation:** Built using a synchronized dual-axis trend analysis plotting `SUM(Retail Sales)` against `SUM(Retail Transfers)` continuously by month. 
* **Business Insights:** The tight visual synchronization of the line paths proves an aggressive, razor-thin inventory strategy. Minor decoupling gaps instantly surface historical windows where stock-outs or over-corrections threatened retail fulfillment continuity.

### 2. Supplier Concentration Risk (Dynamic Ranked Bar Chart)
* **Objective:** Quantify and expose procurement dependencies on top-tier vendors.
* **Implementation:** Designed a horizontally oriented bar chart reflecting total `Net Warehouse Sales` mapped across text dimensions. The chart utilizes custom field sorting parameters to isolate high-volume revenue drivers dynamically.
* **Visual Polish:** Implemented a continuous color gradient mapping sales intensity onto the Marks card, guiding executive attention straight to high-exposure entities (e.g., *Crown Imports*, *Miller Brewing Company*).

### 3. Logistics Flow & Efficiency (Calculated Field Pie Visualization)
* **Objective:** Isolate processing overhead tied to product returns and distribution cycles.
* **Implementation:** Engineered a custom Tableau calculated field (`Volume Handled`) aggregating forward and backward supply streams:
  ```tableau
  [Net Warehouse Sales] + [Returns Volume]
