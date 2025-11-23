### COVID-19 Testing Data Analysis

This repository explores the COVID-19 time series testing data in the United States by John Hopkins University. 
## Data Source
The data is accessed via an API end point 
- `https://jhucoronavirus.azureedge.net/api/v1/testing/daily.json`  
More information and the original repository are available here  
- `https://github.com/govex/COVID-19/tree/master/data_tables/testing_data`

## Files in this repository:  
- **COVID_19_testing_data_analysis_JHU.ipynb**  
  Jupyter notebook containing the code for data import, transformation, profiling, and visualization, with a focus on New York State.
  
- **newyork_covid_testing_data.csv**  
  Testing data filtered for New York State.

- **`tests_combined_total`_NY.png**  
  Time series line chart of `tests_combined_total` vs. `date` for New York.

- **requirements.txt**  
  List of Python libraries used in the notebook.


## Overview

The goals of this analyis are to: 
* Access and understand the national testing dataset
* Export the New York only subset to a CSV
* Compute an average metric for New York
* Visualize the testing trend over time
  
All work was done in Python using the pandas, requests, and matplotlib libraries.

* Data Import and Profiling  
I used the requests library to call the API endpoint, downloaded the JSON, and converted it into a pandas DataFrame named testing_df.

To get a quick sense of the dataset and verify that it loaded correctly, I:
* Displayed the first 5 and last 5 rows (head() and tail())
* Checked the shape of the DataFrame (testing_df.shape)
* Used testing_df.info() to inspect:
** Column names and data types
** Non-null counts
** Approximate memory usage
** Used testing_df.describe() to generate summary statistics.

Data Quality and Missingness  
* To understand uniqueness and potential inconsistencies, I used testing_df.nunique():
* I also checked for duplicate rows

To analyze missing data, I calculated the percentage of null values per column for each state.

## New York State Data  

To focus on New York, I extracated the New York only data as newyork_covid_testing_data.csv
I repeated basic profiling on New york data. I then computed the simple arithmetic mean of `tests_combined_total` for New York. 

According to the data dictionary, `tests_combined_total` for New York is derived from `encounters_viral_total`, which represents the cumulative number of people tested via PCR or other approved nucleic acid amplification tests (NAAT). Because this is a cumulative measure, taking a plain average over the entire column is mathematically valid but not very intuitive as a “daily” metric. 

A more meaningful approach for understanding testing intensity would be to:  
* Compute average new tests per day over the period. 
* Compute 7-day rolling averages on these daily values.

Visualization  

To visualize testing in New York, I created a time-series line chart of `tests_combined_total` over time:
* X-axis: `date`
* Y-axis: `tests_combined_total` (cumulative number of people tested)
* I also added a horizontal reference line at the average value



