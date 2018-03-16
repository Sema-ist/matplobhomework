

```python
import pandas as pd
import csv
import matplotlib.pyplot as plt

data1 = 'city_data.csv'

city_data = pd.read_csv(data1)

data2= 'ride_data.csv'

ride_data = pd.read_csv(data2)

cityride_data = pd.merge(ride_data, city_data, on='city', how='left')

cityride_data.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Karenfurt</td>
      <td>2017-01-01 19:03:03</td>
      <td>32.90</td>
      <td>3383346995405</td>
      <td>19</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Melissaborough</td>
      <td>2017-01-01 08:55:58</td>
      <td>19.59</td>
      <td>2791839504576</td>
      <td>15</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Sandraport</td>
      <td>2017-01-01 16:21:54</td>
      <td>31.04</td>
      <td>3341437383289</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Curtismouth</td>
      <td>2017-01-03 06:36:53</td>
      <td>15.12</td>
      <td>6557246300691</td>
      <td>40</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Port Michael</td>
      <td>2017-01-03 09:56:52</td>
      <td>19.65</td>
      <td>9887635746234</td>
      <td>73</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
labels = []
colors=('gold','lightskyblue','lightcoral')
i = 0
for type, ride_type_data in cityride_data.groupby("type"):
    # Average Fare ($) Per City
    ride_city_grouped = ride_type_data.groupby("city")
    average_fare = ride_city_grouped['fare'].mean()

    # Total Number of Rides Per City
    total_rides = ride_city_grouped['ride_id'].nunique()
    
    # Total Number of Drivers Per City
    total_drivers = city_data_grouped['driver_count'].mean()

    labels.append(type)
    plt.scatter(total_rides, average_fare, s=total_drivers*5, c=colors[i], alpha=0.7 , marker="o", edgecolors="black")    
    i+=1

```


```python
plt.title("Pyber Ride Sharing Data (2016)")

plt.ylabel("Average Fare")

plt.xlabel("Total Number of Rides (Per City)")

plt.gcf().set_size_inches(11, 7)

plt.legend(labels)

plt.show()
```


![png](output_2_0.png)



```python
print (city_data.city.count(), city_data.city.nunique())
```

    126 126
    


```python
ride_data.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>Karenfurt</td>
      <td>2017-01-01 19:03:03</td>
      <td>32.90</td>
      <td>3383346995405</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Melissaborough</td>
      <td>2017-01-01 08:55:58</td>
      <td>19.59</td>
      <td>2791839504576</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Sandraport</td>
      <td>2017-01-01 16:21:54</td>
      <td>31.04</td>
      <td>3341437383289</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Curtismouth</td>
      <td>2017-01-03 06:36:53</td>
      <td>15.12</td>
      <td>6557246300691</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Port Michael</td>
      <td>2017-01-03 09:56:52</td>
      <td>19.65</td>
      <td>9887635746234</td>
    </tr>
  </tbody>
</table>
</div>




```python
# In addition, you will be expected to produce the following three pie charts:

# % of Total Fares by City Type
# % of Total Rides by City Type
# % of Total Drivers by City Type

city_type = cityride_data.groupby("type")

total_fares_by_city = city_type['fare'].sum()

pie_chart = total_fares_by_city.plot(kind='pie', figsize=(9,9), 
                                     fontsize=15, shadow=0.1, startangle=45, 
                                     explode=[0.0,0.02,0.03], autopct='%1.1f%%',
                                     colors=('gold','lightskyblue','lightcoral'))

plt.title("% of Total Fares by City Type")

plt.gcf().set_size_inches(10, 7)

plt.ylabel("")

plt.show()

plt.show()
```


![png](output_5_0.png)



```python
# In addition, you will be expected to produce the following three pie charts:

# % of Total Rides by City Type
# % of Total Drivers by City Type

city_type = cityride_data.groupby("type")

total_rides_by_city = city_type['ride_id'].nunique()

pie_chart = total_rides_by_city.plot(kind='pie', figsize=(9,9), 
                                     fontsize=15, shadow=0.1, startangle=45, 
                                     explode=[0.0,0.02,0.03], autopct='%1.1f%%',
                                     colors=('gold','lightskyblue','lightcoral'))

plt.title("% of Total Rides by City Type")

plt.gcf().set_size_inches(10, 7)

plt.ylabel("")

plt.show()

plt.show()
```


![png](output_6_0.png)



```python
# % of Total Drivers by City Type

city_type = cityride_data.groupby("type")

total_drivers_by_city = city_type['driver_count'].mean()

pie_chart = total_drivers_by_city.plot(kind='pie', figsize=(9,9), 
                                     fontsize=15, shadow=0.1, startangle=45, 
                                     explode=[0.0,0.02,0.03], autopct='%1.1f%%',
                                     colors=('gold','lightskyblue','lightcoral'))

plt.title("% of Total Drivers by City Type")

plt.gcf().set_size_inches(10, 7)

plt.ylabel("")

plt.show()
```


![png](output_7_0.png)



```python
total_rides_by_city = city_type['ride_id'].nunique()


```


```python
total_drivers_by_city = city_type['driver_count'].count()
```
