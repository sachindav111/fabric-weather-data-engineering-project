# 🌦️ End-to-End Weather Data Engineering Project using Microsoft Fabric

> **An enterprise-grade Data Engineering solution built on Microsoft Fabric demonstrating Medallion Architecture, Incremental Data Loading, Data Quality Framework, Pipeline Orchestration, Audit Logging, and Power BI Semantic Modeling.**

---

# 📌 Project Overview

This project demonstrates a complete **end-to-end Data Engineering solution** built using **Microsoft Fabric** following industry-standard best practices.

The project ingests historical weather data from the **Open-Meteo ERA5 API**, processes it through the **Bronze → Silver → Gold Medallion Architecture**, performs data quality validations, implements incremental loading, creates dimensional models for analytics, orchestrates everything through Microsoft Fabric Pipelines, and provides complete monitoring using audit tables.

The solution is designed as an enterprise-ready architecture suitable for production environments.

---

# 🚀 Advanced Microsoft Fabric Features

This project demonstrates enterprise-grade Microsoft Fabric capabilities beyond standard ETL development.

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

Example libraries used:

* geopy

---

# ⚡ High Concurrency

High Concurrency is enabled to improve Spark notebook execution.

Benefits

* Multiple notebooks share Spark sessions
* Reduced cluster startup time
* Lower execution latency
* Better resource utilization
* Reduced execution cost

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

---

⏰ Pipeline Scheduling

The Microsoft Fabric Data Pipeline is designed to support automated and event-driven execution, enabling reliable and production-ready data ingestion.

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

---

# 💼 Why This Project?

This project demonstrates an enterprise-grade Microsoft Fabric implementation that covers

* End-to-End ETL Pipeline
* Medallion Architecture
* Incremental Data Loading
* Data Quality Framework
* Delta Lake
* Spark Optimization
* Custom Spark Environment
* Custom Spark Pool
* High Concurrency
* OneLake
* Deployment Pipelines
* CI/CD Ready Architecture
* Audit Logging
* Monitoring
* Dimensional Modeling
* Star Schema
* Semantic Modeling
* Power BI Reporting

This repository is designed to showcase practical Microsoft Fabric Data Engineering skills expected in production environments.


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
Start

↓

Bronze Notebook

↓

Silver Notebook

↓

Gold Notebook

↓

Success / Failure Logging

↓

Pipeline Audit
```

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
