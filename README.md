# India Air Quality Analysis (2015–2020)

![India Air Quality Dashboard](Air_Quality_Dashboard__Project.png)

An end-to-end data analysis project exploring daily air quality across 26 Indian cities using Python, Pandas, and Databricks, with an interactive Power BI dashboard for visualizing trends, pollution levels, and AQI patterns.

## Data Source

The dataset comes from the Central Pollution Control Board (CPCB), India, accessed through the Kaggle dataset *Air Quality Data in India (2015–2020)*.

* **File:** `city_day.csv`
* **Original dataset size:** 29,531 rows and 16 columns
* **Period:** January 2015 to July 2020
* **Coverage:** 26 Indian cities

The raw dataset is not included in this repository.

## Tools and Technologies

* **Python** — Data processing and analysis
* **Pandas** — Data cleaning, transformation, aggregation, and analysis
* **Databricks** — Notebook-based development and execution
* **Power BI** — Interactive dashboard and data visualization
* **DAX** — Calculated tables and analytical measures in Power BI
* **GitHub** — Version control and project documentation

## Project Workflow

The project follows a three-stage data processing workflow: Bronze, Silver, and Gold. The transformations and analysis are implemented using Python and Pandas.

### 1. Bronze — Raw Data Inspection

**Notebook:** `01.bronze_python.ipynb`

* Loaded the original `city_day.csv` dataset using Pandas.
* Inspected the dataset structure, column names, data types, and missing values.
* Renamed `PM2.5` to `PM2_5` for easier column access and consistency.
* Preserved the original dataset by performing the processing on a DataFrame.

**Original dataset:** 29,531 rows.

### 2. Silver — Data Cleaning and Transformation

**Notebook:** `02_silver_python.ipynb`

The Silver stage prepares the dataset for reliable analysis.

* Converted the `Date` column to a datetime data type.
* Extracted `Year` and `Month` from the date.
* Created a `Season` column for seasonal analysis.
* Removed 1,374 rows where AQI and all pollutant measurements were missing.
* Dropped the `Xylene` column because approximately 61% of its values were missing.
* Recreated the `AQI_Bucket` column using the defined Indian AQI category ranges.
* Added an `AQI_Above_500` flag to identify readings above 500 rather than automatically deleting them.
* Preserved missing AQI values instead of replacing them with zero, which would misrepresent missing measurements as actual readings.

**Silver dataset:** 28,157 rows.

### 3. Gold — Analytical Summary Tables

**Notebook:** `03_gold_python.ipynb`

The Gold stage uses Pandas groupby and aggregation operations to generate analysis-ready summary datasets.

The main outputs are:

* **City-wise AQI summary:** Average AQI, maximum AQI, valid AQI readings, and additional statistics for readings above 500.
* **Monthly AQI trend:** Monthly average AQI, number of readings, and number of cities reporting data.
* **Pollutant summary:** City-wise average concentrations of PM2.5, PM10, NO2, SO2, CO, O3, and NH3, along with available PM2.5 and PM10 reading counts.
* **AQI category days:** Counts grouped by city, year, and AQI category.

The analysis also includes checks for readings above 500 and a separate review of Ahmedabad's AQI readings.

### 4. Export — Prepare Data for Power BI

**Notebook:** `04.Export_python.ipynb`

The export stage prepares the processed and aggregated datasets as CSV files for use in Power BI.

The main datasets used by the dashboard are:

* `aqi_silver.csv`
* `gold_city_avg_aqi.csv`
* `gold_monthly_trend.csv`
* `gold_pollutant_summary.csv`
* `gold_aqi_category_days.csv`

The exported column names and data structures should remain consistent with the versions used by the existing Power BI dashboard.

## Power BI Dashboard

The interactive dashboard presents the major findings through:

* KPI cards summarizing air quality indicators.
* Average AQI by city.
* Monthly AQI trends.
* AQI category distribution.
* Pollutant-level comparisons.
* Top 5 cities by average AQI.
* A city map showing geographic patterns.
* Key analytical insights.
* Interactive slicers for City, Year, Month, and AQI category.

The dashboard uses the processed datasets for analysis and visualization. DAX-created tables and calculations remain within Power BI.

## Key Findings

* **Ahmedabad:** The dashboard reports an average AQI of approximately 292 after excluding readings above 500 from the relevant averages.
* **Potential anomalous readings:** 412 of Ahmedabad's 1,334 AQI readings are above 500 and require careful interpretation.
* **Other highly polluted cities:** Delhi has an average AQI of approximately 252, followed by Patna at approximately 236.
* **AQI categories:** Approximately 26% of readings fall into the Poor, Very Poor, or Severe categories, while approximately 5% fall into the Good category.
* **Seasonal variation:** Winter shows the highest pollution levels, with December averaging approximately 215. July has a lower average AQI of approximately 105.
* **Pollutant levels:** PM10 and PM2.5 have the highest average measured levels among the pollutants analyzed.

These findings describe patterns in the available dataset and should be interpreted in the context of data quality and coverage.

## Limitations

* Data availability varies across cities. For example, Aizawl has only 111 days with AQI readings.
* Early 2015 has data from only two cities, making early national comparisons less representative.
* The dataset contains 543 AQI readings above 500, exceeding the standard maximum of the Indian AQI scale. These readings were flagged for investigation, and the relevant dashboard averages exclude them.
* City map coordinates were added manually and are approximate.
* The analysis identifies patterns and associations; it does not establish causal relationships.
* Pollutants have different measurement scales, so their raw concentrations should not be compared directly as equivalent measures of health risk.

## Scope and Future Improvements

The current project focuses on exploratory air quality analysis, data preparation, aggregation, and dashboard development.

Potential extensions include:

* Comparing AQI trends with public health data, where reliable and appropriate data is available.
* Conducting a dedicated analysis of air quality during the 2020 COVID-19 lockdown.
* Investigating anomalous AQI readings and differences in city-level data coverage.
* Automating the data processing and export workflow.

## Repository Structure

```text
Air-Quality-Analysis/
│
├── 01.bronze_python.ipynb
├── 02_silver_python.ipynb
├── 03_gold_python.ipynb
├── 04.Export_python.ipynb
├── Air_Quality_Dashboard__Project.png
└── README.md
```

The repository contains the Python notebooks and project documentation. The original dataset is not included.

## Conclusion

This project demonstrates an end-to-end data analysis workflow using Python and Pandas, from raw data inspection and cleaning to analytical aggregation and Power BI visualization. It highlights practical data analysis skills, including missing-value handling, feature engineering, groupby operations, data quality checks, and dashboard development.
