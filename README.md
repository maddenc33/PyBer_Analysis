# PyBer_Analysis

#### Christopher Madden

---

## Project Overview

I will be analyzing two datasets containing four months of rideshare data from PyBer, a Pyhon-based ride-sharing app company.  The following is a list of steps and deliverables for the project: 

- Import the data into a Pandas DataFrame.
- Merge the DataFrames.
- Create a bubble chart that showcases the average fare versus the total number of rides with bubble size based on the total number of drivers for each city type, including urban, suburban, and rural.
- Determine the mean, median, and mode for the following:
  - The total number of rides for each city type.
  - The average fares for each city type.
  - The total number of drivers for each city type.
- Create box-and-whisker plots that visualize each of the following to determine if there are any outliers:
  - The number of rides for each city type.
  - The fares for each city type.
  - The number of drivers for each city type.
- Create a pie chart that visualizes each of the following data for each city type:
  - The percent of total fares.
  - The percent of total rides.
  - The percent of total drivers.

---

## Resources

GitHub Repository URL:

https://github.com/maddenc33/PyBer_Analysis

### Data Sources

 - ciy_data.csv

 - ride_data.csv

### Software

 - Python 3.9.7

 - Jupyter Notebook 6.4.5

 - Anaconda 4.12.0

  >  conda version : 4.12.0
  > 
  >  conda-build version : 3.21.6
  > 
  >  python version : 3.9.7.final.0

---

## Challenge Overview

Challenge overview.

After importing the files and before merging them, I was challenged with checking the data for errors and formatting, so that I could execute the merge successfully.  Missing, malformed or incorrect data could lead to a poor or incorrect analysis, so this step is very important.
Specifically, I first verified there weren't any null values. Then I had to ensure that the data that was intuitively numbers were stored as the correct data type to perform mathematical calculations.
The following functions are particularly useful for data verification: .unique(), .sum(), .count(), .dtypes(), and .info().
In this particular case, both data sets were confirmed to be formatted correctly and not missing data.
I merged the two dataframes on the column 'city'.  The new dataframe includes all six unique columns from the two datasets.

```python

# Example code

```

---

## Analysis

The following is a summary of some of the key overall findings:

---

## Challenge Summary

Challenge summmary.