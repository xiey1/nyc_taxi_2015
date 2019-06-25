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
<br>The daily trip number for both green and yellow taxi fluctuates throughout year 2015 in a periodic pattern at intervals of approximately 4 cycles per month.

#### Q: What happend on 01/27/2015? -- The Blizzard of January 26-27, 2015
   reference: https://www.weather.gov/okx/Blizzard_01262715
<img src="https://www.weather.gov/images/okx/Blizzard_01262715//header.png" width=600px>


### 2. Total number of trips on each day of week
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Total_trip_number_dayofweek.png' width=600px>
<br>Overall, trip number reaches peak on Saturday and returns to the lowest level on Monday for both green and yellow taxi.

### 3. Hourly trip number
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Total_trip_number_hour.png' width=600px>
<br>The hourly trip number varies significantly throughout the day and both green and yellow taxi exhibit a similar changing trend. Generally, the trip number reaches the lowest point at 5 am in the morning and starts to quickly ascent until 8 am (when most people start to go to work). The trip number keeps relatively constant from 9 am to 4 pm (1 pm for green taxi) and then starts to climb again until 7 pm. The evening peak at 6-7 pm is likely due to the rush hour of people getting off work (either heading home or other places). After 7 pm, the hourly trip number starts to descent and plunges after 1 am until reaches the lowest point at 5 am. The dynamic temporal pattern of hourly trip number largely reflects people's daily activity.

### 4. Total number of trips on each month
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Total_trip_number_month.png' width=600px>
Overall, March, April and May are the months with the highest total trip number for both NYC green and yellow taxi. This might be due to the improved weather conditions since the winter season so that people can have more outdoor activites. The trip number plunges since May and hits the bottom in August and September. One possible explanation is the expanding business of [Uber](https://www.amny.com/transit/manhattan-taxi-trips-plunge-almost-4-million-in-3-months-analysis-1.10984180).



### Heatmap for green taxi pickup and dropoff density by hour
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/green_taxi_pickup_hour.gif' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/green_taxi_dropoff_hour.gif' width=400px>

### Heatmap for yellow taxi pickup and dropoff density by hour
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/yellow_taxi_pickup_hour.gif' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/yellow_taxi_dropoff_hour.gif' width=400px>

### Heatmap for green and yellow taxi speed by hour
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/green_taxi_speed_hour.gif' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/yellow_taxi_speed_hour.gif' width=400px>
