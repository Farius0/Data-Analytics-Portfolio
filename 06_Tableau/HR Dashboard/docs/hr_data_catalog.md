# Human Resources Dashboard -- Data Catalog

## Overview

The **Human Resources Dashboard Data Catalog** documents the single dataset used to build the HR analytics dashboard in **Tableau**.

Unlike a multi-table analytical model, this project is based on **one flat employee dataset** that combines demographic, geographic, organizational, employment, and compensation information in a single source file.

This structure enables interactive analytics for:

- workforce overview and headcount tracking
- active vs terminated employee analysis
- demographic segmentation
- department and job role exploration
- salary distribution analysis
- employee-level drilldown

---

## Dataset Structure

| Dataset Type | Dataset Name |
|-------------|--------------|
| Flat File | `hr_dataset.csv` |

---

## Data Source

| Source File | Description |
|------------|-------------|
| `hr_dataset.csv` | Employee-level HR dataset used for all dashboard views and filters |

---

# Main Dataset

## `hr_dataset`

**Business purpose**

Stores employee-level HR information used to analyze workforce composition, hiring status, demographics, location, salary, and performance in a single Tableau data source.

| Property | Value |
|----------|-------|
| Grain | One row per employee |
| Primary Key | `Employee_ID` |
| Analytical Role | Core dataset for all dashboard calculations and filters |
| Total Rows | 9,350 |

### Columns

| Column | Type | Description |
|-------|------|-------------|
| Employee_ID | String | Unique identifier of the employee |
| First Name | String | Employee first name |
| Last Name | String | Employee last name |
| Gender | String | Employee gender |
| State | String | Employee state |
| City | String | Employee city |
| Education Level | String | Highest education level attained by the employee |
| Birthdate | Date | Employee date of birth |
| Hiredate | Date | Employee hiring date |
| Termdate | Date / Null | Employee termination date when applicable; null means the employee is still active |
| Department | String | Department to which the employee belongs |
| Job Title | String | Employee job role |
| Salary | Integer | Annual salary amount |
| Performance Rating | String | Employee performance evaluation category |

---

## Data Notes

| Topic | Detail |
|------|--------|
| File format | CSV with semicolon (`;`) separator |
| Record level | Employee-level dataset |
| Active employee logic | `Termdate` is null |
| Terminated employee logic | `Termdate` is populated |
| Date coverage | Hire dates range from 2015-01-01 to 2026-03-30 |
| Salary range | 32,012 to 149,377 |

---

## Distinct Value Summary

| Attribute | Count |
|----------|------:|
| Employees | 9,350 |
| States | 8 |
| Cities | 24 |
| Departments | 7 |
| Job Titles | 28 |
| Education Levels | 4 |
| Gender Categories | 2 |
| Performance Categories | 4 |

---

## Analytical Capabilities Enabled

This dataset supports the following analytical use cases:

### Workforce Analysis

- Total employees hired
- Active vs terminated employee tracking
- Hiring and termination timeline analysis
- Workforce size by department

### Demographic Analysis

- Gender distribution
- Age group segmentation
- Education level distribution
- Demographic cross-analysis by department or location

### Organizational Analysis

- Department-level workforce structure
- Job title exploration
- Employee distribution by role

### Geographic Analysis

- Employee distribution by state and city
- HQ vs branch analysis when derived in Tableau
- Regional workforce filtering

### Compensation Analysis

- Salary distribution across job titles
- Salary by age group
- Salary by education level
- Salary comparison by gender

### Performance Analysis

- Performance rating distribution
- Education vs performance relationship
- Performance exploration by department or demographic group

### Employee-Level Exploration

- Drilldown to individual employees
- Multi-filter workforce exploration
- Salary and tenure range filtering

---

## Tableau Modeling Note

This project does **not** use a relational data model or star schema.
All visualizations are built from a **single flat dataset**, with calculated fields and dashboard interactions handled directly in Tableau.

---

## Author

**Farius Aina**  
Data Analytics & Decision Support
