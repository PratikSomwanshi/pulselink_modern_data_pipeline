# PulseLink — Metadata-Driven Data Platform on Azure & Databricks

PulseLink is an end-to-end, metadata-driven data engineering platform designed for a multi-hospital healthcare network. It ingests relational data from an internal hospital management system (**Azure SQL Database**) alongside recurring file-based feeds from external healthcare partners (CSV). The platform processes data through a **Bronze–Silver–Gold medallion architecture** using Azure Databricks and Delta Lake.

A single reusable Azure Data Factory (ADF) pipeline orchestrates ingestion based on configuration stored in SQL control tables. Every pipeline execution is automatically audited, with success and failure notifications delivered through Azure Logic Apps.

## Architecture

![PulseLink Architecture](./PulseLink%20Data%20Pipeline%20Architecture.png)

Data flows from source systems through ingestion and transformation to reporting and analytics, with orchestration, governance, security, and CI/CD integrated across the platform.

### Core Components

- **Ingestion:** Azure Data Factory orchestrates metadata-driven ingestion from Azure SQL Database and external CSV feeds stored in Azure Data Lake Storage Gen2.
- **Transformation:** Azure Databricks, PySpark, and Delta Lake transform data across Bronze, Silver, and Gold layers.
- **Orchestration:** Azure Data Factory pipelines use Azure SQL Database control tables to manage ingestion configurations, watermarks, and execution audits.
- **Governance & Security:** Unity Catalog manages data governance and access control, while Azure Key Vault and managed identities support secure resource access. Azure Logic Apps handles automated email notifications.
- **CI/CD:** GitHub-based workflows manage version control and deployment for Azure Data Factory and Databricks development.
- **Consumption:** Databricks AI/BI Dashboards and Power BI provide reporting and analytics on curated Gold-layer datasets.

## Key Features

### 1. Metadata-Driven Ingestion
A single reusable Azure Data Factory pipeline ingests data from multiple sources based on configuration records stored in an Azure SQL Database control table. Adding a new table or source requires updating metadata rather than developing a separate pipeline.

### 2. Full and Incremental Loads
The platform supports multiple ingestion strategies through reusable pipelines and notebooks:

- **Full load:** Reloads the complete source dataset.
- **Append load:** Adds new records without replacing existing data.
- **Incremental merge:** Uses watermark-based extraction and Delta Lake merge operations to process new and updated records.

### 3. Bronze–Silver–Gold Medallion Architecture
Data is progressively transformed into three layers using Databricks and Delta Lake:

- **Bronze:** Stores raw ingested data while preserving source information.
- **Silver:** Applies data cleansing, standardization, validation, and deduplication.
- **Gold:** Contains curated, business-ready datasets optimized for reporting and analytics.

A calendar dimension table supports time-based analysis and reporting.

### 4. Automated Auditing and Alerting
Pipeline executions and processing stages are recorded in centralized audit tables. Azure Logic Apps sends automated status emails for successful and failed executions, including a dynamically generated email subject and an HTML table summarizing execution results.

### 5. Governed and Secure Data Access
The platform uses Unity Catalog for data governance and access management, together with Azure managed identities and Azure Key Vault for secure access to supported Azure resources. Credentials and secrets are not hardcoded into pipeline definitions or notebooks.

### 6. CI/CD and Version Control
GitHub supports version control and collaborative development across both Azure Data Factory and Databricks. Feature branches, pull requests, and deployment workflows help maintain consistent and controlled releases.

### 7. Reporting and Analytics
The Gold layer serves as the common data foundation for:

- **Databricks AI/BI Dashboards:** Interactive dashboards built on curated Gold-layer tables.
- **Power BI:** Business intelligence reports and visualizations for healthcare operations, data quality, and performance metrics.

Both reporting tools consume the same curated datasets to maintain consistent business definitions and reporting logic.

## Tech Stack

**Cloud & Storage:** Microsoft Azure, Azure Data Lake Storage Gen2

**Ingestion & Orchestration:** Azure Data Factory, Azure SQL Database

**Data Engineering:** Azure Databricks, PySpark, Delta Lake

**Governance & Security:** Unity Catalog, Azure Key Vault, Azure Managed Identities

**Automation & Monitoring:** Azure Logic Apps, SQL-based audit logging

**Reporting & Analytics:** Databricks AI/BI Dashboards, Power BI

**Source Data:** Azure SQL Database, CSV files

**Version Control & CI/CD:** Git, GitHub

## Project Goals

PulseLink demonstrates how to build a reusable, scalable, and secure data engineering platform that reduces pipeline duplication through metadata-driven ingestion, standardizes data processing through a medallion architecture, and improves operational reliability through automated auditing and notifications.

The project showcases practical data engineering concepts including incremental ingestion, watermark management, Delta Lake transformations, data quality validation, centralized metadata management, governance, CI/CD, and analytics-ready data modeling.
