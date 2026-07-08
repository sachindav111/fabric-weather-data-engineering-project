# 🌦️ End-to-End Weather Data Engineering Project using Microsoft Fabric

> **An enterprise-grade Data Engineering solution built on Microsoft Fabric demonstrating Medallion Architecture, Incremental Data Loading, Data Quality Framework, Pipeline Orchestration, Audit Logging, and Power BI Semantic Modeling.**

---

# 📌 Project Overview

This project demonstrates a complete **end-to-end Data Engineering solution** built using **Microsoft Fabric** following industry-standard best practices.

The project ingests historical weather data from the **Open-Meteo ERA5 API**, processes it through the **Bronze → Silver → Gold Medallion Architecture**, performs data quality validations, implements incremental loading, creates dimensional models for analytics, orchestrates everything through Microsoft Fabric Pipelines, and provides complete monitoring using audit tables.

The solution is designed as an enterprise-ready architecture suitable for production environments.

---

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
├── Bronze Notebook.ipynb
├── Silver Notebook.ipynb
├── Gold Notebook.ipynb
│
├── Pipeline
│
├── SQL Scripts
│
├── Audit Tables
│
├── Sample Data
│
├── Power BI Dashboard
│
├── Images
│
│     ├── Architecture.png
│     ├── Pipeline.png
│     ├── Dashboard.png
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
