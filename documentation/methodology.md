# Methodology

## POS Agent Revenue Insights

## 1. Project Objective

The objective of this project was to build an end-to-end business intelligence system capable of analysing a simulated Nigerian POS agent network.

Rather than starting with a dashboard, the project began with the underlying business model.

The workflow was:

```text
Business Questions
       ↓
Business/Data Model
       ↓
Entity Design
       ↓
Synthetic Data Generation
       ↓
Data Validation
       ↓
Dimensional Model
       ↓
DAX & KPI Development
       ↓
Power BI Dashboard
       ↓
Interactive Analysis
```

---

# 2. Why Synthetic Data Was Used

Real POS transaction data is commercially sensitive and generally unavailable at the level of detail required for a public portfolio project.

Using fabricated random numbers, however, would not provide a sufficiently useful analytical environment.

The solution was to create a **synthetic but structured dataset** designed to behave like a plausible agent-banking environment.

The dataset therefore contains relationships between:

* agents
* providers
* geography
* transaction types
* customers
* transaction values
* commissions
* processing costs
* operational outcomes
* risk indicators

The resulting data is intended for analytical demonstration, not statistical claims about the real Nigerian market.

---

# 3. Agent Population

The model contains:

**13,010 simulated agents**

Each agent receives a profile containing operational, geographic, business, and risk attributes.

The agent model includes:

* provider
* state
* LGA
* business category
* agent tier
* KYC level
* terminal type
* registration date
* years in business
* risk score
* average daily customers
* geographic coordinates

This creates a population that can be analysed at the agent, provider, state, and LGA levels.

---

# 4. Geographic Model

The project represents:

**252 LGAs**

The geographic hierarchy is structured around:

```text
Geo Zone
    ↓
State
    ↓
LGA
    ↓
Agent
    ↓
Transaction
```

This enables geographic analysis in Power BI and supports questions around concentration and regional performance.

Latitude and longitude attributes were also generated for agents to support geographic visualisation.

---

# 5. Transaction Generation

The final transaction fact table contains:

**1,000,000 transactions**

Each transaction is assigned:

* a unique transaction ID
* timestamp
* date
* hour
* weekday
* weekend status
* agent
* provider
* state
* geographic zone
* LGA
* business category
* agent tier
* customer segment
* payment method
* transaction type
* transaction amount
* commission
* processing cost
* revenue
* transaction status
* fraud status

---

# 6. Transaction Behaviour

The generation process was designed to avoid treating every transaction as an identical random observation.

Transaction behaviour is influenced by the characteristics of the simulated business environment.

Examples include:

* different transaction types
* different transaction amounts
* different customer segments
* different provider distributions
* different agent characteristics
* weekday/weekend behaviour
* hourly activity
* successful and failed transactions
* operational costs
* risk indicators

This makes the resulting dataset more suitable for analytical modelling than a simple uniform random dataset.

---

# 7. Revenue Model

The revenue structure was designed around transaction commissions.

For each transaction:

```text
Gross Revenue = Commission
```

Processing costs are then applied:

```text
Net Revenue = Gross Revenue - Processing Cost
```

This distinction allows the dashboard to analyse both revenue generation and the cost required to process transactions.

---

# 8. Transaction Status

Transactions are assigned an operational status.

The final generated dataset contains:

```text
Successful: 984,066
Failed:      15,934
```

This corresponds to:

```text
Success Rate ≈ 98.41%
Failure Rate ≈ 1.59%
```

These are characteristics of the synthetic dataset and are not real-world POS industry statistics.

---

# 9. Fraud Simulation

The model also contains a synthetic fraud indicator.

Final distribution:

```text
Clean:  996,804
Fraud:    3,196
```

This represents approximately:

```text
Fraud Rate ≈ 0.32%
```

The field is intended to demonstrate risk analysis and should not be interpreted as an actual fraud rate for any provider or market.

---

# 10. Customer Segmentation

Transactions are assigned customer segments to allow the dashboard to examine how different customer groups contribute to transaction activity.

Customer segmentation is used primarily for:

* transaction mix
* transaction volume
* revenue analysis
* operational comparison

The segmentation is synthetic and does not represent a real provider's customer classification system.

---

# 11. Data Generation Architecture

The generation process was separated into logical components rather than attempting to create the entire dataset in a single operation.

The workflow included:

### Step 1 — Model design

Define:

* entities
* relationships
* fields
* business assumptions
* analytical requirements

### Step 2 — Agent generation

Generate the agent population and assign:

* provider
* location
* business attributes
* operational characteristics
* risk attributes

### Step 3 — Geographic dimensions

Create the geographic reference tables and LGA structure.

### Step 4 — Date dimension

Create the calendar dimension used for Power BI time analysis.

### Step 5 — Transaction generation

Generate the 1,000,000 transaction fact records using chunk-based processing.

Chunk generation was used to make large-scale transaction creation more manageable in a Jupyter/Python environment.

### Step 6 — Validation

Validate:

* row counts
* duplicate IDs
* missing values
* distributions
* data types
* relationships

### Step 7 — Export

Export the fact and dimension tables as CSV files for Power BI.

---

# 12. Data Validation

Validation was performed before the Power BI modelling stage.

The final transaction dataset achieved:

```text
Rows:             1,000,000
Columns:          23
Missing values:   0
Duplicate IDs:    0
```

The agent dimension achieved:

```text
Agents:           13,010
Missing values:   0
Duplicate IDs:    0
```

The validation stage was important because generating a large dataset is not sufficient by itself.

The data must also be structurally consistent before it becomes useful for analysis.

---

# 13. Power BI Data Model

The Power BI model follows a dimensional structure.

The transaction fact table connects to descriptive dimensions through key fields.

Core relationships include:

```text
dim_agent[Agent_ID]
        1
        │
        *
fact_transactions[Agent_ID]
```

```text
dim_provider[Provider]
        1
        │
        *
fact_transactions[Provider]
```

```text
dim_transaction_type[Transaction_Type]
        1
        │
        *
fact_transactions[Transaction_Type]
```

```text
dim_date[Date]
        1
        │
        *
fact_transactions[Transaction_Date]
```

This structure supports reusable measures and consistent filtering across the report.

---

# 14. Time Intelligence

A dedicated date dimension was used rather than relying only on the transaction date column.

The date dimension contains:

* year
* quarter
* month
* month number
* month-year
* weekday
* weekday number
* weekend indicator

Two sorting columns were specifically used to maintain chronological ordering:

```text
MonthYear_Sort
DayOfWeekNumber
```

This prevents Power BI from displaying months or weekdays alphabetically.

---

# 15. Dashboard Design

The final Power BI report was divided into three analytical perspectives.

## Executive Overview

Focus:

**What is happening?**

The page provides the high-level performance picture.

## Geographic & Provider Intelligence

Focus:

**Where is it happening and who is driving it?**

This page examines provider and geographic performance.

## Operations, Customers & Risk

Focus:

**Why might performance look this way?**

This page examines transaction timing, customer segments, failures, fraud indicators, transaction types, and processing costs.

---

# 16. Interactivity

The dashboard includes:

* date slicers
* provider filtering
* cross-visual filtering
* geographic interaction
* report-page tooltips
* drill-through
* page navigation

The goal is to allow users to move from summary information into increasingly detailed analysis.

---

# 17. Design Philosophy

The dashboard was deliberately designed around business questions rather than filling available canvas space with visuals.

Each visual should support at least one analytical purpose:

```text
Metric
  ↓
Question
  ↓
Visual
  ↓
Interaction
  ↓
Decision
```

This approach reduces unnecessary visuals and keeps the dashboard focused on exploration and decision support.

---

# 18. Limitations

There are several important limitations.

### Synthetic data

The data is generated and does not represent actual provider transactions.

### Assumption-driven behaviour

Transaction distributions, commission structures, processing costs, risk indicators, and other behaviours are modelling assumptions.

### Geographic representation

The geographic structure is intended for analytical demonstration rather than precise measurement of real POS activity.

### Fraud indicators

Fraud status is simulated and should not be interpreted as evidence of actual fraud patterns.

### Provider comparisons

Provider-level comparisons describe the generated dataset only.

---

# 19. Reproducibility

The project includes two primary notebooks.

### `01_Data_Model_Design.ipynb`

Documents the business model, entities, relationships, assumptions, and analytical design.

### `02_Data_Generation.ipynb`

Generates the synthetic dimensions, transaction fact table, KPI summaries, performs validation, and exports the analytical datasets.

The objective is for another analyst to be able to understand not only the final dashboard but also how the underlying analytical environment was constructed.

---

# 20. Final Analytical Principle

The central principle behind the project is:

> **A dashboard should not simply display data. It should make the next business question easier to ask.**

The POS Agent Revenue Insights project therefore treats Power BI as the final analytical layer of a broader data engineering, modelling, and business intelligence workflow.
