# delta/ – Pre-processed Global Weather Data (Delta Format)

This folder contains the final pre-processed NOAA GSOD weather dataset (2000–2024), ready for immediate analysis.

### What is inside
  
  → Delta table with all 6 continents combined  
  → Over 531,000 cleaned rows  
  → 77 selected stations (5 countries × 3 cities per continent)  
  → Key columns already cleaned and enriched:  
    - STATION, DATE, NAME, TEMP_c, MAX_c, MIN_c, PRCP, WDSP, DEWP, FRSHTT  
    - year, continent, country, season, emisfero  
    - Temperatures converted to °C, missing values handled, formats standardized

### Quick start – How to use it

1. Clone this repository:
   ```
   git clone https://github.com/SasySpanish/NOAA-GSOD-Global-Weather-Analysis-with-PySpark-on-Databricks/tree/main/data/delta.git
   cd delta
   ```
2. In a Databricks notebook (or any Spark environment), load the Delta table directly:
   ```python
   from pyspark.sql import SparkSession

   spark = SparkSession.builder.appName("WeatherAnalysis").getOrCreate()

   delta_path = "dbfs:/path/to/cloned/repo/delta/"   # adjust to your local/cloned path

   df = spark.read.format("delta").load(delta_path)

   # Quick check

   df.printSchema()
   display(df.limit(10))
   ```

You can now jump straight into aggregations, statistics, visualizations, or machine learning — no need to re-download from S3 or re-clean the data.

### Why this format?

- Delta Lake format ensures ACID transactions, schema enforcement, optimized queries and time travel
- Data is already filtered to the 77 relevant stations
- Countries and continents are correctly mapped and enriched
- Temperatures are in Celsius, seasons are assigned, extreme values are ready for feature engineering

Simply clone the repo, point to the Delta path, and start analyzing.
