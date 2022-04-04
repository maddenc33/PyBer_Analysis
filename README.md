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
  - numpy library
  - scipy library

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

Next, I used the scipy library to calculate summary statisics.  Here is an example of its implementation for suburban fares:

```python

mode_urban_fares = sts.mode(urban_fares)

mode_urban_drivers = sts.mode(urban_drivers)

```

To create a box-and-whisker plot for ride count data and urban fare data using object oriented programming, I first made three seperate box and whisker plots for each city type, then combined them into one graph.  Here is the syntax followed by the output:

```python

# Add all ride count box-and-whisker plots to the same graph.
x_labels = ["Urban", "Suburban","Rural"]
ride_count_data = [urban_ride_count, suburban_ride_count, rural_ride_count]
fig, ax = plt.subplots(figsize=(10, 6))
ax.set_title('Ride Count Data (2019)',fontsize=20)
ax.set_ylabel('Number of Rides',fontsize=14)
ax.set_xlabel("City Types",fontsize=14)
ax.boxplot(ride_count_data, labels=x_labels)
ax.set_yticks(np.arange(0, 45, step=3.0))
ax.grid()

```

![Ride Count Box-and-Whisker Plot](https://github.com/maddenc33/PyBer_Analysis/blob/main/analysis/Fig2.png?raw=true)

```python

# Add all fare data box-and-whisker plots to the same graph.
x_labels = ["Urban", "Suburban","Rural"]
fare_data = [urban_fares, suburban_fares, rural_fares]
fig, ax = plt.subplots(figsize=(10, 6))
ax.set_title('Ride Fare Data (2019)',fontsize=20)
ax.set_ylabel('Fare($USD)',fontsize=14)
ax.set_xlabel("City Types",fontsize=14)
ax.boxplot(fare_data, labels=x_labels)
ax.set_yticks(np.arange(0, 60, step=5.0))
ax.set_ylim(0,60)
ax.grid()

```

![Ride Fare Data Box-and-Whisker Plot](https://github.com/maddenc33/PyBer_Analysis/blob/main/analysis/Fig3.png?raw=true)

Notice how the two graphs are similar but inverted.  This is a visual demonstration of the negative correlation between the fare and ride count in a given area.

---

## Analysis

The average number of rides in rural cities tends to be 2.5-3.5x lower than urban and suburban cities, respectively.  Also, the average price of a fare is significantly higher in rural areas, 1.4x higher than in urban areas and suburban areas, respectively.
This is probably due to driver scarcity and longer distances in rural areas.  Examining the issue of driver scarcity, we can see that the driver count in rural areas is significantly lower than in urban areas.

Here are the driver counts by city for rural areas:

Bradshawfurt      7.0
Garzaport         7.0
Harringtonfort    4.0
Jessicaport       1.0
Lake Jamie        4.0

and here are driver counts by urban city:

Amandaburgh        12.0
Barajasview        26.0
Carriemouth        52.0
Christopherfurt    41.0
Deanville          49.0

Now let's look at the code and resulting output for a box-and-whisker plot of driver count data for all three city types:

```python

# Add all driver count box-and-whisker plots to the same graph.
x_labels = ["Urban", "Suburban","Rural"]
driver_data = [urban_drivers, suburban_drivers, rural_drivers]
fig, ax = plt.subplots(figsize=(10, 6))
ax.set_title('Driver Count Data (2019)',fontsize=20)
ax.set_ylabel('Number of Drivers',fontsize=14)
ax.set_xlabel("City Types",fontsize=14)
ax.boxplot(driver_data, labels=x_labels)
ax.set_yticks(np.arange(0, 80, step=5.0))
ax.set_ylim(-5,80)
ax.grid()

```

![Driver Count Data Box-and-Whisker Plot](https://github.com/maddenc33/PyBer_Analysis/blob/main/analysis/Fig4.png?raw=true)

There is a massive discrepency in driver counts between the three city types, as can be easily visualized above.

Another visualization that may be useful would be three pie charts representing percentage of total fares by city type, percentage of total rides by city type, and percentage of total drivers by city type.  The code for creating a pie chart looks like this:

```python

plt.subplots(figsize=(10, 6))
plt.pie(type_percents,
    labels=["Rural", "Suburban", "Urban"],
    colors=["gold", "lightskyblue", "lightcoral"],
    explode=[0, 0, 0.1],
    autopct='%1.1f%%',
    shadow=True, startangle=150)
plt.title("% of Total Fares by City Type")
mpl.rcParams['font.size'] = 14

```

Here are the resulting three pie charts:

![Percentage Fares by Type Pie Chart](https://github.com/maddenc33/PyBer_Analysis/blob/main/analysis/Fig5.png?raw=true)

![Percentage Fares by Type Pie Chart](https://github.com/maddenc33/PyBer_Analysis/blob/main/analysis/Fig6.png?raw=true)

![Percentage Fares by Type Pie Chart](https://github.com/maddenc33/PyBer_Analysis/blob/main/analysis/Fig7.png?raw=true)

---

## Challenge Summary

At first glance, the lower ride volume in rural areas seems to be balanced out by greater fare per ride in those areas.  The scarcity of drivers lowers the available supply, increasing price.  Conversely, in densely populated urban areas, the supply of available drivers is much higher and fares are lower.

Below is a line chart showing total fare by city type over a five month period from January 2019 to May 2019:

![Percentage Fares by Type Pie Chart](https://github.com/maddenc33/PyBer_Analysis/blob/main/analysis/Total_Fare_by_City_Type.png?raw=true)

Notice how the three data series seem to mirror one another week by week.  It seems as though demand tends to be the same in all three city types at a given time.  When demand increases in urban areas, it does so in suburban and rural areas at the same time.

Recommendations:
  - Rural fares are your high-end.  Low volume and high revenue.  Continue efforts to increase rural volume to increase profits.
  - Urban fares are your low-end.  High volume, low margin.  Suburban areas fall in the middle.
  - I would focus efforts on expanding urban markets to maximize revenue.  Although revenue per ride is lower, the sheer volume makes up for it.
  - Demand is uniform across all three city types, so there is no advantage for the rural or suburban market over the urban market.
  - I would highly recommend analyzing the elasticity of demand with regards to price for each city type.  This way you can gauge whether or not you can increase the price of fares in either of the city types and see an increase in revenue as a result.  Without knowing the elasticity of demand for rides with regards to price, we will not know whether or not we should increase prices, decrease prices, or keep prices the same.