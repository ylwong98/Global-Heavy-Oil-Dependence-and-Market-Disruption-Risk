# **Shifting Crude Oil Quality & Refining Constraints: A Data‑Driven Analysis of Global Heavy-Oil Dependence and Market Disruption Risk**
### **Professional Graduate Industry Capstone - Chirality Research x University of Calgary**
**Team:**  
- [Andrew Gellner](https://www.linkedin.com/in/andrew-gellner-data-analytics/) 
- [Michael Morgan](https://www.linkedin.com/in/michael-morgan-calgary/)  
- [Yu Ling (Elaine) Wong](https://www.linkedin.com/in/yu-ling-wong/) 
---

## **📌 Project Overview**
Heavy crude oil is essential for producing marine fuels, bunker oil, and heavy distillates. Canada is a major heavy‑oil producer, but faces constraints related to refining configuration, transportation capacity, and shifting global supply dynamics.

This project delivers:
- A **Heavy‑Oil Market Disruption Risk Index**  
- **Production & consumption forecasts** to 2030  
- **Scenario modelling** for geopolitical & localized disruptions  
- A **Power BI dashboard** for interactive exploration  
- Strategic insights for Canada’s heavy‑oil export opportunities  

---

## **📘 Executive Summary**
Heavy crude oil supply is increasingly constrained, while many countries remain structurally dependent on heavy crude for marine fuel production and refining operations. Canada produces the majority of heavy crude in a market trending toward lighter grades, creating both risk and opportunity.

To quantify these dynamics, we:
- Estimated heavy‑oil production for **18 major producing countries (1973–2026)**  
- Modeled heavy‑oil consumption using **residual fuel oil** as a proxy  
- Incorporated major **geopolitical and localized disruption events**  
- Forecasted production and consumption to **2030** under multiple scenarios  
- Built a **risk index** combining heavy‑oil supply and demand shocks, and Canada’s trade‑based exposure to each disruption scenario

Results are visualized in an interactive **Power BI dashboard**.

---

## **🎯 Research Questions**
1. How has the global crude oil mix changed over time?  
2. Which countries produce and consume heavy oil, and how has this changed across historical disruptions?  
3. How concentrated is global heavy crude production??  
4. Which countries are structurally dependent on heavy crude?  
5. What strategic role could Canada play in mitigating future heavy crude shortages?

---

## **📂 Repository Structure**
```text
heavy-oil-analysis/
│ 
├── notebooks/                                                                     # All development notebooks (Databricks-exported)
│   ├── 1-Data-Preparation-ETL/                                                     
│   │   ├── 01-Canada's Heavy Crude Trade Partners - Ingestion.ipynb               # Process Canada's heavy crude trade data (imports/exports)
│   │   ├── 01-EIA Country level heavy crude production - data ingestion.ipynb     # Ingest & calculate country-level heavy crude production using % heavy assumptions (from EIA-production-with-percent-heavy-calculation.xlsx)
│   │   ├── 01-EIA residual fuel consumption API ingestion.ipynb                   # Ingest residual fuel consumption data from EIA API
│   │   ├── 01-EIA total crude production ingestion.ipynb                          # Ingest total crude oil production data from EIA API
│   │   ├── 02-Clean consumption EIA data.ipynb                                    # Clean & transform consumption data
│   │   ├── 02-Update Binary Scenario Variables from Google Drive.ipynb            # Sync predefined exogenous scenario variables (from Timeline-of-historical-events.csv) to gold.exogenous_variables table
│   │   ├── 02-Update Canada's Trade Relationships from Google Drive.ipynb         # Update country-specific trade shares used in the risk index calculation
│   │   ├── 03-Create gold - heavy_consumption_timeseries_annual.ipynb             # Gold-layer heavy consumption table creation
│   │   └── 03-Create prod and heavy_prod_monthly gold.ipynb                       # Gold-layer heavy production table creation
│   └── 2-Modelling-Analysis/                                                      
│       ├── 04-Consumption - Looping All Selected Countries and Run All Scenarios.ipynb    # Batch consumption forecasting across all country-scenario pairs
│       ├── 04-Production - Looping All Countries and Scenarios.ipynb                      # Batch production forecasting across all country-scenario pairs
│       └── 05-Update Index.ipynb                                                          # Compute Heavy-Oil Market Disruption Risk Index
│
├── dashboard/
│   └── Chirality Research - Analysis of Global Heavy-Oil Dependence and Market Disruption Risk - Dashboard.pbix
│
├── supporting-documents-reports/
│   ├── Canada-heavy-crude-trade-exports_Jun2021-Jun2026.csv                          # Canada's heavy crude exports
│   ├── Canada-heavy-crude-trade-imports-Jun2021-Jun2026.csv                          # Canada's heavy crude imports
│   ├── Timeline-of-historical-events.csv                                             # Historical disruption events
│   ├── Assumptions-percent-heavy-oil-production-by-country.xlsx                      # Assumption references for country-level heavy crude production share
│   ├── EIA-production-with-percent-heavy-calculation.xlsx                            # Country‑level heavy crude production share values
│   ├── Final Report.pdf                                                              # Project final written report
│   ├── Dashboard Main Interface.png                                                  # Dashboard main page diagram
│   ├── Data Pipeline Diagram.png                                                     # Project data pipeline diagram
│   └── Global Heavy Oil Dependence and Market Disruption Risk - Presentation.pptx    # Project presentation slides    
│
├── LICENSE
├── README.md
├── databricks-jupyter-notebooks-description.txt
└── library-requirements.txt
```
---

## **📊 Data Sources**
- **U.S. Energy Information Administration (EIA)**

  <table>
    <thead>
      <tr>
        <th>Category</th>
        <th>Data</th>
        <th>Source Period</th>
        <th>Notes</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Production</td>
        <td>Total Crude Production<br>(Monthly)</td>
        <td>Jan&nbsp;1973&nbsp;&#8209;&nbsp;Feb&nbsp;2026</td>
        <td>
          "crude oil including lease condensate value" as proxy for total crude volumes. Assumptions of % heavy crude shares will be used to calculate heavy crude volumes. [
          <a href="https://www.eia.gov/international/data/world/petroleum-and-other-liquids/monthly-petroleum-and-other-liquids-production?pd=5&p=0000000000000000000000000000000000vg&u=0&f=M&v=mapbubble&a=-&i=none&vo=value&t=C&g=00000000000000000000000000000000000000000000000001&l=249-ruvvvvvfvtvnvv1vrvvvvfvvvvvvfvvvou20evvvvvvvvvvnvvvs0008&s=94694400000&e=1775001600000">
            Link
          </a>]
        </td>
      </tr>
      <tr>
        <td>Consumption</td>
        <td>Residual Fuel Consumption<br>(Annual)</td>
        <td>1980 &#8209; 2024</td>
        <td>
          Residual fuel as proxy for heavy crude volumes. Monthly data not available for residual fuel consumption. [
          <a href="https://www.eia.gov/international/data/world/petroleum-and-other-liquids/more-petroleum-and-other-liquids-data?pd=5&p=00000000002&u=0&f=A&v=mapbubble&a=-&i=none&vo=value&t=C&g=none&l=249-ruvvvvvfvtvnvv1vrvvvvfvvvvvvfvvvou20evvvvvvvvvvnvuvs0008&s=315532800000&e=1735689600000">
            Link
          </a>]
        </td>
      </tr>
    </tbody>
  </table>

- **Statistics Canada (StatCan)** [[Link](https://www150.statcan.gc.ca/n1/pub/71-607-x/71-607-x2021004-eng.htm)]
  <table>
    <thead>
      <tr>
        <th>Category</th>
        <th>Source Period</th>
        <th>Notes</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Production</td>
        <td>Jun&nbsp;2021&nbsp;&#8209;&nbsp;Jun&nbsp;2026</td>
        <td>Commodity selected: Petroleum & bituminous min oils, crude, relative density >= 0.9042 (< 25°A.P.I.)</td>
      </tr>
      <tr>
        <td>Consumption</td>
        <td>Jun&nbsp;2021&nbsp;&#8209;&nbsp;Jun&nbsp;2026</td>
        <td>Commodity selected: Petroleum & bituminous min oils, crude, relative density >= 0.9042 (< 25°A.P.I.)</td>
      </tr>
    </tbody>
  </table>
- Government reports & industry publications
- Chirality Research domain expertise

---

## **🛠️ Methodology**
### **1. Literature Review**
Built domain knowledge on API gravity, refining constraints, Canada’s trade relationships, and historical disruption events.<br><br>

### **2. Heavy‑Oil Production & Consumption Estimation**
Estimated heavy‑oil shares for **18 major producing countries** (1973–2026).
Used residual fuel oil as a proxy for heavy‑oil demand. <br><br>

### **3. Disruption Event Modelling**
Events encoded as structural breaks or temporary shocks:

<table>
  <tbody>
    <tr>
      <td><b>1973 OPEC Embargo</b></td>
      <td><b>1979 Iranian Revolution</b></td>
      <td><b>Iran–Iraq War (1980–1988)</b></td>
      <td><b>Gulf War (1990–1991)</b></td>
    </tr>
    <tr>
      <td><b>Venezuelan Sanctions (2017, 2019)</b></td>
      <td><b>Pipeline Expansions (Line 3, Line 6, Keystone, TMX)</b></td>
      <td><b>Fort McMurray Wildfires (2016)</b></td>
      <td><b>Hurricane Katrina (2005)</b></td>
    </tr>
    <tr>
      <td><b>Venezuelan General Strike (2002–2003)</b></td>
      <td><b>COVID‑19 Shutdowns (2020)</b></td>
      <td><b>Russian Oil Price Cap (2022)</b></td>
      <td><b>Iraq War (2003)</b></td>
    </tr>
    <tr>
      <td><b>Gulf War-related Trade Sanctions (1991-1996)<b></td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
  </tbody>
</table>
<br>
        
### **4. Forecasting Models**
**Models Evaluated:** **_ARIMAX_**, **_SARIMAX_**, **_Prophet_**

**Train/Test Split:**
- Consumption: Final 3 years = test set
- Production: Final 12 months = test set

**Modelling Framework:**
<table>
  <thead>
    <tr>
      <th rowspan="2">Component</th>
      <th colspan="2">Period</th>
      <th rowspan="2">Description</th>
    </tr>
    <tr>
      <th>Production</th>
      <th>Consumption</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Training Period</b></td>
      <td>Jan 1973 – Feb 2025 </td>
      <td>1980 – 2021 </td>
      <td>Models trained on historical heavy‑oil production and residual‑fuel‑oil consumption data</td>
    </tr>
    <tr>
      <td><b>Validation Period</b></td>
      <td>Feb 2025 – Feb 2026 </td>
      <td>2022 – 2024 </td>
      <td>Final 3 years (consumption) and final 12 months (production) used for out‑of‑sample testing</td>
    </tr>
    <tr>
      <td><b>Retrain Period</b></td>
      <td>1973 – 2026 </td>
      <td>1980 – 2024 </td>
      <td>Models retrained on the full dataset before generating final scenario forecasts</td>
    </tr>
    <tr>
      <td><b>Forecast Period</b></td>
      <td>2026 – 2030 </td>
      <td>2025 – 2030 </td>
      <td>Heavy‑oil production and consumption projections used for scenario analysis and risk‑index calculation</td>
    </tr>
  </tbody>
</table>


Best model selected per country using MAPE.<br><br>

### **5. Heavy‑Oil Market Disruption Risk Index**
Index components:
- Heavy‑oil supply shock
- Heavy‑oil demand shock
- Canada’s exposure weight to each disruption scenario  

---

## **⚙️ How to Run the Code**
All development and execution occur in **Databricks**, using a structured Bronze → Silver → Gold pipeline and a three‑stage workflow: **Data Preparation (ETL)** → **Forecasting** → **Analysis**.

**Databricks Workspace:**  
[https://dbc-91c40ae8-df1c.cloud.databricks.com/browse/folders/3838865724760078?o=7474659271125396](https://dbc-91c40ae8-df1c.cloud.databricks.com/browse/folders/3838865724760078?o=7474659271125396)

**Data Pipeline Diagram:**<br>
![Data Pipeline Diagram](supporting-documents-reports/Data%20Pipeline%20Diagram.png)

**Suggested Run Sequence (Full Pipeline):**
Refer to numeric digits in front of notebook naming : 01-* → 02-* → 03-* → 04-* → 05-*

A description of notebook functions is provided in `databricks-jupyter-notebooks-description.txt` within the `main` branch.

**Running the Workflow:**
1. Attach a Databricks cluster  
2. Run **Data Preparation (ETL)** notebooks in order (01 → 02 → 03)
3. Run **Forecasting** notebooks (04)  
4. Run **Analysis** notebook - (05)  
5. Export Gold tables for Power BI dashboard

**Requirements:**
All dependencies are managed inside Databricks clusters, list of libraries required are listed in `library-requirements.txt` within the `main` branch.

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
The interactive dashboard is built in **Microsoft Power BI** using **Import mode** to load the **Gold‑layer tables** exported from Databricks. 
Import mode avoids the performance limitations of DirectQuery on a capacity‑constrained environment, ensuring fast visuals, stable performance, and full DAX functionality.

The dashboard provides an interactive view of the project’s core insights, including:
- Country‑level production & consumption forecasts
- Scenario toggles for each disruption event
- Heavy‑oil surplus/deficit projections
- Risk index visualization
- Canada‑specific opportunity analysis

![Dashboard Main Interface](supporting-documents-reports/Dashboard%Main%Interface.png)<br><br> 

A copy of the dashboard file is available in the `dashboard/` folder of the repository.
`Chirality Research - Analysis of Global Heavy-Oil Dependence and Market Disruption Risk - Dashboard.pbix`

---

## **🔧 Future Improvements**
- Expand heavy‑oil production estimates beyond the initial 18 countries.
- Automate remaining manual inputs (scenario variables, trade relationships).
- Incorporate more granular API‑gravity consumption data instead of relying on residual fuel as a proxy.
- Add support for multi‑event or compound disruption scenarios.
- Strengthen forecasting models with additional exogenous variables (refinery outages, shipping constraints, macroeconomic indicators).
- Improve pipeline capacity modelling, especially API‑gravity‑based throughput effects.
- Enable scheduled or real‑time dashboard refreshes once Databricks capacity allows.

---

## **📜 License**
MIT License (unless otherwise required by Chirality Research)
