# Sales Store Data Mart — Data Catalog

## Overview

The **Sales Store Data Mart** is the **Gold analytical layer** used to power interactive dashboards in **Qlik Sense**.

The model follows a **Star Schema architecture** centered on `fact_sales`, with descriptive dimensions for customers, products, employees, and date analysis.

## Tables

| Table Type | Table Name |
|------------|------------|
| Fact Table | `fact_sales` |
| Dimension  | `dim_customers` |
| Dimension  | `dim_products` |
| Dimension  | `dim_employees` |
| Dimension  | `dim_date` |

---

## Data Source

| Source File | Description |
|-------------|-------------|
| `store_sales.xlsx` | Raw business dataset containing orders, order details, customers, products, suppliers, employees, and offices |

---

## ETL Pipeline (Qlik Scripts)

| Script | Responsibility |
|--------|----------------|
| `01_raw_tables.qvs` | Load raw tables from the Excel source |
| `02_dimensions_tables.qvs` | Build customer, product, and employee dimensions |
| `03_fact_sales.qvs` | Build `fact_sales` from `OrderDetails` and enrich it with `OrderHeader` |
| `04_date_dimension.qvs` | Generate the calendar dimension |
| `05_drop_raw_tables.qvs` | Drop staging/raw tables after transformation |

---

## Fact Table

### `fact_sales`

**Business purpose**  
Stores transactional sales data at the **order line level** for KPI calculation and dashboard analysis.

| Property | Value |
|----------|-------|
| Source table | `OrderDetails` |
| Join enrichment | `OrderHeader` joined on `OrderID` |
| Natural identifier | `OrderID` + `ProductID` |

#### Columns

| Column | Type | Description |
|--------|------|-------------|
| `OrderID` | Integer | Order identifier from order header |
| `ProductID` | Integer | Product identifier from order detail |
| `Quantity` | Integer | Quantity sold for the order line |
| `Sales` | Decimal | Sales amount for the order line |
| `Discount` | Decimal | Discount amount or rate applied to the line |
| `COS` | Decimal | Cost of sales for the order line |
| `GP` | Decimal | Gross profit for the order line |
| `CustomerID` | Integer | Customer linked to the order |
| `EmployeeID` | Integer | Employee responsible for the order |
| `OrderDate` | Date | Order creation date |
| `DeliveryDate` | Date | Delivery date |

---

## Dimension Tables

### `dim_customers`

**Business purpose**  
Provides customer master data and geographic context for customer and regional analysis.

| Property | Value |
|----------|-------|
| Grain | One row per customer |
| Key | `CustomerID` |

#### Columns

| Column | Type | Description |
|--------|------|-------------|
| `CustomerID` | Integer | Unique customer identifier |
| `CustomerName` | String | Customer or company name |
| `ContactName` | String | Main customer contact |
| `Address` | String | Street address |
| `City` | String | Customer city |
| `Region` | String | Customer region |
| `Country` | String | Customer country |
| `PostalCode` | String | Postal code |
| `CountryCode` | String | Standardized country code |
| `Phone` | String | Phone number |
| `Fax` | String | Fax number |
| `Latitude` | Decimal | Geographic latitude |
| `Longitude` | Decimal | Geographic longitude |

---

### `dim_products`

**Business purpose**  
Provides product, category, department, and supplier attributes for product performance analysis.

| Property | Value |
|----------|-------|
| Grain | One row per product |
| Key | `ProductID` |

#### Columns

| Column | Type | Description |
|--------|------|-------------|
| `ProductID` | Integer | Unique product identifier |
| `CategoryID` | Integer | Category identifier |
| `SupplierID` | Integer | Supplier identifier |
| `ProductName` | String | Product name |
| `CategoryName` | String | Product category name |
| `Department` | String | Business department |
| `CategoryDescription` | String | Category description |
| `Supplier` | String | Supplier company name |
| `SupplierContact` | String | Supplier contact person |
| `SupplierCountry` | String | Supplier country |

---

### `dim_employees`

**Business purpose**  
Provides employee and office attributes used for sales performance and target tracking.

| Property | Value |
|----------|-------|
| Grain | One row per employee |
| Key | `EmployeeID` |

#### Columns

| Column | Type | Description |
|--------|------|-------------|
| `EmployeeID` | Integer | Unique employee identifier |
| `EmployeeName` | String | Employee full name |
| `EmployeeGender` | String | Employee gender |
| `Office` | String | Office code or office label used in source tables |
| `Extension` | String | Internal phone extension |
| `HireDate` | Date | Hiring date |
| `Supervisor` | String | Direct supervisor |
| `JobTitle` | String | Employee job title |
| `AnnualSalary` | Decimal | Annual salary |
| `SalesTarget` | Decimal | Assigned sales target |
| `SalesOffice` | String | Office descriptive label from the office table |

---

### `dim_date`

**Business purpose**  
Provides a reusable calendar dimension for time-based reporting.

| Property | Value |
|----------|-------|
| Grain | One row per date |
| Key | `OrderDate` |

#### Columns

| Column | Type | Description |
|--------|------|-------------|
| `OrderDate` | Date | Calendar date |
| `Year` | Integer | Year |
| `Quarter` | Integer | Quarter number |
| `Month` | Integer | Month number |
| `YearMonth` | String | Year-month analytical key |
| `Week` | Integer | Week number |
| `Day` | Integer | Day of month |

---

## Referential Integrity

| Fact Table | Dimension | Join Key |
|------------|-----------|----------|
| `fact_sales` | `dim_customers` | `CustomerID` |
| `fact_sales` | `dim_products` | `ProductID` |
| `fact_sales` | `dim_employees` | `EmployeeID` |
| `fact_sales` | `dim_date` | `OrderDate` |

---

## Author

**Farius Aina**  
Data Analytics & Decision Support
