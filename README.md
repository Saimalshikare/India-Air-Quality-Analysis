# India Air Quality Analysis (2015-2020)

![India Air Quality Dashboard](Air_Quality_Dashboard__Project.png)

An end-to-end project on daily air quality in 26 Indian cities: data cleaning with PySpark in Databricks and an interactive Power BI dashboard.

## Data source
CPCB (Central Pollution Control Board, India), accessed through the Kaggle dataset "Air Quality Data in India (2015-2020)". File used: city_day.csv (29,531 rows, 16 columns, Jan 2015 to Jul 2020). The data file is not included in this repository.

## Tools
Databricks (PySpark, Delta tables), Power BI (DAX), GitHub.

## Pipeline
- **Bronze** (`01_bronze.ipynb`): raw CSV stored as a Delta table (29,531 rows). Only the column PM2.5 was renamed to PM2_5.
- **Silver** (`02_silver.ipynb`): 28,157 rows after cleaning.
  - Converted Date to a date type and added Year, Month and Season.
  - Removed 1,374 rows where AQI and every pollutant were null.
  - Dropped Xylene (61% of values missing).
  - Rebuilt AQI_Bucket from the official Indian AQI ranges.
  - Flagged 543 readings above 500 (AQI_Above_500) instead of deleting them.
  - Missing AQI was not filled with zero.
- **Gold** (`03_gold.ipynb`): summary tables for city averages, monthly trend, pollutants and AQI category days.

## Dashboard
One Power BI page with KPI cards, average AQI by city, monthly trend, AQI category split, pollutant levels, Top 5 cities, a city map, key insights, and City, Year, Month and AQI category slicers.

## Key findings
- Ahmedabad has the highest average AQI (about 292), but 412 of its 1,334 readings are above 500 and may be sensor errors.
- Delhi (252) and Patna (236) follow.
- About 26% of readings are Poor, Very Poor or Severe; about 5% are Good.
- Winter is worst (December about 215); July is cleanest (about 105).
- PM10 and PM2.5 have the highest average pollutant levels.

## Limitations
- Data coverage differs by city (Aizawl has only 111 days of AQI).
- Early 2015 has only 2 cities, so early national averages are less reliable.
- 543 AQI readings are above 500 (the AQI maximum) and may be sensor errors; averages on the dashboard exclude them.
- Map coordinates were added manually and are approximate.
- Results show relationships, not causes.
- Different pollutants are on different scales and should not be compared directly.

## Not covered
Health data (AQI vs respiratory illness) and a dedicated 2020 lockdown analysis.
