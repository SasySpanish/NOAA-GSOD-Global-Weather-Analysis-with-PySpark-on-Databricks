# NOAA GSOD Global Weather Analysis with PySpark on Databricks

Exploratory and statistical analysis of global historical weather data (2000–2024) using **NOAA Global Summary of the Day (GSOD)** dataset hosted on Amazon S3.

<p>
  <img src="https://img.shields.io/badge/Python-grey?style=for-the-badge&logo=python">
  <img src="https://img.shields.io/badge/PySpark-orange?style=for-the-badge&logo=apache-spark">
  <img src="https://img.shields.io/badge/Databricks-blue?style=for-the-badge&logo=databricks">
  
</p>

## Project description

This repository contains a Databricks notebook that:

- reliably reads daily NOAA GSOD CSV files directly from public S3 (`s3a://noaa-gsod-pds/`)
- works with ~77 representative weather stations distributed across all continents
- performs data cleaning, unit conversion (°F → °C), enrichment (seasons, macro-regions, anomalies vs 2000–2010 baseline)
- computes aggregated statistics by city / year / season / continent
- identifies climate trends, heatwaves, extreme rainfall periods, temperature anomalies
- ranks locations (hottest cities, rainiest periods, most frost days, etc.)
- creates interactive visualizations (Plotly) and static plots (Seaborn heatmaps)

**Current focus**: global exploratory data analysis  
**Planned next steps**: long-term trend detection, significant anomaly flagging, continental comparisons, lightweight predictive modeling

## How to use / reproduce

1. Clone the repository

```bash
git clone https://github.com/SasySpanish/NOAA-GSOD-Global-Weather-Analysis-with-PySpark-on-Databricks.git
```
- Open Databricks (Community Edition or your organization workspace)
- Import the .ipynb notebook located in the repository
- Make sure the cluster has internet access (the NOAA S3 bucket is public – no credentials needed)
- Run the cells sequentially
- File reading is already protected with try/except to handle missing years/stations
- Final cleaned & enriched data can be saved as Delta tables (path is configurable)

## Main technologies & requirements

- Databricks cluster running Spark 3.4+ / Python 3.10+
- Internet access (to read public NOAA S3 data)
- Libraries used (installed via %pip inside the notebook when needed):
- pyspark.sql
- plotly, seaborn, matplotlib, pandas


### Data license
The NOAA GSOD dataset is public domain in the United States
.
