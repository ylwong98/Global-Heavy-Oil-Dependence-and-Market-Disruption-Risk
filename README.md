# **Shifting Crude Oil Quality & Refining Constraints: A Data‑Driven Analysis of Global Heavy-Oil Dependence and Market Disruption Risk**
### **Professional Graduate Industry Capstone - Chirality Research x University of Calgary**
**Team:**  
- [Yu Ling (Elaine) Wong](https://www.linkedin.com/in/yu-ling-wong/)  
- [Michael Morgan](https://www.linkedin.com/in/michael-morgan-calgary/)  
- [Andrew Gellner](https://www.linkedin.com/in/andrew-gellner-data-analytics/)  
---

## **📌 Project Overview**
Heavy crude oil is essential for producing marine fuels, bunker oil, and heavy distillates. Canada is a major heavy‑oil producer, but faces constraints related to refining configuration, transportation capacity, and shifting global supply dynamics.

This project delivers:

- A **Heavy‑Oil Market Disruption Risk Index**  
- **Production & consumption forecasts** to 2030  
- **Scenario modeling** for geopolitical & localized disruptions  
- A **Power BI dashboard** for interactive exploration  
- Strategic insights for Canada’s heavy‑oil export opportunities  

---

## **📘 Executive Summary**
Heavy crude oil supply is increasingly constrained, while many countries remain structurally dependent on heavy crude for marine fuel production and refining operations. Canada produces the majority of heavy crude in a market trending toward lighter grades, creating both risk and opportunity.

To quantify these dynamics, we:

- Estimated heavy‑oil production for **18 major producing countries (1975–2026)**  
- Modeled heavy‑oil consumption using **residual fuel oil** as a proxy  
- Incorporated major **geopolitical and localized disruption events**  
- Forecasted production and consumption to **2030** under multiple scenarios  
- Built a **risk index** combining supply volatility, demand exposure, refining rigidity, and Canada’s trade relationships  

These results are visualized in an interactive **Power BI dashboard**.

---

## **🎯 Research Questions**
1. How has the global crude oil mix changed over time?  
2. Which countries produce and consume heavy oil, and how has this changed across historical disruptions?  
3. How concentrated is global heavy crude production??  
4. Which countries are structurally dependent on heavy crude?  
5. What strategic role could Canada play in mitigating future heavy crude shortages?

---

## **📂 Repository Structure**
```bash
project-root/
│ 
├── notebooks/                                                                     # All development notebooks (Databricks-exported)
│   ├── 1-Data-Preparation-ETL/                                                     
│       ├── 01-Canada's Heavy Crude Trade Partners - Ingestion.ipynb               # Process Canada's heavy crude trade data (imports/exports)
│       ├── 01-EIA Country level heavy crude production - data ingestion.ipynb     # Ingest & calculate country-level heavy crude production using % heavy assumptions (from EIA-production-with-percent-heavy-calculation.xlsx)
│       ├── 01-EIA residual fuel consumption API ingestion.ipynb                   # Ingest residual fuel consumption data from EIA API
│       ├── 01-EIA total crude production ingestion.ipynb                          # Ingest total crude oil production data from EIA API
│       ├── 02-Clean consumption EIA data.ipynb                                    # Clean & transform consumption data
│       ├── 02-Update Binary Scenario Variables from Google Drive.ipynb            # Sync predefined exogenous scenario variables (from Timeline-of-historical-events.csv) to gold.exogenous_variables table
│       ├── 02-Update Canada's Trade Relationships from Google Drive.ipynb         # Update country-specific trade shares used in the risk index calculation
│       ├── 03-Create gold - heavy_consumption_timeseries_annual.ipynb             # Gold-layer heavy consumption table creation
│       └── 03-Create prod and heavy_prod_monthly gold.ipynb                       # Gold-layer heavy production table creation
│   └── 2-Modelling-Analysis/                                                      
│       ├── 04-Consumption - Looping All Selected Countries and Run All Scenarios.ipynb    # Batch consumption forecasting across all country-scenario pairs
│       ├── 04-Production - Looping All Countries and Scenarios.ipynb                      # Batch production forecasting across all country-scenario pairs
│       └── 05-Update Index.ipynb                                                          # Compute Heavy-Oil Market Disruption Risk Index
│
├── dashboard/
│   └── Chirality Research - Analysis of Global Heavy-Oil Dependence and Market Disruption Risk - Dashboard.pbix
│
├── supporting-documents-reports/
│   ├── Canada-heavy-crude-trade-exports_Jun2021-Jun2026.csv                 # Canada's heavy crude exports
│   ├── Canada-heavy-crude-trade-imports-Jun2021-Jun2026.csv                 # Canada's heavy crude imports
│   ├── Timeline-of-historical-events.csv                                    # Historical disruption events
│   ├── Assumptions-percent-heavy-oil-production-by-country.xlsx             # Assumption references for country-level heavy crude production share
│   ├── EIA-production-with-percent-heavy-calculation.xlsx                   # Country‑level heavy crude production share values
│   └── Final Report - Chirality Research.pdf                                # Final written report
│
├── LICENSE
├── README.md
└── library-requirements.txt
```
---

## **📊 Data Sources**
- **U.S. Energy Information Administration (EIA)**
- Government reports & industry publications
- Chirality Research domain expertise

## **🛠️ Methodology**
### **1. Literature Review**
Built domain knowledge on API gravity, refining constraints, Canada’s trade relationships, and historical disruption events.

### **2. Heavy‑Oil Production & Consumption Estimation**
Heavy‑oil production is rarely published directly. We estimated heavy‑oil shares for **18 major producing countries**, constructing a **1975–2026** time series.
Residual fuel oil consumption was used as a proxy for heavy‑oil demand due to limited API‑specific consumption data.

### **3. Disruption Event Modelling**
Events included:
- **1973 OPEC Embargo**  
- **1979 Iranian Revolution**  
- **Iran–Iraq War (1980–1988)**  
- **Gulf War (1990–1991)**  
- **Venezuelan sanctions (2017, 2019)**  
- **Pipeline expansions** (Line 3, Line 6, Keystone, TMX)  
- **Fort McMurray wildfires (2016)**  
- **Hurricane Katrina (2005)**  
- **Venezuelan General Strike (2002–2003)**  
- **COVID‑19 shutdowns (2020)**  
- **Russian oil price cap (2022)**  

Events were encoded as structural breaks or temporary shocks.

### **4. Forecasting Models**
Models evaluated:
- **ARIMAX**  
- **SARIMAX**  
- **Prophet**

Training/testing split:  
- Final 3 years of available data = test set
- Remaining history = training set

Best model selected per country based on error metrics.

### **5. Heavy‑Oil Market Disruption Risk Index**
Index components:
- Heavy‑oil supply volatility  
- Heavy‑oil demand exposure  
- Refining rigidity  
- Marine fuel dependence  
- Canada’s exposure to each disruption scenario  

---

## **⚙️ How to Run the Code**
All development and execution occur in **Databricks**, using a structured Bronze → Silver → Gold pipeline and a three‑stage workflow: **Data Preparation (ETL)** → **Forecasting** → **Analysis**.

**Databricks Workspace:**  
https://dbc-91c40ae8-df1c.cloud.databricks.com/browse/folders/3838865724760078?o=7474659271125396

**Suggested Run Sequence (Full Pipeline)**
Refer to numeric digits in front of notebook naming : 01-* → 02-* → 03-* → 04-* → 05-*

---

### **1. Data Preparation (ETL)**
Located under **1‑Data Preparation (ETL)**

**Ingestion (Bronze Layer)**  
1. `01-Canada’s Heavy Crude Trade Partners - Ingestion`  
2. `01-EIA residual fuel consumption API ingestion`  
3. `01-EIA total crude production ingestion`  
4. `01-EIA_Country level heavy crude - data ingestion`  

These notebooks pull raw production, consumption, trade partner, and heavy‑oil proxy data from EIA APIs and external sources.

**Cleaning & Updates (Silver Layer)**  
5. `02-Clean consumption EIA data`  
6. `02-Update Binary Scenario Variables from Google Drive`  
7. `02-Update Canada’s Trade Relationships from Google Drive`  

These notebooks standardize formats, update scenario variables, and prepare model‑ready datasets.

**Gold Table Creation (Gold Layer)**  
8. `03-Create gold - heavy_consumption_timeseries_annual`  
9. `03-Create prod and heavy_prod_monthly gold`  

These produce final business‑ready tables for forecasting, risk index modeling, and dashboard integration.

---

### **2. Forecasting — Production & Consumption Models**
Located under **2‑Forecasting**:

**Validation Scripts (Optional, for testing only)**  
- `(FOR VALIDATION ONLY) Consumption Forecast - Individual Scenario`  
- `(FOR VALIDATION ONLY) Production Forecast - Individual Scenario`  

**Worker Notebooks (Main Forecasting Logic)**  
10. `Consumption Forecast - Single Scenario by Country`  
11. `Production Forecast - Single Scenario by Country`  
12. `Production - Run All Scenarios for a Country and Update Heavy Crude Production`  
13. `04-Consumption - Looping All Selected Countries and Run All Scenarios`  
14. `04-Production - Looping All Countries and Scenarios` 

These notebooks run ARIMAX, SARIMAX, and Prophet models for all countries and all disruption scenarios.

---

### **3. Analysis — Risk Index & Final Outputs**
Located under **3‑Analysis**:

15. `05-Update Index`  

This notebook generates the **Heavy‑Oil Market Disruption Risk Index**, combining supply volatility, demand exposure, refining rigidity, and Canada’s trade exposure.

---

### **4. Running the Workflow**
1. Attach a Databricks cluster  
2. Run **Data Preparation (ETL)** notebooks in order  
3. Run **Forecasting** notebooks (single‑scenario or looping versions)  
4. Run **05-Update Index** to generate final risk index tables  
5. Export Gold tables for Power BI dashboard

---

### **5. Dashboard Integration**
Power BI uses the Import data connectivity mode to load the **Gold‑layer tables** exported from Databricks. 
By avoiding DirectQuery on a capacity-constrained Databricks environment, Import mode ensures fast visuals, stable performance, and full DAX functionality.

---

### **6. Requirements**
All dependencies are managed inside Databricks clusters, list of libraries required are listed in `library-requirements.txt`.

---

## **📈 Key Findings**
- Canada produces the majority of global heavy crude in a market trending toward lighter grades.  
- Heavy‑oil production is highly concentrated, increasing systemic risk.  
- Many countries have structural dependence on heavy crude.  
- Canada’s export relationships with heavy‑oil‑dependent countries are weak, limiting strategic opportunities.  
- Pipeline constraints significantly affect Canada’s ability to capitalize on disruptions.  
- Forecasts show tightening heavy‑oil supply through 2030 under most scenarios.

---

## **📊 Dashboard Preview**
The interactive dashboard is created using Microsoft Power BI.
The Power BI dashboard an interactive view of the project’s core insights, including:
- Country‑level production & consumption forecasts
- Scenario toggles for each disruption event
- Heavy‑oil surplus/deficit projections
- Risk index visualization
- Canada‑specific opportunity analysis

---

## **🔧 Future Improvements**
- Expand heavy‑oil production estimates beyond the initial 18 countries.
- Automate remaining manual inputs (scenario variables, trade relationships).
- Incorporate more granular API‑gravity consumption data instead of relying on residual fuel as a proxy.
- Add support for multi‑event or compound disruption scenarios.
- Strengthen forecasting models with additional exogenous variables (refinery outages, shipping constraints, macroeconomic indicators).
- Improve pipeline capacity modeling, especially API‑gravity‑based throughput effects.
- Enable scheduled or real‑time dashboard refreshes once Databricks capacity allows.

---

## **📜 License**
MIT License (unless otherwise required by Chirality Research)
