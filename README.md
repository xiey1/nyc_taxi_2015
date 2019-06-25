# nyc_taxi_2015
NYC green and yellow taxi trip data in year 2015
<br>Data source: https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page

* [PartI: Data cleaning, pre-processing, computation and visualization of summary statistics](#PartI_link)

* [PartII: Exploratory data analysis of randomly selected 1,000,000 trip records for each of green and yellow taxi datasets](#PartII_link)

* PartIII: Create animation of geographical heatmaps of pickup and dropoff trip density as well as speed
* PartIV: K-means clustering, data interpretation and visualization
* PartV: Geohash encoding and analyze the top10 popular routes for NYC green and yellow taxi 

<a id='PartI_link'></a>
## PartI: Data cleaning, pre-processing, computation and visualization of summary statistics
### Summary of dataset statistics:
    Total number of trip records for NYC green taxi: 19233765
    Total number of trip records for NYC yellow taxi: 146112989
    Ratio: 1:7.7

## Question: When does people take taxi?
### 1. Daily trip number in year 2015 (day_of_year)
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Total_trip_number_dayofyear.png' width=600px>

#### Q: What happend on 01/27/2015? -- The Blizzard of January 26-27, 2015
   reference: https://www.weather.gov/okx/Blizzard_01262715
<img src="https://www.weather.gov/images/okx/Blizzard_01262715//header.png" width=600px>


<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Total_trip_number_dayofweek.png' width=600px>
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Total_trip_number_hour.png' width=600px>
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Total_trip_number_month.png' width=600px>



### Heatmap for green taxi pickup and dropoff density by hour
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/green_taxi_pickup_hour.gif' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/green_taxi_dropoff_hour.gif' width=400px>

### Heatmap for yellow taxi pickup and dropoff density by hour
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/yellow_taxi_pickup_hour.gif' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/yellow_taxi_dropoff_hour.gif' width=400px>

### Heatmap for green and yellow taxi speed by hour
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/green_taxi_speed_hour.gif' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/yellow_taxi_speed_hour.gif' width=400px>
