# Azure Data Factory ETL Pipeline

A cloud-native ETL pipeline built with Azure Data Factory that ingests raw CSV data from Azure Blob Storage, applies schema mapping and transformation logic, and loads structured records into an Azure SQL Database on a daily scheduled trigger.

---

## Tech Stack
- **Pipeline Orchestration:** Azure Data Factory (V2)
- **Cloud Storage:** Azure Blob Storage
- **Database:** Azure SQL Database
- **Data Format:** CSV → SQL Table
- **Trigger:** Daily Schedule
- **Resource Group:** adf-pipeline-rg

---

## Architecture

```
Azure Blob Storage (raw-data/superstore_sales.csv)
        ↓
ADF Copy Data Activity (schema mapping + transformation)
        ↓
Azure SQL Database (dbo.superstore_sales)
        ↓
Daily Schedule Trigger (automated runs)
```

---

## Pipeline Components

**Source:**
- Linked Service: Azure Blob Storage (`adfstoragenitish`)
- Dataset: `SourceCSV` — DelimitedText format with header row
- Container: `raw-data`
- File: `superstore_sales.csv`

**Sink:**
- Linked Service: Azure SQL Database (`adf-server-nitish`)
- Dataset: `SinkSQLDB`
- Table: `dbo.superstore_sales`
- Write behavior: Insert

**Trigger:**
- Type: Schedule
- Recurrence: Every 1 Day

---

## Database Schema

```sql
CREATE TABLE superstore_sales (
    order_id VARCHAR(20),
    customer_name VARCHAR(100),
    category VARCHAR(50),
    product_name VARCHAR(100),
    sales DECIMAL(10,2),
    quantity INT,
    discount DECIMAL(5,2),
    profit DECIMAL(10,2),
    region VARCHAR(50),
    order_date DATE
);
```

---

## Pipeline Run Results

- **Status:** Succeeded ✅
- **Records copied:** 15
- **Trigger:** Daily schedule active

> See `/images` folder for pipeline screenshots.

---

## Steps to Reproduce

1. Create an Azure Resource Group
2. Create an Azure Blob Storage account and upload source CSV to a container
3. Create an Azure SQL Database and run the schema SQL above
4. Create an Azure Data Factory instance and launch ADF Studio
5. Create linked services for both Blob Storage and SQL Database
6. Build a pipeline with a Copy Data activity connecting source to sink
7. Add a daily schedule trigger and publish
8. Monitor pipeline runs via the ADF Monitor tab

---

## Skills Demonstrated
- Cloud-native ETL pipeline design on Azure
- Azure Blob Storage data ingestion
- Azure Data Factory pipeline authoring
- Linked service configuration and firewall management
- Azure SQL Database schema design and data loading
- Scheduled pipeline automation with ADF triggers
- End-to-end cloud data movement from storage to database
