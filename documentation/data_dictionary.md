# Data Dictionary

## POS Agent Revenue Insights

This document describes the datasets used in the POS Agent Revenue Insights project, including the fact table, dimensions, measures, and important business fields.

> **Data type note:** The datasets are synthetic and were generated specifically for this analytical project.

---

# 1. Fact Transactions

## `fact_transactions.csv`

**Rows:** 1,000,000
**Columns:** 23

This is the central transaction-level fact table.

| Column               | Description                                                                       |
| -------------------- | --------------------------------------------------------------------------------- |
| `Transaction_ID`     | Unique identifier assigned to each transaction                                    |
| `Timestamp`          | Date and time at which the transaction occurred                                   |
| `Transaction_Date`   | Calendar date of the transaction                                                  |
| `Hour`               | Hour of the day extracted from the transaction timestamp                          |
| `Weekday`            | Day of the week                                                                   |
| `Weekend`            | Indicates whether the transaction occurred on a weekend                           |
| `Agent_ID`           | Unique identifier of the POS agent processing the transaction                     |
| `Provider`           | Payment provider associated with the agent                                        |
| `State`              | Nigerian state associated with the agent                                          |
| `Geo_Zone`           | Geographic zone associated with the state                                         |
| `LGA`                | Local Government Area associated with the agent                                   |
| `Business_Category`  | Category of the agent's business                                                  |
| `Agent_Tier`         | Operational tier assigned to the agent                                            |
| `Customer_Segment`   | Customer category associated with the transaction                                 |
| `Payment_Method`     | Payment channel used for the transaction                                          |
| `Transaction_Type`   | Type of transaction performed                                                     |
| `Transaction_Amount` | Monetary value processed by the transaction                                       |
| `Commission`         | Commission generated from the transaction                                         |
| `Processing_Cost`    | Simulated operational/provider processing cost                                    |
| `Gross_Revenue`      | Revenue generated before processing cost                                          |
| `Net_Revenue`        | Revenue remaining after processing cost                                           |
| `Transaction_Status` | Indicates whether the transaction was successful or failed                        |
| `Fraud_Status`       | Synthetic risk classification indicating clean or potentially fraudulent activity |

---

# 2. Agent Dimension

## `dim_agent.csv`

**Rows:** 13,010
**Columns:** 16

This dimension describes the simulated POS agent population.

| Column                    | Description                                        |
| ------------------------- | -------------------------------------------------- |
| `Agent_ID`                | Unique identifier for each agent                   |
| `Business_Name`           | Simulated business name                            |
| `Provider`                | Payment provider associated with the agent         |
| `State`                   | State where the agent operates                     |
| `Geo_Zone`                | Geographic zone                                    |
| `LGA`                     | Local Government Area                              |
| `Business_Category`       | Agent business category                            |
| `Agent_Tier`              | Agent performance/operational tier                 |
| `KYC_Level`               | Simulated KYC classification                       |
| `Terminal_Type`           | Type of POS terminal assigned                      |
| `Registration_Date`       | Date the agent joined the simulated network        |
| `Years_in_Business`       | Estimated years the business has operated          |
| `Risk_Score`              | Simulated agent risk score                         |
| `Average_Daily_Customers` | Estimated average number of customers served daily |
| `Latitude`                | Simulated geographic latitude                      |
| `Longitude`               | Simulated geographic longitude                     |

---

# 3. Date Dimension

## `dim_date.csv`

The date dimension supports time-based analysis in Power BI.

Important fields include:

| Field             | Purpose                                      |
| ----------------- | -------------------------------------------- |
| `Date`            | Calendar date and primary date key           |
| `Year`            | Calendar year                                |
| `Quarter`         | Calendar quarter                             |
| `Month`           | Month name                                   |
| `MonthNumber`     | Numeric month used for chronological sorting |
| `MonthYear`       | Combined month/year reporting label          |
| `MonthYear_Sort`  | Numeric sorting key for MonthYear            |
| `Weekday`         | Day name                                     |
| `DayOfWeekNumber` | Numeric weekday sorting key                  |
| `Weekend`         | Weekend indicator                            |

The numeric sorting fields are intentionally kept in the date dimension so Power BI can display chronological labels correctly.

---

# 4. LGA Dimension

## `dim_lga.csv`

Contains the geographic LGA structure used for analysis.

Primary attributes include:

* LGA
* State
* Geographic zone
* Geographic identifiers used by the analytical model

The project contains **252 represented LGAs**.

---

# 5. Location Dimension

## `dim_location.csv`

Provides geographic reference information used to support location-level analysis and mapping.

Typical attributes include:

* State
* Geographic zone
* LGA
* Latitude
* Longitude

---

# 6. Provider Dimension

## `dim_provider.csv`

Contains the payment provider reference structure used by the model.

The simulated dataset contains five providers:

* Moniepoint
* OPay
* PalmPay
* FirstMonie
* Paga

These names are used strictly for the synthetic modelling scenario and do not imply access to provider-owned data.

---

# 7. Transaction Type Dimension

## `dim_transaction_type.csv`

Provides the reference structure for transaction categories used in the fact table.

Examples represented in the generated transaction data include:

* Cash Deposit
* Cash Withdrawal
* Bank Transfer
* Bill Payment

The dimension allows transaction types to be analysed independently of the transaction fact table.

---

# 8. KPI Summary Tables

The project also exports pre-aggregated analytical tables used for validation, exploration, and Power BI support.

### `kpi_daily.csv`

Daily transaction and revenue performance.

### `kpi_provider.csv`

Provider-level performance.

### `kpi_state.csv`

State-level performance.

### `kpi_lga.csv`

LGA-level performance.

### `kpi_transaction_type.csv`

Transaction-type performance.

### `kpi_customer_segment.csv`

Customer-segment performance.

These KPI tables should be treated as analytical summaries rather than replacements for the underlying fact table.

---

# 9. Key Business Calculations

## Gross Revenue

Revenue generated from the transaction before processing costs.

Conceptually:

```text
Gross Revenue = Commission
```

within the generated model.

## Net Revenue

Revenue remaining after the simulated processing cost.

```text
Net Revenue = Gross Revenue - Processing Cost
```

## Success Rate

Percentage of transactions classified as successful.

```text
Success Rate =
Successful Transactions / Total Transactions
```

## Failure Rate

Percentage of transactions classified as failed.

```text
Failure Rate =
Failed Transactions / Total Transactions
```

## Fraud Rate

Percentage of transactions classified with the synthetic fraud indicator.

```text
Fraud Rate =
Fraud Transactions / Total Transactions
```

## Profit Margin

Net revenue expressed relative to gross revenue.

```text
Profit Margin =
Net Revenue / Gross Revenue
```

---

# 10. Data Quality Rules

The generated data was validated against the following requirements:

### Transaction IDs

Every transaction must have a unique `Transaction_ID`.

Final result:

```text
Duplicate transaction IDs: 0
```

### Agent IDs

Every agent must have a unique `Agent_ID`.

Final result:

```text
Duplicate Agent IDs: 0
```

### Missing values

Required fields were checked for null values.

Final result:

```text
Missing transaction values: 0
Missing agent values: 0
```

### Transaction volume

The final fact table contains:

```text
1,000,000 rows
```

### Status validation

Generated transaction statuses were checked to ensure both successful and failed transactions existed.

### Fraud validation

The generated dataset includes both clean and fraud-indicated records.

---

# 11. Data Interpretation

The dataset should be interpreted as a **synthetic business simulation**.

The values are designed to support realistic analytical behaviour and demonstrate data modelling techniques.

They should not be interpreted as:

* actual Nigerian POS industry statistics
* actual provider market share
* actual provider revenue
* actual customer behaviour
* actual fraud rates
* actual transaction volumes

This distinction is important when presenting the project publicly.
