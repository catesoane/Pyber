

```python
# Import Dependencies
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
```


```python
# Import/Read in Files
city_data = "city_data.csv"
ride_data = "ride_data.csv"
```


```python
# City DataFrame
city_data_df = pd.read_csv(city_data)
city_data_df.head()

# Drop Dupilcates
city_data_df = city_data_df.drop_duplicates('city')
city_data_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Ride DataFrame
ride_data_df = pd.read_csv(ride_data)
ride_data_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge DataFrames
pyber_data = pd.merge(city_data_df, ride_data_df, on="city")
pyber_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-19 04:27:52</td>
      <td>5.51</td>
      <td>6246006544795</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-04-17 06:59:50</td>
      <td>5.54</td>
      <td>7466473222333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-05-04 15:06:07</td>
      <td>30.54</td>
      <td>2140501382736</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-01-25 20:44:56</td>
      <td>12.08</td>
      <td>1896987891309</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-09 18:19:47</td>
      <td>17.91</td>
      <td>8784212854829</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Calculate Average Fare Per City
average_fare = pyber_data.groupby("city")["fare"].mean()
average_fare.head()
```




    city
    Alvarezhaven    23.928710
    Alyssaberg      20.609615
    Anitamouth      37.315556
    Antoniomouth    23.625000
    Aprilchester    21.981579
    Name: fare, dtype: float64




```python
# Total Number of Rides Per City
total_rides = pyber_data.groupby("city")["ride_id"].count()
total_rides.head()
```




    city
    Alvarezhaven    31
    Alyssaberg      26
    Anitamouth       9
    Antoniomouth    22
    Aprilchester    19
    Name: ride_id, dtype: int64




```python
# Total Number of Drivers Per City
total_drivers = pyber_data.groupby("city")["driver_count"].mean()
total_drivers.head()
```




    city
    Alvarezhaven    21
    Alyssaberg      67
    Anitamouth      16
    Antoniomouth    21
    Aprilchester    49
    Name: driver_count, dtype: int64




```python
# City Type Count (Urban, Suburban, Rural)
city_type = city_data_df.set_index("city")["type"]
city_type.value_counts()
```




    Urban       66
    Suburban    41
    Rural       18
    Name: type, dtype: int64




```python
# New DataFrame
pyber_df = pd.DataFrame({"Average Fare": average_fare,
                        "Number of Rides": total_rides,
                        "Number of Drivers": total_drivers,
                        "City Type": city_type})
pyber_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Fare</th>
      <th>City Type</th>
      <th>Number of Drivers</th>
      <th>Number of Rides</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>23.928710</td>
      <td>Urban</td>
      <td>21</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>20.609615</td>
      <td>Urban</td>
      <td>67</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>37.315556</td>
      <td>Suburban</td>
      <td>16</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>23.625000</td>
      <td>Urban</td>
      <td>21</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>21.981579</td>
      <td>Urban</td>
      <td>49</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Locating Each City
urban = pyber_df.loc[pyber_df["City Type"] == "Urban"]
suburban = pyber_df.loc[pyber_df["City Type"] == "Suburban"]
rural = pyber_df.loc[pyber_df["City Type"] == "Rural"]
```


```python
# Create Bubble Plot of Ride Share Data
plt.scatter(urban["Number of Rides"], 
            urban["Average Fare"], 
            color = "gold", 
            edgecolors="black", 
            s = urban["Number of Drivers"]*10, 
            label = "Urban", 
            alpha = 0.5, 
            linewidth = 1)
plt.scatter(suburban["Number of Rides"],
            suburban["Average Fare"], 
            color = "lightskyblue", 
            edgecolors="black", 
            s = suburban["Number of Drivers"]*10, 
            label = "Suburban", 
            alpha = 0.5, 
            linewidth = 1)
plt.scatter(rural["Number of Rides"],
            rural["Average Fare"], 
            color = "lightcoral", 
            edgecolors="black", 
            s = rural["Number of Drivers"]*10, 
            label = "Rural", 
            alpha = 0.5, 
            linewidth = 1)

# Graph Formatting
plt.title("Pyber Ride Sharing Data")
plt.xlabel("Total Number of Rides (Per City)")
plt.ylabel("Average Fare ($)")
plt.legend(loc="best")
plt.text(37, 45,"Note: Circle size correlates with driver count per city.")
plt.show()

```


![png](Pyber_files/Pyber_11_0.png)



```python
# Percentage of Total Fares by City Type
city_fares = pyber_data.groupby(["type"])["fare"].sum()

# Create Pie Chart
plt.pie(city_fares, 
        labels = city_fares.index, 
        autopct = "%1.2f%%", 
        colors = ["gold", "lightskyblue", "lightcoral"], 
        explode = (0,0,.1), 
        shadow = True, 
        startangle = 125)
plt.axis("equal")
plt.title("% of Total Fares by City Type")
plt.legend(loc= "best")
plt.show()

```


![png](Pyber_files/Pyber_12_0.png)



```python
# Percentage of Total Rides by City Type
city_rides = pyber_data.groupby(["type"])["ride_id"].count()

# Create Pie Chart
plt.pie(city_rides, 
        labels = city_rides.index, 
        autopct = "%1.2f%%", 
        colors = ["gold", "lightskyblue", "lightcoral"], 
        explode = (0,0,.1), 
        shadow = True, 
        startangle = 125)
plt.axis("equal")
plt.title("% of Total Rides by City Type")
plt.legend(loc= "best")
plt.show()
```


![png](Pyber_files/Pyber_13_0.png)



```python
# Percentage of Total Drivers by City Type
city_drivers = pyber_data.groupby(["type"])["driver_count"].mean()

# Create Pie Chart
plt.pie(city_drivers, 
        labels = city_drivers.index, 
        autopct = "%1.2f%%", 
        colors = ["gold", "lightskyblue", "lightcoral"], 
        explode = (0,0,.1), 
        shadow = True, 
        startangle = 125)
plt.axis("equal")
plt.title("% of Total Drivers by City Type")
plt.legend(loc= "best")
plt.show()
```


![png](Pyber_files/Pyber_14_0.png)

