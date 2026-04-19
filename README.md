# MoPhones Credit Risk Analysis

## Overview

This project analyzes MoPhones credit portfolio performance, customer behavior, and customer satisfaction (NPS) using multi-period credit snapshots and customer-level datasets.

The goal is to understand:

* Portfolio health trends over time
* Risk differences across customer segments
* Relationship between credit performance and customer experience
* Data quality limitations and structural improvements

---

## Data Sources

The analysis uses the following datasets:

### 1. Credit Data Snapshots (Time Series)

* Credit Data - 01-01-2025.csv
* Credit Data - 30-03-2025.csv
* Credit Data - 30-06-2025.csv
* Credit Data - 30-09-2025.csv
* Credit Data - 30-12-2025.csv

Used for:

* PAR30+ tracking
* NPL / write-offs
* arrears trends
* collection performance

---

### 2. Sales and Customer Data (Excel, multi-sheet)

Contains:

* DOB (Date of Birth)
* Income Level
* Gender

Used for:

* Age derivation
* Income segmentation
* demographic risk analysis

---

### 3. NPS Data (Excel)

Contains:

* NPS scores
* survey responses
* customer feedback metadata

Used for:

* customer satisfaction analysis
* linking experience vs credit performance

---

## Key Metrics

The analysis focuses on five core credit health metrics:

1. PAR30+ Rate – proportion of loans 30+ days overdue
2. NPL / Write-off Rate – loans considered unrecoverable
3. First Payment Default (FPD) – early-stage default behavior
4. Collection Rate – proportion of total due amount recovered
5. Total Arrears – absolute value of overdue balances

---

## Data Model

The project uses a star-schema style structure:

### Dimension Tables

* dim_customer: customer identity and demographics
* dim_income: income profile
* dim_product: device/product attributes

### Fact Tables

* fact_loan: loan-level information
* fact_credit_snapshot: monthly/quarterly loan status tracking
* fact_nps: customer feedback linked to credit state at time of survey

---

## Key Transformations

### 1. Customer Identity

A unified CUSTOMER_ID is required to link:

* loans
* demographics
* NPS responses

---

### 2. Age Calculation

Real age is derived from DOB:

* CUSTOMER_AGE field is loan age (NOT demographic age)
* True age is computed from DOB

---

### 3. Segmentation

Customers are grouped into:

* Age bands: 18–25, 26–35, 36–45, 46+
* Income bands based on monthly inflow

---

## Key Findings

### Portfolio Health

* PAR30+ remains high and stable (~38–39%)
* NPL rates are increasing over time
* Collection rates are slightly declining
* Arrears are growing faster than portfolio size

### High-Risk Segment

* Customers aged 18–25 show the fastest deterioration in repayment behavior
* Low-income customers (<20K KES/month) show significantly higher default rates

---

### Customer Experience vs Credit Risk

* Strong relationship between arrears and low NPS
* Major friction points:

  * incorrect phone locking
  * delayed payment reflection
  * poor support accessibility

---

## Data Quality Issues

1. CUSTOMER_AGE is mislabelled (loan age, not demographic age)
2. ~50% demographic coverage missing or unlinked
3. Redundant or inconsistent financial fields
4. NPS timing misalignment with credit snapshots

---

## Recommendations

1. Introduce unified CUSTOMER_ID across all systems
2. Standardize credit status taxonomy and transitions
3. Attach credit state at time of NPS survey

---

## Outputs

* Jupyter notebook for full analysis
* Slide deck summarizing insights
* ERD / data model diagram

---

## Author Notes

This project is designed for repeatable credit risk monitoring and scalable analytics across portfolio, customer experience, and operational decision-making.
