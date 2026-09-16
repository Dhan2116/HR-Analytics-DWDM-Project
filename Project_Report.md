# ❄️ Snowflake Enterprise HR Analytics & Data Recovery Platform
## Project Completion Report

**Student:** Swati Gupta  
**Date:** September 2026  
**Platform:** Snowflake

---

## 1. Abstract

This project implements a miniature enterprise HR analytics platform using Snowflake.

Instead of demonstrating Snowflake commands independently, the project connects them into a realistic data lifecycle:

**Source Data → Staging → Core Table → Data Quality → CRUD → Analytics → Incident → Time Travel → Recovery → Audit**

The project demonstrates both **analytical capability** and **data resilience**, showing how a cloud data warehouse can support business reporting while protecting historical information from accidental changes.

---

## 2. Business Problem

An organization maintains employee information across departments and locations. Management needs reliable answers to questions such as:

- How many employees are currently active?
- Which departments have the largest workforce?
- What is the average salary by department?
- Which employees fall into different salary bands?
- How has hiring changed over time?
- What happens if HR accidentally deletes an employee?
- How can incorrect salary updates be reversed?

A traditional tutorial would answer these questions separately. This project builds a connected workflow that addresses them as one data-platform problem.

---

## 3. Objectives

### Primary Objectives

1. Configure a Snowflake analytical environment.
2. Design a structured employee dataset.
3. Load and validate HR data.
4. Demonstrate CRUD operations.
5. Build reusable analytical views.
6. Generate management-level KPIs.
7. Simulate a controlled data incident.
8. Query historical data using Time Travel.
9. Recover deleted and modified records.
10. Maintain an audit trail.

---

## 4. System Architecture

```text
             HR / CSV SOURCE
                    │
                    ▼
             ┌─────────────┐
             │  HR_STAGE   │
             └──────┬──────┘
                    │
                    ▼
        ┌─────────────────────┐
        │     EMPLOYEES       │
        │     CORE TABLE      │
        └──────────┬──────────┘
                   │
          ┌────────┴────────┐
          ▼                 ▼
   DATA QUALITY        TIME TRAVEL
   VALIDATION          HISTORICAL DATA
          │                 │
          └────────┬────────┘
                   ▼
          ┌─────────────────┐
          │ ANALYTICAL      │
          │ VIEWS / KPIs    │
          └────────┬────────┘
                   ▼
          MANAGEMENT REPORTS

                   +
          ┌─────────────────┐
          │ OPERATION_AUDIT │
          └─────────────────┘
```

---

## 5. Snowflake Objects Created

| Object | Name | Purpose |
|---|---|---|
| Database | `HR_ANALYTICS_DB` | Project-level data container |
| Schema | `CORE` | Core HR data |
| Warehouse | `HR_ANALYTICS_WH` | SQL compute |
| Stage | `HR_STAGE` | Data ingestion layer |
| Table | `EMPLOYEES` | Employee master data |
| Table | `OPERATION_AUDIT` | Demonstration audit trail |
| View | `VW_DEPARTMENT_KPIS` | Department analytics |
| View | `VW_SALARY_BANDS` | Salary segmentation |
| View | `VW_EMPLOYEE_TENURE` | Tenure analytics |

---

## 6. Data Model

The central `EMPLOYEES` table contains:

- Employee ID
- Employee name
- Department
- Job title
- Salary
- Joining date
- Employment type
- Location
- Record creation timestamp

The model is intentionally simple enough for an academic project while being structured like a real HR master dataset.

---

## 7. CRUD Implementation

### Create

New employees can be inserted into the employee master table.

### Read

Employee information and management KPIs are retrieved using SELECT queries and analytical views.

### Update

Department-wide salary changes are demonstrated using conditional UPDATE operations.

### Delete

A controlled employee deletion is introduced specifically to demonstrate recovery.

The important design idea is that the deletion is not simply treated as an irreversible operation: Snowflake's historical capabilities are then used to inspect and recover the previous state.

---

## 8. Data Quality Framework

Before analytics are trusted, the project checks for:

### Duplicate Employee IDs

```sql
SELECT emp_id, COUNT(*)
FROM employees
GROUP BY emp_id
HAVING COUNT(*) > 1;
```

### Missing Critical Values

Employee name, department, salary and joining date are checked for NULL values.

### Invalid Salaries

Records with salary values less than or equal to zero are flagged.

### Department Distribution

A grouped query provides a quick structural check of the workforce.

This creates a basic data-quality gate before business analysis.

---

## 9. Analytics Layer

Three reusable views were created.

### `VW_DEPARTMENT_KPIS`

Provides:

- Headcount
- Average salary
- Minimum salary
- Maximum salary
- Total salary cost

### `VW_SALARY_BANDS`

Segments employees into:

- Entry
- Mid
- Senior
- Leadership / Specialist

### `VW_EMPLOYEE_TENURE`

Calculates:

- Tenure in months
- Tenure in years

These views allow analysts to query business metrics without rewriting the underlying transformation logic.

---

## 10. Management KPIs

The project produces the following metrics:

| KPI | Business Use |
|---|---|
| Total Headcount | Workforce size |
| Average Salary | Compensation overview |
| Department Headcount | Workforce distribution |
| Total Salary Cost | Department compensation planning |
| Salary Bands | Compensation segmentation |
| Top Salaries | Compensation review |
| Hiring by Year | Recruitment trend |
| Employees by Location | Geographic workforce distribution |

---

## 11. Time Travel Experiment

A controlled incident is simulated:

1. Finance salaries are increased by 25%.
2. Employee `104` is deleted.
3. The current state is inspected.
4. A historical snapshot is queried using Time Travel.
5. The deleted employee is recovered.
6. Historical Finance salary values are restored.
7. The final state is verified.

### Conceptual Flow

```text
ORIGINAL STATE
      │
      ▼
ACCIDENTAL UPDATE + DELETE
      │
      ▼
CURRENT / INCORRECT STATE
      │
      │  TIME TRAVEL
      ▼
HISTORICAL STATE
      │
      ▼
RECOVERY
      │
      ▼
RESTORED STATE
```

This is the central feature that turns the tutorial into a data-resilience project.

---

## 12. Audit Trail

The `OPERATION_AUDIT` table records demonstration operations such as:

- INSERT
- UPDATE
- DELETE
- Recovery-related events

Each record can contain:

- Operation ID
- Operation type
- Affected table
- Employee ID
- Timestamp
- Notes

This makes the workflow easier to inspect and explain during a project demonstration.

---

## 13. Final Validation

The project concludes with a platform health check covering:

- Final employee count
- Number of audit events
- Duplicate ID check
- Invalid salary check
- Final execution status

The goal is to finish the pipeline with explicit validation rather than simply stopping after the last SQL command.

---

## 14. Expected Demonstration

During a viva or project presentation, the following sequence can be shown:

### Step 1
Display the Snowflake environment and connection information.

### Step 2
Show the database, schema, warehouse and stage.

### Step 3
Display the employee table.

### Step 4
Run CRUD operations.

### Step 5
Show data-quality validation.

### Step 6
Open the department KPI view.

### Step 7
Show management analytics.

### Step 8
Simulate an accidental deletion and salary update.

### Step 9
Use Time Travel to retrieve the historical state.

### Step 10
Recover the affected records.

### Step 11
Display the audit log.

### Step 12
Run the final health check.

---

## 15. Advantages of the Proposed System

- Cloud-native data warehouse architecture
- Clear separation of storage and compute concepts
- Reusable analytical views
- Built-in historical data access through Time Travel
- Controlled recovery workflow
- Basic data-quality validation
- Auditability for demonstration operations
- Management-oriented KPIs
- Easy to extend with dashboards or additional HR datasets

---

## 16. Future Enhancements

The platform can be extended with:

1. Automated CSV ingestion pipelines.
2. Snowpipe for continuous ingestion.
3. Role-based access control for HR users.
4. Masking policies for sensitive employee information.
5. Row access policies.
6. Streamlit dashboards.
7. Scheduled Tasks for automated transformations.
8. dbt-based transformation workflows.
9. ML-based employee attrition analysis.
10. Department-level workforce forecasting.

---

## 17. Conclusion

The project demonstrates Snowflake as more than a SQL execution environment.

It combines **data engineering, analytics, data quality, historical querying and recovery** into one coherent workflow.

The resulting platform provides a realistic foundation for an HR analytics system and demonstrates how Snowflake can support both day-to-day reporting and recovery from accidental data changes.

---

## 18. Skills Demonstrated

**Snowflake | SQL | Data Warehousing | Data Loading | CRUD | Data Quality | Analytical Views | KPI Development | Time Travel | Data Recovery | Audit Logging | Cloud Data Platforms**
