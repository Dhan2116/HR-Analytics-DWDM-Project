# ❄️ Snowflake Enterprise HR Analytics & Data Recovery Platform

## Project Overview

This project transforms a basic Snowflake tutorial into a **mini enterprise data-platform project**.

The system demonstrates how an organization can use Snowflake to:

- Build a cloud data warehouse environment
- Create databases, schemas, warehouses, tables and stages
- Load and validate employee data
- Perform CRUD operations safely
- Create analytical views and KPI queries
- Demonstrate data-quality checks
- Use Snowflake Time Travel for point-in-time analysis
- Recover accidentally deleted or modified records
- Maintain an audit trail
- Produce management-ready HR analytics

### Business Scenario

A growing organization wants a centralized HR analytics platform to understand:

- Headcount by department
- Salary distribution
- Hiring trends
- Average compensation
- Employee tenure
- Department-level workforce metrics

At the same time, the HR team needs a reliable way to recover data after accidental updates or deletions.

This project models that complete workflow in Snowflake.

---

## Architecture

```text
                    ┌──────────────────────────┐
                    │       HR Source Data     │
                    │ CSV / Manual / SnowSQL    │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │     Snowflake STAGE      │
                    │        hr_stage          │
                    └────────────┬─────────────┘
                                 │
                                 ▼
             ┌────────────────────────────────────────┐
             │          RAW / CORE HR TABLE            │
             │              employees                  │
             └───────────────┬────────────────────────┘
                             │
                 ┌───────────┴──────────────┐
                 ▼                          ▼
       ┌──────────────────┐       ┌──────────────────┐
       │ Data Quality      │       │ Time Travel      │
       │ Validation        │       │ Recovery Layer   │
       └─────────┬────────┘       └────────┬─────────┘
                 │                         │
                 └────────────┬────────────┘
                              ▼
                    ┌──────────────────────┐
                    │ Analytical Views     │
                    │ HR KPIs & Insights   │
                    └──────────┬───────────┘
                               ▼
                    ┌──────────────────────┐
                    │ Management Reporting │
                    └──────────────────────┘
```

---

## Technology Stack

| Technology | Purpose |
|---|---|
| Snowflake | Cloud data warehouse |
| SnowSQL / SQL | Data definition and manipulation |
| Time Travel | Historical querying and recovery |
| Stages | Data ingestion layer |
| Views | Reusable analytics |
| SQL | KPI and business analysis |

---

## Project Structure

```text
snowflake-enterprise-hr-analytics-project/
├── README.md
├── sql/
│   └── Enterprise_HR_Analytics.sql
├── data/
│   └── employees_sample.csv
└── reports/
    └── Project_Report.md
```

## How to Run

1. Log into Snowflake.
2. Open `sql/Enterprise_HR_Analytics.sql`.
3. Execute the script sequentially.
4. Use the validation queries after each major section.
5. For the Time Travel demonstration, execute the marked steps in order.
6. Review the analytical views at the end.

> **Important:** Time Travel recovery depends on the retention available in your Snowflake account. The demo uses a short-offset workflow so it can be tested immediately after making the controlled changes.

---

## Key Deliverables

### 1. Snowflake Environment
Database, schema, warehouse and stage.

### 2. HR Data Model
Employee master data with department, compensation and joining information.

### 3. Data Operations
INSERT, UPDATE and DELETE workflows.

### 4. Data Quality
Duplicate ID, null and invalid salary checks.

### 5. Analytics
Department headcount, average salary, salary bands and tenure analysis.

### 6. Data Resilience
Time Travel snapshots and controlled record recovery.

### 7. Auditability
An operation log records important changes made during the demonstration.

---

## Learning Outcomes

After completing this project, a student should be able to explain:

- Snowflake's logical data objects
- Separation of storage and compute
- How warehouses execute SQL workloads
- How staged data enters a warehouse
- Difference between transactional operations and analytical queries
- How Time Travel supports historical analysis
- How deleted data can be recovered
- Why data-quality checks are important in analytics systems
- How reusable SQL views support reporting

---

## Author

**Student:** Swati Gupta  
**Date:** September 2026  
**Platform:** Snowflake
