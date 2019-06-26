# nyc_taxi_2015
NYC green and yellow taxi trip data in year 2015
<br>Data source: https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page

* [Part I: Summary statistics](#PartI_link)
* [Part II: Exploratory data analysis](#PartII_link)
* [Part III: Create animation of geographical heatmaps of trip density and speed](#PartIII_link)
* [Part IV: K-means clustering](#PartIV_link)
* [Part V: Geohash encoding and the top10 popular routes](#PartV_link)

<a id='PartI_link'></a>
## Part I: Summary statistics
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
<br>Overall, March, April and May are the months with the highest total trip number for both NYC green and yellow taxi. This might be due to the improved weather conditions since the winter season so that people can have more outdoor activites. The trip number plunges since May and hits the bottom in August and September. One possible explanation is the expanding business of Uber.
<br>(reference: https://www.amny.com/transit/manhattan-taxi-trips-plunge-almost-4-million-in-3-months-analysis-1.10984180)

<a id='PartII_link'></a>
## Part II: Exploratory data analysis
Here I randomly selected 1,000,000 trip records from each of green and yellow taxi datasets for exploratory data analysis.
### 1. Geographical features
Here a bounding box with coordinates LL = (-74.30, -73.70, 40.56, 40.90) was used to filter trips. Only trips with pickup and dropoff coordinates that fall in the range defined by the bounding box are analyzed.

<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Geographical_distribution_map_green.png' width=600px>
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Geographical_distribution_map_yellow.png' width=600px>

* 1. NYC green taxi has almost zero pickup in upper east side, midtown or downtown Manhattan, consistent with the regulation that green taxi is not allowed to pick up passengers below West 110th and East 96th streets in Manhattan.

* 2. Pickup locations for yellow taxi is highly enriched in upper east side, upper west side, midtown and downtown Manhattan. Yellow taxi also has heavy pickup in JFK and LGA. Green taxi has pickup locations more widely distributed in Harlem, Bronx, Brooklyn and Queens, which almost exhibits an exclusive pattern with yellow taxi pickup distribution. In addition, green taxi has a higher pickup trip density in areas closer to Manhattan compared to regions that are farther away.

* 3. For both green and yellow taxi, the density map of dropoff locations has a wider and more diluted distribution pattern compared to the pickup density map. Green taxi can drop off passengers in Manhattan and there is also a heavy dropoff in JFK. Dropoff locations for yellow taxi have a wider spread to Brooklyn and Queens, but with a higher dropoff density in areas closer to Manhattan.

<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Coordinate_distribution_green.png' width=500px>
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Coordinate_distribution_yellow.png' width=500px>

As shown in the density plots, the numerical distributions of coordinates have very different patterns between green and yellow taxi. 

* 1. For green taxi, both longitude and latitude distributions have multiple peaks. The longitude distribution is more centered around a main peak at -73.95 with multiple small peaks next to it spanning from -74.05 to -73.75.The latitude has a wider distribution of 4 peaks with approximately equal height spanning from 40.65 to 40.90. This is consistent with the pickup and dropoff patterns of NYC green taxi visualized in seciton 2.1.1 that green taxi mainly operate in Harlem, Bronx, Brooklyn and Queens. These areas have closer longitude coordinates while the latitude shows larger variation.

* 2. For both longitude and latitude of green taxi trips, there is no significant difference between pickup and dropoff distributions. However, we do notice that peaks for pickup coordinates are sharper and have better separation from surrounding peaks compared to dropoff coordinates. One possible reason is that the pickup locations are relatively more concentrated (eg. at transportation hubs) while dropoff locations have a wider and more diluted distribution pattern. 

* 3. The distributions of pickup and dropoff coordinates for yellow taxi approximate normal distribution. The longitude has a sharper peak compared to latitude, which can be explained by the shape of Manhattan Island. The longitude is centered around -73.99 and the latitude around 40.75, which corresponds to the coordinates of several busiest transportation hubs in NYC such as the Grand Central Terminal (lat:40.7527, lon:-73.9772) and the Penn Station (lat:40.7506,lon:-73.9936). These altogether sugguest that trips of NYC yellow taxi are heavily concentrated in Manhattan.

* 4. In addition, there is a small but distinct peak for latitude at 40.64, which corresponds to the coordinate of JFK (lat:40.6413, lon:-73.7781). This also explains the small peak centered around -73.78 for longitude. The other small peak at longitude centered around -73.88 may likely correspond to Jackson Heights (lat:40.7557, lon:-73.8831).

### 2. Temporal features
Since weekend has very different trip patterns from weekday, it is helpful to analyze how hourly trip number fluctuates conditioned on day of week.

<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_number_hour_dayofweek_green.png' width=600px>
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_number_hour_dayofweek_yellow.png' width=600px>

### 3. Distribution of trip direction
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_direction.png' width=600px>

The two main peaks in trip direction for yellow taxi center around 60 and -120 degree respectively. This aligns with the long axis of Manhattan with 60 corresponding to uptown trips and -120 corresponding to downtown trips. Green taxi still has the direction peak centered around -120 degree while the 60 degree peak is not very distinct. This suggests that there are more trips heading downtown compared to updown for green taxi. Since green taxi mainly operates in regions outside Manhanttan, distribution of trip direction has a more uniform distribution except for the peak at -120 degree.

### 4. Correlation between trip_distance, trip_duration and fare_amount
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_distance_duration.png' width=600px>
<br>Pearson correlation for trip distance and trip duration for NYC green taxi data: 0.793
<br>Pearson correlation for trip distance and trip duration for NYC yellow taxi data: 0.781

<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_distance_amount.png' width=600px>
<br>Pearson correlation for trip distance and fare amount for NYC green taxi data: 0.940
<br>Pearson correlation for trip distance and fare amount for NYC yellow taxi data: 0.954
The majority of the trips with fare amount of $52 are trips with either pickup or dropoff locations at JFK.

### 5. Temporal distribution of trip_duration, speed, trip_distance and fare_amount
#### Trip duration
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_duration_hour_green.png' width=600px>
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_duration_hour_yellow.png' width=600px>

#### Speed
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_speed_hour_green.png' width=600px>
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_speed_hour_yellow.png' width=600px>

#### Trip distance
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_distance_hour_green.png' width=600px>
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_distance_hour_yellow.png' width=600px>

#### fare amount
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_amount_hour_green.png' width=600px>
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Trip_amount_hour_yellow.png' width=600px>

<a id='PartIII_link'></a>
## Part III: Create animation of geographical heatmaps of trip density and speed

### Heatmap for green taxi pickup and dropoff density by hour
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/green_taxi_pickup_hour.gif' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/green_taxi_dropoff_hour.gif' width=400px>

### Heatmap for yellow taxi pickup and dropoff density by hour
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/yellow_taxi_pickup_hour.gif' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/yellow_taxi_dropoff_hour.gif' width=400px>

### Heatmap for green and yellow taxi speed by hour
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/green_taxi_speed_hour.gif' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/yellow_taxi_speed_hour.gif' width=400px>

<a id='PartIV_link'></a>
## Part IV: K-means clustering
### 1. Cluster pickup and dropoff coordinates
<br>Here, I chose to use 15 clusters

<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/K-means_cluster1_15_green_total.png' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/K-means_cluster1_15_yellow_total.png' width=400px>

The animation of taxi trips operating between each cluster is shown here:
<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/green_taxi_cluster1_hour_col.gif' width=420px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/animation/yellow_taxi_cluster1_hour_col.gif' width=420px>

<br>The neighborhood interactions:

<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Interaction_map_green.png' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Interaction_map_yellow.png' width=400px>

<br>The number of inbound and outbound trips in each area:

<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Outbound_Inbound_green.png' width=400px><img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/Outbound_Inbound_yellow.png' width=400px>


<a id='PartV_link'></a>
## Part V: Geohash encoding and the top10 popular routes
<br>I use precision = 6 to encode and decode the pickup and dropoff coordinates of each trip with ±0.61 km error.
<br>For green taxi:
* unique number of gh6 encoded pickup points: 1785
* unique number of gh6 encoded dropoff points: 2397
* unique number of routes: 285293
* The top10 most popular routes account for 1.42% total trips in year 2015 for green taxi (267974, ~734/day)

<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/NYC_green_taxi_top10_routes.png' width=900px>
<br>The top10 popular routes is distributed in 3 areas: Jackson Heights, McCarren Park and Harlem. 

<br>For yellow taxi:
* unique number of gh6 encoded pickup points: 2877
* unique number of gh6 encoded dropoff points: 3179
* unique number of routes: 320727
* The top10 most popular routes account for 2.09% total trips in year 2015 for yellow taxi (2977667 trips, ~8158/day)

<img src='https://github.com/xiey1/nyc_taxi_2015/blob/master/images/NYC_yellow_taxi_top10_routes.png' width=900px>
<br>The top10 popular routes for NYC yellow taxi operate between transportation hubs or popular spots in Manhattan such as Port Authority, Penn Station and Grand Central.

