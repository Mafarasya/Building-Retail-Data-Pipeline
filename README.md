# E-commerce Data Pipeline Project 
This project was creating a data pipeline for the analysis of supply and demand around the holidays, along with conducting a preliminary analysis of the data
I worked on this project from the DataCamp platform to meet the needs of a data engineering project portfolio.

![Wallmart Retail](walmartecomm.jpg)


## Project Overview
The data pipeline is designed to:
- Extract data from a PostgreSQL database and a Parquet file.
- Clean and transform the data to create a well-structured dataset for analysis.
- Aggregate the data to calculate the average weekly sales per month.
- Save the cleaned and aggregated data into CSV files.
- Validate the existence of the output files after the data pipeline is complete.

## Data Sources

1. **grocery_sales** (PostgreSQL):
   - `index`: Unique ID of the row
   - `Store_ID`: The store number
   - `Date`: The week of sales
   - `Weekly_Sales`: Weekly sales for the given store
   
2. **extra_data.parquet**:
   - `IsHoliday`: Whether the week contains a public holiday (1 if yes, 0 if no)
   - `Temperature`: Temperature on the day of sale
   - `Fuel_Price`: Cost of fuel in the region
   - `CPI`: Consumer Price Index
   - `Unemployment`: Unemployment rate
   - `MarkDown1`, `MarkDown2`, `MarkDown3`, `MarkDown4`: Number of promotional markdowns
   - `Dept`: Department number in each store
   - `Size`: Size of the store
   - `Type`: Store type, based on size

## Data Pipeline Steps

### 1. Data Extraction
- The SQL query provided for the `grocery_sales` table is executed to extract sales data.
- The `extra_data.parquet` file is loaded into a DataFrame.
- The two datasets are merged for further analysis.

### 2. Data Transformation
- The `transform()` function is implemented to clean and transform the merged dataset:
  - Missing numerical values are filled.
  - A new `Month` column is added, extracted from the `Date` column.
  - Only rows where `Weekly_Sales` are greater than $10,000 are kept.
  - Unnecessary columns are dropped.
- The resulting DataFrame is stored as `clean_data`.

### 3. Data Aggregation
- The `avg_weekly_sales_per_month()` function is implemented to calculate the average weekly sales per month:
  - Only the `Month` and `Weekly_Sales` columns are used for analysis.
  - The data is grouped by `Month`, and the average weekly sales are calculated.
  - The index is reset and the result is rounded to two decimal places.
- The aggregated DataFrame is stored as `agg_data`.

### 4. Data Loading
- The `load()` function is created to save the cleaned and aggregated DataFrames into CSV files:
  - `clean_data.csv` for the transformed dataset.
  - `agg_data.csv` for the aggregated data.
- The CSV files are saved without including the index.

### 5. Validation
- The `validation()` function checks whether `clean_data.csv` and `agg_data.csv` exist in the current working directory to ensure successful data loading.

## Conclusion

This project successfully implements a data pipeline for analyzing weekly sales data, focusing on identifying trends in average monthly sales. The pipeline includes data extraction, transformation, aggregation, loading, and validation steps to ensure accurate and structured results.



Source: https://app.datacamp.com/learn/projects/
