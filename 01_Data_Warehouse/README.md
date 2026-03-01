# Data Warehouse Architecture -- Cross-Platform Implementation

This section presents a complete Data Warehouse implementation across
two environments:

-   SQL Server (classical ETL architecture)
-   Snowflake (cloud-native ELT architecture)

The objective is to demonstrate architectural portability while
preserving dimensional modeling principles.

------------------------------------------------------------------------

## Core Architecture

Both implementations follow the same layered logic:

Bronze / RAW → Silver / CLEAN → Gold / MART

This layered approach ensures: - Clear separation of concerns - Data
quality control - Business-ready star schema modeling - Reproducible
analytical foundations

------------------------------------------------------------------------

## Why Two Implementations?

This project was intentionally built twice to demonstrate:

-   Platform adaptability
-   ETL vs ELT approaches
-   On-premise vs Cloud data warehousing
-   Security & compute separation models
-   Architectural continuity across technologies

------------------------------------------------------------------------

## SQL Server Implementation

Highlights:

-   Bronze / Silver / Gold layered schemas
-   Bulk ingestion (CSV)
-   Stored procedure orchestration
-   Star schema modeling
-   Structured ETL logic

Focus: traditional Business Intelligence architecture.

Location: `SQL_Server/`

------------------------------------------------------------------------

## Snowflake Implementation

Highlights:

-   RAW / CLEAN / MART schemas
-   COPY INTO ingestion
-   Streams & Tasks (incremental logic)
-   Role-Based Access Control (RBAC)
-   Virtual Warehouses (compute isolation)
-   Time Travel recovery

Focus: modern scalable ELT cloud architecture.

Location: `Snowflake/`

------------------------------------------------------------------------

## Architectural Comparison

  -----------------------------------------------------------------------
  Concept         SQL Server                  Snowflake
  --------------- --------------------------- ---------------------------
  Ingestion       BULK INSERT                 COPY INTO

  Orchestration   Stored Procedures / Agent   Streams + Tasks

  Security        Database Roles              RBAC + Warehouses

  Recovery        Backup                      Time Travel

  Compute         Fixed Server                Elastic Warehouses
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## Business Value

This cross-platform design demonstrates the ability to:

-   Build scalable data models
-   Ensure data quality & consistency
-   Deliver decision-ready datasets
-   Maintain analytical continuity across platforms

This section reflects architectural thinking beyond dashboard-level
analytics.
