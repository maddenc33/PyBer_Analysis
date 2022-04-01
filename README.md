# PyBer_Analysis

#### Christopher Madden

---

## Project Overview

I will be analyzing two datasets containing four months of rideshare data from PyBer, a Pyhon-based ride-sharing app company.  The following is a list of steps and deliverables for the project: 

- Import the data into a Pandas DataFrame.
- Merge the DataFrames.
- Create a scatter plot that showcases the average fare versus the total number of rides with bubble size based on the total number of drivers for each city type, including urban, suburban, and rural.
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

 - city_data.csv

 - ride_data.csv

### Software

- Python 3.9.7
  - pandas library
  - matplotlib library

- Jupyter Notebook 6.4.5

- Anaconda 4.12.0

  >  conda version : 4.12.0
  > 
  >  conda-build version : 3.21.6
  > 
  >  python version : 3.9.7.final.0

---

## Challenge Overview

After importing the files and before merging them, I was challenged with checking the data for errors and formatting, so that I could execute the merge successfully.  Missing, malformed or incorrect data could lead to a poor or incorrect analysis, so this step is very important.  Specifically, I first verified there weren't any null values. Then I had to ensure that the data that was intuitively numbers were stored as the correct data type to perform mathematical calculations.

The following functions are particularly useful for data verification: .unique(), .sum(), .count(), .dtypes(), and .info().

In this particular case, both data sets were confirmed to be formatted correctly and not missing data.
I merged the two dataframes on the column 'city'.  The new dataframe ('pyber_data_df') includes all six unique columns from the two datasets.

Next I was tasked with creating a scatter plot to visualize the data, plotting the following:
- The average fare for each type of city on the y-axis
- The total number of rides for each type of city on the x-axis
- Make the size of each marker correlate to the average number of drivers for each type of city

I needed to create additional dataframes to store the data by type ('urban_cities_df','suburban_cities_df', and 'rural_cities_df'), then I used the .groupby() and .count() functions to create a series of data that has the name of each city as the index:

```python

urban_ride_count = urban_cities_df.groupby(["city"]).count()["ride_id"]

suburban_ride_count = suburban_cities_df.groupby(["city"]).count()["ride_id"]

rural_ride_count = rural_cities_df.groupby(["city"]).count()["ride_id"]

```

I used a similar syntax for finding the average city fare for each city type, using .mean() instead of .count():

```python

urban_avg_fare = urban_cities_df.groupby(["city"]).mean()["fare"]

suburban_avg_fare = suburban_cities_df.groupby(["city"]).mean()["fare"]

rural_avg_fare = rural_cities_df.groupby(["city"]).mean()["fare"]

```

To find the average number of drivers for each city type, I used a similar syntax again:

```python

urban_driver_count = urban_cities_df.groupby(["city"]).mean()["driver_count"]

suburban_driver_count = suburban_cities_df.groupby(["city"]).mean()["driver_count"]

rural_driver_count = rural_cities_df.groupby(["city"]).mean()["driver_count"]

```

With the sums and averages calculated and stored in dataframes, I now had the data I needed to create a scatter plot.
In order to create a scatter plot containing data for each city type, I had to first create three individual scatter plots, one for each city type (urban, suburban and rural).
Here is what the three individual scatter plots look like:

![Urban Data](https://github.com/maddenc33/PyBer_Analysis/blob/main/analysis/scatterplot1.png?raw=true)

![Suburban Data](https://github.com/maddenc33/PyBer_Analysis/blob/main/analysis/scatterplot2.png?raw=true)

![Rural Data](https://github.com/maddenc33/PyBer_Analysis/blob/main/analysis/scatterplot3.png?raw=true)

To combine the three scatter plots, I called all three .scatter() functions in the same cell.  Once the three scatter plots were merged, I needed to add titles, add a grid, format the legend, and add a note.
Here is what the cell looks like:

```python

# Build the scatter charts for each city type.

plt.subplots(figsize=(10, 6))

plt.scatter(urban_ride_count,
      urban_avg_fare,
      s=10*urban_driver_count, c="coral",
      edgecolor="black", linewidths=1,
      alpha=0.8, label="Urban")

plt.scatter(suburban_ride_count,
      suburban_avg_fare,
      s=10*suburban_driver_count, c="skyblue",
      edgecolor="black", linewidths=1,
      alpha=0.8, label="Suburban")

plt.scatter(rural_ride_count,
      rural_avg_fare,
      s=10*rural_driver_count, c="gold",
      edgecolor="black", linewidths=1,
      alpha=0.8, label="Rural")

# Incorporate the other graph properties

plt.title("PyBer Ride-Sharing Data (2019)", fontsize=20)
plt.ylabel("Average Fare ($)", fontsize=12)
plt.xlabel("Total Number of Rides (Per City)", fontsize=12)
plt.grid(True)

# Add the legend.

lgnd = plt.legend(fontsize="12", mode="Expanded",
         scatterpoints=1, loc="best", title="City Types")
lgnd.legendHandles[0]._sizes = [75]
lgnd.legendHandles[1]._sizes = [75]
lgnd.legendHandles[2]._sizes = [75]
lgnd.get_title().set_fontsize(12)

# Incorporate a text label about circle size.

plt.text(42, 35, "Note: Circle size correlates with driver count per city.", fontsize="12")

# Save the figure.

plt.savefig("analysis/Fig1.png")

# Show the plot

plt.show()

```

Executing the cell creates a scatter plot 'Fig1.png' and saves it in the 'analysis' folder.  Here is the final product:

![Combined Scatter Plot](https://github.com/maddenc33/PyBer_Analysis/blob/main/analysis/Fig1.png?raw=true)

---

## Analysis

The following is a summary of some of the key overall findings:

---

## Challenge Summary

Challenge summmary.
