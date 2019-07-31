# Opening a new Pizza Place in Toronto
#### Gurjyot Singh
#### July 26, 2019

## 1.	Introduction
#### 1.1.	Background
Toronto is a big city and abundant with people. It is the most populated city in Canada. Food places in Canada are famous for having a variety of cuisines. The most popular type of food places are Pizza Places. Pizza is loved by everyone and is affordable too. There are more than 1500 pizzerias in the city of Toronto. To start a new pizza place is a difficult task and requires some analysis of the places first. The main obstacle is predicting if a new pizza place will be popular or not. To do so, one needs to do some analysis of neighbourhoods and the type of food places there.

#### 1.2.	Problem
Data used in the analysis will contain different neighbourhoods, the types of restaurants there and the average number of pedestrians moving from that place. The project aims to finding a suitable place in Toronto where there are few pizza places nearby and a good amount of pedestrians pass by.

#### 1.3.	Interests
People looking to open a new Pizza Place in the city of Toronto will be very much interested in this analysis as it will help them pin point specific locations where they have promising future of a Pizza Place. This project can be modified to work for any kind of business, so anyone looking to open a new business would be very much interested in this project.

## 2.	Data acquisition and cleaning
#### 2.1.	Data Sources
There is no single source of data which could give the types of restaurants and the number of people passing by from locations. We will need to combine data from different sources. The neighbourhoods in Toronto can be scraped by <a href='https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M'>Wikipedia page</a>. We will fetch the restaurants in a neighbourhood using Foursquare API. The dataset for volume of pedestrians passing by at various intersections in Toronto is made available on the <a href='https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/transportation/#7c8e7c62-7630-8b0f-43ed-a2dfe24aadc9'>website of Toronto.</a> The pedestrian volume data however was last updated in 2018, being not so old, it should work fine.

#### 2.2.	Data Cleaning
The data was downloaded from website of Toronto. The data was very clean and didn’t require much processing. The dataset contained coordinates of intersections in the city of Toronto and people passing by those intersections each day. I used Nominatim geocoder from geopy.geocoder. Nominatim geocoder has a method called reverse() used for reverse geocoding coordinates. I found the neighbourhoods of coordinates using this method. There were some locations for which the package couldn’t determine neighbourhood, so I used the city district for those locations instead. After doing so, I noticed there were still some locations with no value in the neighbourhood column. To fill in those missing values, I used the main street name on the intersection.
  
  Next, I grouped the dataframe by neighbourhoods and used average of all the coordinates of intersections in the neighbourhood. I summed up all the pedestrians crossing the intersections in neighbourhood. By doing so, a dataframe with neighbourhoods, pedestrian volumes, and coordinates of the neighbourhoods was achieved.
  
  This dataframe was then fed into foursquare to fetch all the venues in the neighbourhood. Then the venues were filtered out to get only the type of potential competitors with our said Pizza Place. The competitors include burger joints, taco places, and many more fast food joints.
  
  Next, the competitors were counted according to the neighbourhoods and were joined with dataframe containing pedestrian volumes, giving us the final dataframe used for recommendation.

#### 2.3.	Feature Selection
The dataset didn’t contain much of redundant features, but we still had to drop features like TCS#, Main, Midblock Route, Side 1 Route, Side 2 Route, Activation Date, Count Date and 8 Peak Hr Vehicle Volume simply because they weren’t relevant to our problem statement.
The features selected in final dataset were latitude, longitude, 8 Peak Hr Pedestrian Volume. Rest of the features in final dataframe were neighbourhood name and number of competitors which were calculated in the project itself.

## 3.	Methodology
After collecting the data on neighbourhoods and pedestrian volumes, I did a geospatial mapping of the neighbourhoods along with the number of pedestrians passing. Red to violet represents most number of pedestrian to least. Same is with the size of markers.

![image](https://drive.google.com/uc?export=view&id=17E5AHIZtA_q-7jUVaNK7hyqblngEhKcW)

The analysis on data was done during cleaning and gathering data side by side. I had to check the data on almost every step for its consistency. After collecting and cleaning the full data, I used box plots to understand the skewness of data. It helped me identify outliers and the interquartile ranges. Outliers couldn’t be ignored, but I couldn’t remove the outliers because of the fact that these were the most popular places and if they were to be cast out, it needed to be from the criteria I set in recommendation and not before that. 

![image](https://drive.google.com/uc?export=view&id=1C5TL5M8tB_U7DOcVVP2lI8bR39PY4FMD)

The box plot for number of competitors in neighbourhood gave me an idea to set the limits for choosing number of minimum competitors. I chose the threshold at 75% of data, which gave me 3 competitors or less. Similarly, then I chose the threshold for pedestrian volume as 75% of data, which gave me as 15,661 or more. I chose to set the limit at 15,000.

![image](https://drive.google.com/uc?export=view&id=1AghIRF_RtJaoHHU6JR0HF5khatMBNNOx)

The describe method of dataframe gave me a very accurate insight into the data. The final values of limits were set after consideration with the description of dataframe.

![image](https://drive.google.com/uc?export=view&id=1vSw7YcvkchMiAnhimNLGPB0b4vztPDUN)

## 4.	Results
The final recommendation consisted of 20 such places with less than 3 competitors and more than 15,000 pedestrians passing by every day. This recommendation will allow the new businessmen to jump start their business. The recommendation was made by considering the fact that target business is a Pizza Place. The project can be easily morphed to be working for any kind of business. Here are the top 20 recommendations, Red being most recommended and violet being least one.

![image](https://drive.google.com/uc?export=view&id=1dGePYWUiECkAjFLBm_xo8rZKO2bwA-EV)

The result set contains all the necessary information for the client including neighbourhood name, latitude and longitude, number of pedestrians and the number of competitors.
It is recommended that a place within 400-500 meters of the coordinates would hold true for the business recommendation.

![image](https://drive.google.com/uc?export=view&id=1yge8pTiVIy-FtuP6OR2iYIrU3Bl9yKyN)

## 5.	Discussion
The project was aimed at opening a new Pizza Place in the city of Toronto, Canada. But the process for recommending a place for any other kind of business in Toronto is the same. The project can be modified to work for any kind of business in Toronto. For other cities, if the data of pedestrian volumes can be determined, the same project will work. 
The project is not aimed on at Pizza Places in Toronto, but can be aimed at any kind of business in any city in to world provided correct and updated data can be found.

I observed the recommendation is slightly bias to recommend in Downtown Toronto. This is because of the fact once there is an area in Downtown Toronto with a few competitors, it will be most recommended due to the fact that there is the most number of pedestrians in Downtown. But opening a new Pizza Place Uptown, where there is not much competition can also become a success. This issue can probably be resolved by applying some more analysis techniques that I am currently unaware of.

## 6.	Conclusion
Top 20 places in Toronto for opening a Pizza Place were recommended to the client. The client is recommended to look within 400-500 meters of the given coordinates. 
