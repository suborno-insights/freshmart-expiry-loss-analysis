# Expiry Loss Diagnostics & Prevention Strategy

**A supply chain analytics case study on FreshMart, a fictional FMCG distribution company.**

> ⚠️ **Disclaimer:** FreshMart is a fictional company and **all data in this project is synthetic**. Some patterns are intentionally embedded in the data. The goal of this project is to demonstrate an analytical approach, not to report findings about a real business.

![Status](https://img.shields.io/badge/status-planning%20complete-blue)
![Data](https://img.shields.io/badge/data-synthetic-orange)

---

## Business Context

FreshMart distributes dairy, bakery, snacks, beverages, frozen, personal care, and household products through 5 warehouses. Every month, a portion of its inventory reaches its expiry date and is written off. Management does not have a clear picture of how large the loss is, where it comes from, why it happens, or how much of it could have been prevented.

## Problem Statement

FreshMart is experiencing recurring inventory expiry losses across multiple warehouses. Management lacks visibility into **where** the losses originate, **what operational factors** drive them, and **how much of the loss could have been prevented** through better inventory decisions.

## Project Goals

1. Quantify expiry-related financial loss (BDT) and identify the warehouse, category, and SKU combinations that contribute most.
2. Identify the operational factors most associated with higher expiry losses.
3. Estimate how much of the loss was **avoidable**, and recommend actions with potential savings.

## Business Questions

| # | Type | Question |
|---|------|----------|
| 1 | Primary | How much financial loss was caused by product expiry over the last 12 months, and which warehouse-category-SKU combinations contributed most? |
| 2 | Drivers | Which operational factors (excess inventory, low demand, short shelf life, long delivery lead time) are most associated with higher expiry losses? |
| 3 | Decision | How much of the loss was avoidable, which actions could reduce future losses, and what level of savings could potentially be achieved? |

## Defining "Avoidable Loss"

The rule was fixed **before** generating any data, to avoid defining it after seeing the results. The principle: *given what was known when the batch arrived, could the loss have been avoided?*

For each batch:

- **Expected sellable quantity** = average daily sales × remaining shelf life (days)
- **Avoidable quantity** = batch quantity − expected sellable quantity (floored at 0, and capped at the quantity that actually expired)
- Remaining expired quantity = **unavoidable** (e.g. sudden demand drop)

This is a starting framework. A safety buffer or uncertainty tolerance may be added later.

## Key Metrics (KPIs)

| KPI | Description |
|-----|-------------|
| Total Expiry Loss (BDT) | Cost of expired stock in a period |
| Expiry Rate (%) | Share of received quantity that expired |
| Avoidable Expiry Loss (BDT) | Loss that could have been prevented under the rule above |
| Avoidable Share (%) | Share of total loss that was avoidable |
| Inventory Coverage Days | Current stock ÷ average daily sales |
| Average Lead Time | Average days from order to delivery |
| Loss Contribution | Share of total loss by warehouse, category, and SKU |
| Potential Savings (BDT) | Estimated savings if corrective actions were applied |

## Planned Dataset

| Component | Scale |
|-----------|-------|
| Warehouses | 5 |
| Categories | 6-7 |
| SKUs | 100-120 |
| Time period | 24 months |
| Rows | 100k+ |

**How the 24 months will be used:** months 13-24 form the main analysis window; months 1-12 serve as a baseline for comparison and for understanding seasonality.

**Data generation approach:** realistic relationships will be embedded intentionally (e.g. longer lead times in one warehouse, shorter shelf life in dairy, forecast error on selected SKUs), along with noise and ambiguous cases. Some assumptions will not be supported by the analysis.

## Tools

| Purpose | Tool |
|---------|------|
| Synthetic data generation | Python (pandas, numpy, Faker) |
| Storage and querying | SQL (SQLite or PostgreSQL) |
| Cleaning and analysis | Python (Jupyter Notebook) |
| Dashboard | Power BI or Tableau |
| Version control | Git and GitHub |

## Project Roadmap

- [x] 1. Project planning and overview
- [ ] 2. Dataset design (tables and columns)
- [ ] 3. Synthetic data generation
- [ ] 4. Data loading, cleaning, and validation
- [ ] 5. Loss analysis (Question 1)
- [ ] 6. Driver analysis (Question 2)
- [ ] 7. Avoidable loss and savings estimation (Question 3)
- [ ] 8. Dashboard
- [ ] 9. Business report / presentation
- [ ] 10. Final documentation and release

## Planned Deliverables

- Synthetic dataset and data dictionary
- Analysis code (Jupyter notebooks and SQL scripts)
- Interactive dashboard
- Short business report with findings and recommendations

## Limitations and Assumptions

- The data is synthetic, so results do not apply to any real company.
- Correlation does not imply causation. For example, finding a link between lead time and expiry will not be presented as proof that lead time causes expiry.
- "Potential savings" is a scenario-based estimate, not a proven result.
- The avoidable-loss figure depends on the rule defined above. A different rule would give a different number.

## Repository Structure (planned)

```
freshmart-expiry-loss-analysis/
├── data/
│   ├── raw/
│   └── processed/
├── notebooks/
├── sql/
├── dashboard/
├── reports/
└── README.md
```

## Status

**Current phase:** planning complete; dataset design is next.
