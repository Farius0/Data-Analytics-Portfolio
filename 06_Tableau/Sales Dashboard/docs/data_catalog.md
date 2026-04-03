
# Sales Dashboard -- Data Catalog

## Overview

The **Sales Dashboard Data Model** supports interactive analytics in **Tableau** for monitoring business performance across **sales, customers, products, and geography**.

The dataset follows a **star schema like analytical structure**, centered around transactional order data enriched with customer, product, and location attributes.

This model enables:

- KPI monitoring (Sales, Profit, Quantity)
- Customer behavior analysis
- Product performance tracking
- Regional performance comparisons
- Time-based trend analysis (YoY)

---

## Tables

| Table Type | Table Name |
|-----------|------------|
| Fact Table | `orders` |
| Dimension | `customers` |
| Dimension | `products` |
| Dimension | `location` |

---

## Data Sources

| Source File | Description |
|------------|-------------|
| `Orders.csv` | Transactional dataset containing order-level sales information |
| `Customers.csv` | Customer master data |
| `Products.csv` | Product hierarchy and attributes |
| `Location.csv` | Geographic mapping for regional analysis |

---

# Fact Table

## `orders`

**Business purpose**

Stores transactional sales data at the **order line level**, enabling calculation of revenue, profit, and quantity KPIs across multiple analytical dimensions.

| Property | Value |
|----------|-------|
| Grain | One row per order line |
| Primary Key | Order ID + Product ID |
| Analytical Role | Core performance measurement table |

### Columns

| Column | Type | Description |
|-------|------|-------------|
| Order ID | String | Identifier of the order |
| Order Date | Date | Date when the order was placed |
| Ship Date | Date | Shipping date |
| Ship Mode | String | Shipping method |
| Customer ID | String | Customer identifier |
| Product ID | String | Product identifier |
| Segment | String | Customer segment (Consumer, Corporate, Home Office) |
| Postal Code | String | Geographic postal code |
| Sales | Decimal | Revenue generated |
| Quantity | Integer | Number of units sold |
| Discount | Decimal | Discount applied |
| Profit | Decimal | Profit generated |

---

# Dimension Tables

## `customers`

**Business purpose**

Provides customer master data used for identification and relationship tracking in customer analytics.

| Property | Value |
|----------|-------|
| Grain | One row per customer |
| Key | Customer ID |

### Columns

| Column | Type | Description |
|-------|------|-------------|
| Customer ID | String | Unique customer identifier |
| Customer Name | String | Full customer name |

---

## `products`

**Business purpose**

Describes product hierarchy used for category and subcategory performance evaluation.

| Property | Value |
|----------|-------|
| Grain | One row per product |
| Key | Product ID |

### Columns

| Column | Type | Description |
|-------|------|-------------|
| Product ID | String | Unique identifier of the product |
| Category | String | Product category |
| Sub-Category | String | Product subcategory |
| Product Name | String | Product label |

---

## `location`

**Business purpose**

Supports geographic sales analysis across regions, states, and cities.

| Property | Value |
|----------|-------|
| Grain | One row per postal code |
| Key | Postal Code |

### Columns

| Column | Type | Description |
|-------|------|-------------|
| Postal Code | String | Postal code identifier |
| City | String | Customer city |
| State | String | Customer state |
| Region | String | Sales region |
| Country | String | Country name |

---

# Data Model Relationships

| Fact Table | Dimension | Join Key |
|-----------|-----------|----------|
| orders | customers | Customer ID |
| orders | products | Product ID |
| orders | location | Postal Code |

---

# Analytical Capabilities Enabled

This model supports the following analytical use cases:

### Sales Analysis

- Total Sales KPI tracking
- Monthly performance evolution
- Year-over-Year comparison
- Category and subcategory contribution analysis

### Profitability Analysis

- Total Profit tracking
- Profit trends over time
- Identification of loss-making subcategories

### Customer Analytics

- Total Customers KPI
- Orders per customer distribution
- Sales per customer metric
- Top customers ranking by profit

### Product Analytics

- Top products by profit
- Category-level contribution
- Subcategory performance comparison

### Geographic Analysis

- Sales by region
- State-level performance tracking
- Country filtering

---

# Author

**Farius Aina**  
Data Analytics & Decision Support
