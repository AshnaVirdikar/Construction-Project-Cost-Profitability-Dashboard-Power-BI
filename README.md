## Executive Summary

Construction projects need a clear view of contract value, billed revenue, actual costs, profitability, budget performance, schedule delays, and outstanding receivables. This Power BI portfolio project is designed to help project managers, operations teams, and finance stakeholders monitor project health and investigate cost and cash-flow risks.

The dashboard brings project cost, billing, budget, vendor, and schedule information into an interactive reporting experience. It distinguishes **Gross Project Margin** (revenue less direct costs) from **Net Project Profit** (revenue less direct and allocated indirect costs), making profitability assumptions visible to business users.

> **Data note:** All project and transaction data is simulated for demonstration purposes. It does not represent an actual construction company or live project portfolio. Currency is INR, with financial values intended to be displayed in Crore (Cr).

## Business Problem

Project stakeholders may struggle to identify cost overruns and profitability risks when budget, cost, billing, schedule, and collection data are reviewed separately.

This dashboard is designed to answer:
- Which projects are over budget or delivering weak margins?
- How do billed revenue and actual costs change over time?
- How much billed revenue has been collected, and what remains outstanding?
- How do direct costs compare with allocated overhead?
- Which projects are delayed against planned completion dates?
- How does the interpretation of project profit change between Operations and Finance?

## Dashboard Pages & Features

### 1. Executive Overview
<img width="1432" height="797" alt="image" src="https://github.com/user-attachments/assets/3c8d23cc-c913-478e-8b3b-e6027f0dfed2" />

A portfolio-level view of contract value, revenue, profit, margins, and project budget performance. Interactive filters support analysis by fiscal year, region, project type, project status, and profit definition.


### 2. Project Drill-through
<img width="1432" height="801" alt="image" src="https://github.com/user-attachments/assets/a3f63c05-4ffd-46ac-9019-03a9df28b60f" />

A project-level investigation page for examining completion, cost performance, direct versus indirect costs, vendor spend, cost/revenue trends, and outstanding receivables.

### 3. Budget, Schedule & Cash
<img width="1431" height="807" alt="image" src="https://github.com/user-attachments/assets/4140d9f3-155c-42f9-ae23-58d7ae008a55" />

A project-controls view designed to investigate cost variance, planned versus actual completion, project delays, and cash collection exposure.

### 4. Definitions & Governance
<img width="1430" height="802" alt="image" src="https://github.com/user-attachments/assets/81297698-be56-46bd-bfcf-f0497120f52a" />

A documentation-focused page explaining KPI definitions, calculation logic, source tables, business ownership, refresh assumptions, and the distinction between gross and net project profitability.

## Key KPIs

| KPI | Definition | Decision use |
|---|---|---|
| Contract Value | Total agreed contract price | Commercial baseline |
| Revenue (Billed) | Cumulative progress invoices raised | Tracks billed revenue |
| Cash Received | Cash collected against invoices | Monitors collection progress |
| Outstanding Receivables | Revenue billed minus cash received | Highlights uncollected billed revenue |
| Actual Cost | Project costs, including allocated overhead | Measures recorded expenditure |
| Direct Cost | Costs classified as direct | Supports operational cost analysis |
| Allocated Overhead | Indirect costs allocated to projects | Makes overhead impact visible |
| Gross Project Margin | Revenue minus direct cost | Operations-oriented profitability view |
| Net Project Profit | Revenue minus actual cost | Finance-oriented profitability view |
| Gross / Net Margin % | Relevant profit measure divided by revenue | Compares profitability |
| % Complete | Revenue divided by contract value | Billing-based progress proxy |
| Earned Budget | Budget multiplied by % complete | Progress-adjusted budget benchmark |
| Cost Variance | Earned budget minus actual cost | Negative values indicate potential overruns |
| Cost Performance Index (CPI) | Earned budget divided by actual cost | Values below 1 indicate cost inefficiency against the earned-budget benchmark |
| Projects Over Budget | Count of projects with CPI below 1 | Helps prioritize project review |
| Delay (Months) | Difference between planned and actual or as-of completion | Highlights schedule slippage |

**Interpretation note:** `% Complete` is calculated using billed revenue divided by contract value. It is a simplified proxy for progress, not a substitute for independently certified physical progress. Earned-budget and CPI results should be interpreted in the context of this assumption.

## Methodology

1. **Data preparation:** Load simulated project data from CSV files and set appropriate data types in Power Query.
2. **Dimensional modelling:** Organize data into a star schema with fact tables for cost transactions, billing, and project budgets, supported by project, cost category, vendor, and date dimensions.
3. **Relationship design:** Use one-to-many relationships and single-direction filtering from dimensions to facts to support consistent analysis and reduce ambiguous filter paths.
4. **DAX measures:** Create reusable measures for financial KPIs, gross and net profitability, earned budget, cost variance, CPI, receivables, and fiscal-year time intelligence.
5. **Interactive analysis:** Use slicers, project drill-through, conditional formatting, and cross-filtering to move from portfolio-level monitoring to project-level investigation.
6. **KPI governance:** Document KPI definitions, formulas, source tables, owners, and refresh assumptions so stakeholders can interpret metrics consistently.

## Technical Approach

### Data Model

The model is designed around three fact tables:
- `FactCost` — one row per cost transaction
- `FactBilling` — one row per progress invoice
- `FactBudget` — one row per project and cost category

Supporting dimensions:
- `DimProject`
- `DimCostCategory`
- `DimVendor`
- `DimDate`

The shared project dimension connects cost, billing, and budget facts. The date dimension supports time-based analysis, including fiscal-year reporting. The intended design avoids unnecessary bidirectional relationships.

## Skills Demonstrated

- **Power BI:** Interactive report design, drill-through, slicers, KPI cards, conditional formatting, report navigation
- **DAX:** `CALCULATE`, `DIVIDE`, `SWITCH`, iterator patterns, time intelligence, earned-budget calculations, dynamic metric selection
- **Data modelling:** Star schema, fact-table grain, shared dimensions, relationship direction, date dimension design
- **Business intelligence:** KPI design, profitability analysis, budget monitoring, receivables analysis, schedule reporting
- **Data governance:** KPI definitions, metric ownership, calculation transparency, refresh documentation
- **Construction / AECO analytics:** Project cost control, project profitability, budget variance, schedule delay, vendor spend, cash collection

## Results & Business Recommendations

The report is designed to help stakeholders move from retrospective reporting to targeted project investigation. Example decision workflows include:

- **Investigate cost overruns:** Prioritize projects with negative cost variance or CPI below 1, then review cost-category and vendor spend.
- **Separate operational and financial profitability:** Compare gross project margin with net project profit to understand the effect of allocated overhead.
- **Monitor cash exposure:** Review outstanding receivables alongside billed revenue and cash received, then follow up on overdue collections using the organization's actual ageing and payment terms.
- **Escalate schedule risks:** Compare planned and actual completion dates and review delays by project type or region.
- **Standardize KPI interpretation:** Use the Definitions & Governance page to align stakeholders on metric formulas, source data, ownership, and assumptions.

These are intended decision-support workflows, not claims of measured business impact from a live deployment. The dataset is simulated.

## Architecture & Future Enhancements

The current PBIX uses simulated CSV data as its source. A production-oriented version could use:

`Source systems → Microsoft Fabric Lakehouse (Bronze / Silver / Gold) → Semantic model → Power BI report → Dev / Test / Production deployment pipeline`

In a production implementation, raw data could land in a Bronze layer, be cleaned and validated in Silver, and be organized into dimensional Gold tables for the semantic model. The report could then connect to the governed model, with controlled deployment and refresh monitoring.

## Author
**Ashna Virdikar**  
Data Analyst | Power BI | DAX | SQL | Data Modelling | Business Reporting
---

*Portfolio project for learning and demonstration. All construction data is simulated; figures and insights should not be interpreted as real company performance.*
