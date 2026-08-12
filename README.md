
# POS Agent Revenue Insights

## Turning 1 Million Simulated POS Transactions into Business Intelligence

A large-scale data analytics and Power BI project designed to analyse the economics, operational performance, geographic distribution, customer behaviour, and risk patterns of a Nigerian POS agent network.

The project combines **Python, Pandas, NumPy, Jupyter Notebook, dimensional data modelling, DAX, and Power BI** to build a realistic analytical environment containing **1,000,000 simulated transactions across 13,010 POS agents and 252 LGAs**.

> **Data disclaimer:** This project uses synthetic data. It does not contain private customer transaction records or proprietary data from Moniepoint, OPay, PalmPay, FirstMonie, Paga, or any other payment provider. Provider names and Nigerian geographic information are used to create a realistic analytical scenario.

---

## Project Overview

POS agent networks generate large volumes of transactions, but transaction volume alone doesn't provide enough information to understand business performance.

This project was designed around questions such as:

* Which payment providers generate the most revenue?
* Which states and LGAs have the highest transaction activity?
* Which transaction types contribute most to revenue?
* How does transaction activity change throughout the day?
* What is the relationship between transaction volume and revenue?
* How much revenue is consumed by processing costs?
* What percentage of transactions fail?
* Where are potential fraud indicators concentrated?
* Which customer segments contribute most to transaction activity?
* Are high-volume agents necessarily the most profitable?

The project therefore goes beyond a simple transaction dashboard and models the underlying business environment required to investigate these questions.

---

# Key Project Metrics

| Metric                   |         Value |
| ------------------------ | ------------: |
| Simulated transactions   | **1,000,000** |
| Simulated agents         |    **13,010** |
| Nigerian LGAs            |       **252** |
| Payment providers        |         **5** |
| Transaction fields       |        **23** |
| Transaction success rate |    **98.41%** |
| Transaction failure rate |     **1.59%** |
| Fraud indicator rate     |     **0.32%** |

The success and fraud figures above describe the generated dataset and should not be interpreted as real-world industry statistics.

---

# Technology Stack

### Data generation & analysis

* Python
* Pandas
* NumPy
* Jupyter Notebook

### Business intelligence

* Microsoft Power BI
* DAX
* Power Query
* Dimensional data modelling

### Documentation & version control

* Git
* GitHub
* Git LFS

---

# Data Architecture

The project follows a dimensional modelling approach rather than relying on one large flat table.

```text
                    dim_date
                       │
                       │
dim_agent ─────── fact_transactions ─────── dim_provider
                       │
                       │
              dim_transaction_type
                       │
                       │
                 dim_location
                       │
                    dim_lga
```

The central fact table contains the transaction-level records, while dimension tables provide descriptive attributes for filtering and analysis.

---

# Data Model

## Fact Table

### `fact_transactions.csv`

Contains 1,000,000 simulated transaction records.

Key fields include:

* Transaction_ID
* Timestamp
* Transaction_Date
* Hour
* Weekday
* Weekend
* Agent_ID
* Provider
* State
* Geo_Zone
* LGA
* Business_Category
* Agent_Tier
* Customer_Segment
* Payment_Method
* Transaction_Type
* Transaction_Amount
* Commission
* Processing_Cost
* Gross_Revenue
* Net_Revenue
* Transaction_Status
* Fraud_Status

---

# Dimension Tables

### `dim_agent.csv`

Contains the simulated POS agent population and operational characteristics.

Includes:

* Agent_ID
* Business_Name
* Provider
* State
* Geo_Zone
* LGA
* Business_Category
* Agent_Tier
* KYC_Level
* Terminal_Type
* Registration_Date
* Years_in_Business
* Risk_Score
* Average_Daily_Customers
* Latitude
* Longitude

### `dim_date.csv`

Provides the calendar structure required for time-series analysis and Power BI date intelligence.

### `dim_lga.csv`

Contains the LGA-level geographic dimension used for location analysis.

### `dim_location.csv`

Provides the geographic structure used by the dashboard.

### `dim_provider.csv`

Contains provider-level reference data.

### `dim_transaction_type.csv`

Contains the transaction-type reference structure.

---

# Dashboard

The Power BI report contains three main analytical pages.

## 01 — Executive Overview

Provides a high-level view of network performance.

Key areas:

* Gross Revenue
* Transaction Value
* Transaction Volume
* Success Rate
* Active Agents
* Net Revenue
* Monthly Net Revenue Trend
* Net Revenue by Provider
* Transaction Volume by Type

The purpose of this page is to answer:

> **How is the overall network performing?**

---

## 02 — Geographic & Provider Intelligence

Focuses on where activity occurs and how providers perform across the network.

Key analysis:

* Net Revenue by Provider
* Transaction Volume by Provider
* Top States by Net Revenue
* Top States by Transaction Volume
* Top LGAs by Net Revenue
* Geographic Revenue Concentration

The purpose of this page is to answer:

> **Where is the business activity happening, and which providers are capturing it?**

---

## 03 — Operations, Customers & Risk

Examines the operational and risk characteristics of the transaction network.

Key analysis:

* Transaction Activity by Hour
* Net Revenue by Transaction Type
* Customer Segment Mix
* Transaction Success vs Failure
* Clean vs Fraud Transactions
* Fraud Transactions by Provider
* Revenue vs Processing Cost

The purpose of this page is to answer:

> **What operational, customer, and risk patterns exist beneath the headline numbers?**

---

# Interactive Features

The Power BI report includes:

* Date filtering
* Provider filtering
* Cross-visual interactions
* Geographic filtering
* Interactive page navigation
* Tooltips
* State-level drill-through
* KPI cards
* Interactive geographic analysis

The report is designed so users can move from a high-level business view into geographic, provider, operational, and risk analysis.

---

# Data Quality Checks

The generated transaction dataset was validated before being imported into Power BI.

Validation included:

* Missing-value checks
* Duplicate transaction ID checks
* Transaction status distribution
* Fraud status distribution
* Dimension table validation
* Duplicate Agent ID checks
* Relationship validation
* Transaction row-count validation

Final transaction validation:

```text
Rows:              1,000,000
Columns:           23
Duplicate IDs:     0
Missing values:    0
```

Agent dimension validation:

```text
Agents:            13,010
Duplicate IDs:     0
Missing values:    0
```

---

# Repository Structure

```text
pos-agent-revenue-insights/
│
├── README.md
│
├── data/
│   ├── dim_agent.csv
│   ├── dim_date.csv
│   ├── dim_lga.csv
│   ├── dim_location.csv
│   ├── dim_provider.csv
│   ├── dim_transaction_type.csv
│   └── README.md
│
├── notebooks/
│   ├── 01_Data_Model_Design.ipynb
│   └── 02_Data_Generation.ipynb
│
├── powerbi/
│   └── POS_Agent_Revenue_Insights.pbix
│
├── screenshots/
│   ├── executive_overview.png
│   ├── geographic_provider.png
│   └── operations_customers_risk.png
│
└── documentation/
    ├── data_dictionary.md
    └── methodology.md
```

The Power BI `.pbix` file is managed using **Git LFS** because of its file size.

---

# Reproducibility

The project was built so the analytical dataset can be regenerated using the Python notebooks.

### Notebook 1

`01_Data_Model_Design.ipynb`

Documents:

* Business problem
* Analytical objectives
* Entities
* Relationships
* Assumptions
* Data architecture
* Business rules

### Notebook 2

`02_Data_Generation.ipynb`

Generates:

* Agent dimension
* Location dimensions
* Date dimension
* Transaction type dimension
* Provider dimension
* 1,000,000 transaction fact table
* KPI summary tables

---

# Important Assumptions

This is a simulated business environment.

The project uses assumptions to model:

* agent activity
* customer behaviour
* transaction values
* commission structures
* processing costs
* transaction failures
* fraud indicators
* provider distribution
* geographic activity
* customer segments
* operational behaviour

These assumptions are designed for analytical realism and portfolio demonstration rather than statistical representation of the Nigerian POS industry.

---

# Why This Project Matters

The objective wasn't simply to produce a visually attractive dashboard.

The project demonstrates an end-to-end analytics workflow:

```text
Business Problem
       ↓
Data Model
       ↓
Synthetic Data Generation
       ↓
Data Validation
       ↓
Dimensional Model
       ↓
DAX Measures
       ↓
Power BI Dashboard
       ↓
Interactive Analysis
       ↓
Business Insights
```

The dashboard is therefore the final layer of a broader data analytics workflow.

---

# Author

**Akpan Daniel**

Data Analyst | Business Intelligence | Python | Power BI | DAX

---

## License

This project is intended for portfolio, educational, and analytical demonstration purposes.

The synthetic dataset does not represent real customer transaction data.
