# 🌦️ End-to-End Weather Data Engineering Project using Microsoft Fabric

> **An enterprise-grade Data Engineering solution built on Microsoft Fabric demonstrating Medallion Architecture, Incremental Data Loading, Data Quality Framework, Pipeline Orchestration, Audit Logging, and Power BI Semantic Modeling.**

---

# 📌 Project Overview

This project demonstrates a complete **end-to-end Data Engineering solution** built using **Microsoft Fabric** following industry-standard best practices.

The project ingests historical weather data from the **Open-Meteo ERA5 API**, processes it through the **Bronze → Silver → Gold Medallion Architecture**, performs data quality validations, implements incremental loading, creates dimensional models for analytics, orchestrates everything through Microsoft Fabric Pipelines, and provides complete monitoring using audit tables.

The solution is designed as an enterprise-ready architecture suitable for production environments.

---

# 🚀 Advanced Microsoft Fabric Features

This project demonstrates enterprise-grade Microsoft Fabric capabilities in standard ETL development.

---

# 🔥 Custom Spark Pool

The notebooks execute on a dedicated **Custom Spark Pool** rather than the default runtime.

Benefits:

* Faster notebook startup
* Better workload isolation
* Improved Spark performance
* Optimized resource utilization
* Enterprise scalability
  
![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/d9383c6eb57b915e45cd76877fa5753dcc5cb828/Pipeline/Custom%20Pool.png)
---

# ⚙️ Custom Spark Environment

A dedicated **Custom Spark Environment** is used to provide a consistent runtime across all notebooks.

### Features

* Centralized Python package management
* Consistent runtime across Development, Test, and Production
* Reusable notebook environment
* Simplified dependency management
* Enterprise-ready package governance
* 
  ![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/1004b82285915affdc5f4808b073c40a0e1a8a86/Workspace_Specifications/Custom%20Environment.png)
Example libraries used:

* geopy

![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/7c3e271adf871f6aa53b8bf10ee75c698e49fad8/Workspace_Specifications/Custom%20Library%20for%20Environment.png)
---

# ⚡ High Concurrency

High Concurrency is enabled to improve Spark notebook execution.

Benefits

* Multiple notebooks share Spark sessions
* Reduced cluster startup time
* Lower execution latency
* Better resource utilization
* Reduced execution cost

![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/7c3e271adf871f6aa53b8bf10ee75c698e49fad8/Workspace_Specifications/High%20Concurrency%20for%20pipeline.png)
---

# 🎯 Pipeline Parameters

The Microsoft Fabric Pipeline is fully parameterized for reusable deployments.

Parameters include

| Parameter     | Description                |
| ------------- | -------------------------- |
| Latitude      | Weather location latitude  |
| Longitude     | Weather location longitude |
| StartDate     | API extraction start date  |
| EndDate       | API extraction end date    |
| PipelineRunID | Audit tracking             |

This enables the same notebooks to execute for multiple locations without modifying code.

![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/7c3e271adf871f6aa53b8bf10ee75c698e49fad8/Pipeline/Pipeline%20Base%20Parameter%20specifications.png)

---

⏰ Pipeline Scheduling

The Microsoft Fabric Data Pipeline is designed to support automated and event-driven execution, enabling reliable and production-ready data ingestion.
if the sheduling is failed Email notification alerts also available.

![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/01488f2fb1361d4c3b9765911385b4aae6544c44/Pipeline/Pipeline%20Shedule.png)

---

# 🚀 Deployment Pipeline (CI/CD)

The solution supports Microsoft Fabric Deployment Pipelines.

Deployment Flow

```
Development

↓

Testing

↓

Production
```

![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/01488f2fb1361d4c3b9765911385b4aae6544c44/Workspace_Specifications/Deployment%20Pipeline.png)

Artifacts promoted through Deployment Pipeline

* Lakehouse
* Warehouse
* Spark Notebooks
* Data Factory Pipelines
* Semantic Model
* Power BI Reports

Environment-specific settings are controlled using Pipeline Parameters.

---

# ⚡ Performance Optimization

Several optimization techniques have been implemented.

✔ Incremental Loading

✔ Watermark Processing

✔ Delta Lake Storage

✔ Delta MERGE Operations

✔ Business Key Deduplication

✔ Schema Evolution

✔ Reverse Geocoder Optimization

✔ Spark Caching

✔ High Concurrency

✔ Custom Spark Pool

✔ Delta Lake Optimized Storage

---

# 📊 Monitoring Hub

Microsoft Fabric Monitoring Hub can be used to monitor

* Notebook executions
* Pipeline executions
* Spark job history
* Failed activities
* Execution duration
* Compute utilization
* Workspace activity

  ![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/b81093af893573b4fabda41fe9b9637537c8136a/Workspace_Specifications/Moniter.png)

---

# 🛡️ Enterprise Error Handling & First-Run Support

The solution is designed following production-grade coding standards to ensure reliable execution, robust error handling, and seamless deployment.

## Exception Handling

All Bronze, Silver, and Gold notebooks implement a structured exception handling framework using Python's `try`, `except`, and `finally` blocks.

This approach ensures that:

* ETL failures are captured with meaningful error messages.
* Notebook execution status is always recorded.
* Audit tables are updated regardless of success or failure.
* Pipeline monitoring remains accurate.
* Unexpected runtime exceptions do not leave the audit process incomplete.

## Notebook Auditing

Every notebook execution automatically records:

* Notebook Name
* Pipeline Run ID
* Execution Status (Success/Failed)
* Records Processed
* Start Time
* End Time
* Execution Duration
* Error Message (if any)
* Audit Timestamp

This provides complete execution traceability for monitoring and troubleshooting.

## First-Run Handling

To support initial deployment and avoid runtime failures, the project includes first-run validation using conditional checks before reading or writing data.

Examples include:

* Creating schemas only if they do not already exist.
* Creating Delta tables during the initial execution.
* Checking for existing dimension and fact tables before performing incremental processing.

This ensures that the same notebooks can be executed repeatedly without requiring manual setup or code changes.

## Production Reliability

The project follows several defensive programming practices:

* `CREATE SCHEMA IF NOT EXISTS`
* `spark.catalog.tableExists()` validation
* Incremental watermark processing
* Delta MERGE operations
* Safe append and overwrite strategies
* Schema evolution support (`mergeSchema`)
* Centralized audit logging
* End-to-end exception handling

These practices make the solution suitable for enterprise-scale Microsoft Fabric implementations and simplify deployment across Development, Test, and Production environments.


# 🏗️ Medallion Architecture

## Bronze Layer

### Purpose

Store raw API data without business transformations.

### Operations

* API Data Extraction
* Schema Drift Handling
* Metadata Addition
* Delta Storage
* Incremental Raw Load
* API Audit
* Notebook Audit

### Output Table

```
bronze.weather_data
```

---

## Silver Layer

### Purpose

Clean and standardize raw data.

### Transformations

✔ Incremental Load

✔ Datetime Conversion

✔ Data Type Casting

✔ Null Handling

✔ Data Quality Validation

✔ Duplicate Removal

✔ Reverse Geocoding

✔ Timezone Conversion (UTC → IST)

✔ Metadata Handling

✔ Data Quality Audit

✔ Notebook Audit

### Output Tables

```
silver.weather_selected

silver.weather_rejected
```

---

## Gold Layer

### Purpose

Business-ready analytical model.

### Dimension Tables

```
gold.dim_date

gold.dim_time

gold.dim_location
```

### Fact Table

```
gold.fact_weather
```

### Summary Tables

```
gold.daily_summary

gold.monthly_summary

gold.hourly_summary
```

---

# 🔄 Incremental Loading Strategy

This project avoids reprocessing historical records by using **Watermark Incremental Loading**.

## Bronze

Loads new API data.

## Silver

Reads only records newer than the maximum `ingestion_time` already processed.

```
MAX(ingestion_time)
```

## Gold

Reads only newly processed Silver records using MAX(ingestion_time)

Benefits

* Faster execution
* Lower compute cost
* Production-ready
* Scalable

---

# ✅ Data Quality Framework

The Silver layer includes a complete QC framework.

## Validation Rules

### Mandatory Fields

* Datetime
* Temperature

Rows missing mandatory values are rejected.

---

### Duplicate Detection

Duplicates removed using business columns.

Metadata columns excluded.

---

### Null Handling

Business rules applied before loading.

---

### QC Results

Each record receives:

```
Passed

Rejected
```

---

# 🌍 Reverse Geocoding

Latitude and Longitude are converted into:

* City
* State
* Country

Using

```
Nominatim Reverse Geocoder
```

Distinct coordinates are geocoded only once for better performance.

---

# ⏰ Timezone Conversion

Weather API returns UTC.

Project converts timestamps into

```
Asia/Kolkata
```

using

```
from_utc_timestamp()
```

---

# 📊 Analytical Models

## Daily Summary

Includes

* Average Temperature
* Maximum Temperature
* Minimum Temperature
* Record Count
* Previous Day Temperature
* Temperature Difference
* Heat Wave Classification
* Temperature Bands

---

## Monthly Summary

Includes

* Monthly Average
* Monthly Maximum
* Monthly Minimum
* Month-over-Month Temperature Change

---

## Hourly Summary

Includes

* Hourly Average
* Hourly Maximum
* Hourly Minimum
* Hour-over-Hour Change

---

# ⭐ Star Schema

```
                Dim_Date
                   │
                   │
Dim_Time ─── Fact_Weather ─── Dim_Location
```

![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/b81093af893573b4fabda41fe9b9637537c8136a/Power_BI_Dashboard/Star%20Schema%20for%20weather_data.png)

Fact Table

```
fact_weather
```

Dimensions

```
dim_date

dim_time

dim_location
```

---

# 📋 Audit Framework

The project implements enterprise-grade auditing.

## Notebook Audit

Tracks

* Notebook Name
* Status
* Records Processed
* Start Time
* End Time
* Duration
* Error Message

Table

```
audit.notebook_audit
```

---

## Data Quality Audit

Tracks

* Total Records
* Good Records
* Bad Records
* Duplicate Records
* Quality Score

Table

```
audit.data_qc_table
```

---

## Incremental Load Audit

Tracks

* Previous Watermark
* Current Watermark
* Rows Inserted
* Rows Updated

Table

```
audit.incremental_load_audit
```

---

## Pipeline Audit

Tracks

* Pipeline Name
* Trigger Type
* Status
* Duration
* Error Message

Table

```
audit.pipeline_audit
```

---

# 🔄 Pipeline Orchestration

Microsoft Fabric Pipeline orchestrates the complete ETL.

Pipeline Flow

```

                                        ┌───────────────────────────────┐
                                        │  Schedule / Manual Trigger    │
                                        └───────────────┬───────────────┘
                                                        │
                                                        ▼
                  ┌────────────────────────────────────────────────────────────┐
                  │    Data Flow Orchestration Pipeline (Master pipeline)      │
                  │────────────────────────────────────────────────────────────│
                  │ • Pipeline Parameters                                      │
                  │ • Invoke Medallion ETL Pipeline                            │
                  │ • Pipeline Audit Logging                                   │
                  │ • Error Handling                                           │
                  └──────────────────────┬─────────────────────────────────────┘
                                         │
                                         ▼
  ┌─────────────────────────────────────────────────────────────────┐
  │                         Invoke Pipeline                         │
  │─────────────────────────────────────────────────────────────────│
  │                                                                 │
  │  Bronze Notebook                                                │
  │  • Incremental Data Load                                        │
  │  • Metadata Capture                                             │
  │  • API Audit Logging                                            │
  │                                                                 │
  │                                    ↓                            │
  │                                                                 │
  │  Silver Notebook                                                │
  │  • Schema Validation                                            │
  │  • Null Handling                                                │
  │  • Duplicate Removal                                            │
  │  • Data Quality Validation                                      │
  │  • QC Audit Logging                                             │
  │  • Notebook Audit Logging                                       │
  │                                                                 │
  │                                    ↓                            │
  │                                                                 │
  │  Gold Notebook                                                  │
  │  • Star Schema Creation                                         │
  │  • Dimension & Fact Tables                                      │
  │  • Summary Tables                                               │
  │  • Incremental Watermark Load                                   │
  │  • Incremental Audit Logging                                    │
  │  • Notebook Audit Logging                                       │
  │                                                                 │
  │─────────────────────────────────────────────────────────────────│
  │ Common Features                                                 │
  │ ✔ Try / Except / Finally in every notebook                      │
  │ ✔ First Run Handling using IF conditions                        │
  │ ✔ Incremental Loading                                           │
  │ ✔ Audit Framework                                               │
  │ ✔ Modular Notebook Design                                       │
  └─────────────────────────────┬────────────────────────────────────┘
                ┌───────────────┴────────────────┐
                │                                │
                ▼                                ▼
      ┌────────────────────┐          ┌────────────────────┐
      │ Pipeline Success   │          │ Pipeline Failure   │
      │ Audit Logging      │          │ Audit Logging      │
      └─────────┬──────────┘          └─────────┬──────────┘
                │                               │
                │                               ▼
                │                  ┌─────────────────────────┐
                │                  │ Office 365 Email Alert  │
                │                  └─────────────────────────┘
                │
                ▼
      ┌──────────────────────────────┐
      │ Lakehouse Maintenance        │
      │ • V-Order                    │
      │ • Vacuum                     │
      └──────────────────┬───────────┘
                         │
                         ▼
      ┌───────────────────────────────────────┐
      │    Refresh Business Semantic Model    │
      └──────────────────┬────────────────────┘
                         │
                         ▼
                ┌───────────────────┐
                │ Wait (60 Seconds) │
                └─────────┬─────────┘
                          │
                          ▼
      ┌───────────────────────────────────────────┐
      │     Refresh Audit Semantic Model          │
      └──────────────────┬────────────────────────┘
                         │
                         ▼
                   ┌─────────────┐
                   │    Finish   │
                   └─────────────┘
```
# Data_Flow_Medallion_Pipeline (Invoke Pipeline)
![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/d6307152e5f4848055acdf00cf1fd94fa3fce6d6/Pipeline/Data_Flow_Medallion_Pipeline.png)

# Data_Flow_Orchestration_Pipeline 
![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/d6307152e5f4848055acdf00cf1fd94fa3fce6d6/Pipeline/Data_Flow_Orchestration_Pipeline.png)

Pipeline handles

* Sequential Execution
* Dependency Management
* Retry Policie
* Failure Handling
* Monitoring

---

# ⚡ Microsoft Fabric Features Highlighted

This project showcases several Microsoft Fabric capabilities:

* Lakehouse Architecture
* Warehouse Integration
* Fabric Data Factory Pipelines
* Spark Notebooks
* Delta Lake Storage
* Medallion Architecture
* Incremental Data Loading
* Custom Spark Environment
* Custom Spark Pools
* High Concurrency Execution
* Delta Merge Operations
* Schema Evolution
* OneLake Integration
* Semantic Model
* Power BI Integration
* Fabric Monitoring
* Audit Framework
* Notebook Orchestration

---

# 📈 Power BI Dashboard

The Semantic Model can be connected directly to Power BI.

Possible visuals include:

* Daily Temperature Trend
* Monthly Trend
* Hourly Heatmap
* Temperature Distribution
* Heat Wave Analysis
* Weather Condition Analysis
* Data Quality Score
* Pipeline Execution Status
* Notebook Execution Time
* Incremental Load Statistics

![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/48347bb6b1e53cb48dd341c7c2b4942cde0de072/Power_BI_Dashboard/Audit%20Overview%20from%20audit%20dashboard.png)


![image alt](https://github.com/sachindav111/fabric-weather-data-engineering-project/blob/48347bb6b1e53cb48dd341c7c2b4942cde0de072/Power_BI_Dashboard/Notebook%20Audit%20from%20audit%20Dashboard.png)

---

# 📁 Repository Structure

```
fabric-weather-data-engineering-project

│
├── incremental copy notebook.ipynb
├── silver layer notebook.ipynb
├── Gold layer notebook.ipynb
│
├── Pipeline
│
├── SQL_Scripts
│
├── Workspace_Specifications
│
├── Power_BI_Dashboard
│
└── README.md
```

---

# 📊 Skills Demonstrated

This project demonstrates practical experience in:

* Microsoft Fabric
* Data Engineering
* ETL Development
* Spark
* PySpark
* Delta Lake
* SQL
* Incremental Loading
* Medallion Architecture
* Data Modeling
* Data Quality Framework
* Audit Logging
* Pipeline Orchestration
* Semantic Modeling
* Power BI
* Warehouse Design
* Star Schema
* Performance Optimization

---

# 👨‍💻 Author

**Sachin - [sachindev111@outlook.com](mailto:sachindev111@outlook.com)**

**Data Engineer | Microsoft Fabric | Azure | PySpark | SQL | Power BI**

This project demonstrates an enterprise-level Microsoft Fabric implementation covering ingestion, transformation, data quality, dimensional modeling, orchestration, auditing, and analytics, following modern data engineering best practices.
