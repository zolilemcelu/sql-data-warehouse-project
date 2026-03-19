# SQL Data Warehouse Project
A modern Data Warehouse using SQL Server, including ETL processes, data modeling and analytics.

This project demonstrates a comprehensive data warehousing and analytics solution, from building a data warehouse to generating actionable insights. 
Designed as a portfolio project, it highlights industry best practices in data engineering and analytics.

# Datawarehouse - Medallion Architecture

A data warehouse project built on **SQL Server** using the **medallion architecture** (Bronze → Silver → Gold) to transform raw source data into business-ready analytics for Nedbank.

## Architecture Overview

```mermaid
flowchart LR
    subgraph Sources
        CRM["CRM\n(CSV)"]
        ERP["ERP\n(CSV)"]
    end

    subgraph DW["Data Warehouse · SQL Server"]
        direction LR
        subgraph Bronze["Bronze Layer"]
            B_DB[("Raw Data")]
        end
        subgraph Silver["Silver Layer"]
            S_DB[("Cleaned Data")]
        end
        subgraph Gold["Gold Layer"]
            G_DB[("Business-Ready")]
        end
    end

    subgraph Consume
        BI["BI & Reporting"]
        SQL["Ad-Hoc SQL"]
    end

    CRM --> B_DB
    ERP --> B_DB
    B_DB --> S_DB
    S_DB --> G_DB
    G_DB --> BI
    G_DB --> SQL

    style Bronze fill:#fef3c7,stroke:#d97706,color:#92400e
    style Silver fill:#f3f4f6,stroke:#9ca3af,color:#374151
    style Gold fill:#fef9c3,stroke:#ca8a04,color:#713f12
```

## Layer Details

**Bronze Layer**: Stores raw data as-is from the source systems. Data is ingested from CSV Files into SQL Server Database.
**Silver Layer**: This includes data cleansing, standardization, and normalization processes to prepare data for analysis.
**Gold Layer**: This houses business-ready data modeled into a star schema required for reporting and analytics.

### Sources
| Property | Value |
|----------|-------|
| Systems | CRM, ERP |
| Object Type | CSV Files |
| Interface | Files in Folders |

### Bronze Layer — Raw Ingestion
| Property | Value |
|----------|-------|
| Object Type | Tables |
| Load Method | Batch Processing · Full Load · Truncate & Insert |
| Transformations | None (as-is) |
| Data Model | None (as-is) |

### Silver Layer — Cleansed & Standardized
| Property | Value |
|----------|-------|
| Object Type | Tables |
| Load Method | Batch Processing · Full Load · Truncate & Insert |
| Transformations | Data Cleansing · Standardization · Normalization · Derived Columns · Enrichment |
| Data Model | None (as-is) |

### Gold Layer — Business-Ready
| Property | Value |
|----------|-------|
| Object Type | Views |
| Load Method | No Load (virtual) |
| Transformations | Data Integrations · Aggregations · Business Logics |
| Data Model | Star Schema · Flat Table · Aggregated Table |

### Consumers
| Consumer | Description |
|----------|-------------|
| BI & Reporting | Dashboards and scheduled reports |
| Ad-Hoc SQL Queries | Analyst-driven exploration |

## Tech Stack

- **Database**: SQL Server
- **ETL Pattern**: Batch Processing (Full Load, Truncate & Insert)
- **Modeling**: Star Schema, Flat Tables, Aggregated Tables
- **Consumers**: BI Tools, Ad-Hoc SQL

## Project Structure

```
├── bronze/          # Raw ingestion scripts
├── silver/          # Cleansing & standardization
├── gold/            # Business logic views
├── docs/            # Architecture diagrams
│   ├── architecture.svg
│   └── architecture.mermaid
└── README.md
```
