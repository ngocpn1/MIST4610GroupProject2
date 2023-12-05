# MIST 4610 Group Project 2

Identifying a data set and answering two interesting questions about the data through Tableau models.

## Team Name & Members
1. David Tran [@dstudent17](https://github.com/dstudent17)
2. Nick Kalenik [@NickKalenik](https://github.com/NickKalenik)
3. Minathi Mekala [@minathi11](https://github.com/minathi11)
4. Ngoc Nguyen [@ngocpn1](https://github.com/ngocpn1)
5. Anthony Ramage [@anthonyramage](https://github.com/anthonyramage)
6. CJ Tumlin [@CJTumlin](https://github.com/CJTumlin)
## Dataset Description
We have created two models from the data we obtained from https://catalog.data.gov/dataset. The data includes information about car crashes in the state of Maryland. The first model shows the total count of crashes for each month of the year. The two bar charts in each month section represent constant speed crashes vs non-constant speed crashes. Each bar is colored to represent the three different injury levels of each crash - no apparent injury, possible injury, and suspected minor injury.

The second model is a geographical representation of every crash within the dataset. It shows crash hotspots and could be used to find intersections or portions of roads that have an above average crash rate. The data is further filtered by separating each crash based upon whether or not the driver was in some state of impairment. 

## Our Two Questions Explained
1. How do the frequency and severity of car crashes vary over different months in Maryland, and are there specific patterns associated with levels of injury severity to drivers when the cars are “moving at a constant speed” vs when they are not “moving at a constant speed”?

We chose this question because it highlights an important difference in the data. Cars that are moving at a constant speed should be safer than a car constantly changing speeds, and this should affect the data. In addition, the visualization will show if the time of year impacts the frequency and severity of car crashes in Maryland.

2. What are the geographic hotspots for car crashes in Maryland, and how do these locations of crashes correlate with the driver of the vehicles being impaired or under the influence vs not being impaired?

We chose this question because if there are geographical hotspots for car crashes, then maybe something can be changed about the intersection/etc to fix the issue. We also chose to incorporate data whether the individual was impaired at the time of the accident. This could highlight specific hotspots that may be close to local bars.

## Data Set Manipulations and Filters
For our FIRST question, we had to create a calculated field utilizing the "Vehicle Movement" field. This field had 23 domains, which included: 
- ACCELERATING
- BACKING
- CHANGING LANES
- DRIVERLESS MOVING VEH.
- ENTERING TRAFFIC LANE
- LEAVING TRAFFIC LANE
- MAKING LEFT TURN
- MAKING RIGHT TURN
- MAKING U TURN
- MOVING CONSTANT SPEED
- N/A
- NEGOTIATING A CURVE
- OTHER
- PARKED
- PARKING
- PASSING
- RIGHT TURN ON RED
- SKIDDING
- SLOWING OR STOPPING
- STARTING FROM LANE
- STARTING FROM PARKED
- STOPPED IN TRAFFIC LANE
- UNKNOWN
Because we wanted to analyze the difference in crash severity between a car moving at a constant speed and a car moving at a non-constant speed, we had to condense all of these domains into two categories in a new calculated field named "Constant or Non-Constant Speed?" The two categories included:
- CONSTANT SPEED
- NON-CONSTANT SPEED
The calculation to arrive at this result is as follows:

IF [Vehicle Movement] = 'UNKNOWN' OR [Vehicle Movement] = 'N/A' THEN NULL 
ELSEIF [Vehicle Movement] = 'MOVING CONSTANT SPEED'
THEN 'CONSTANT SPEED'
ELSE 'NON-CONSTANT SPEED'
END

When using this calculated field in our model, we filtered out domains such as "UNKNOWN", "N/A", "OTHER", and any null values to make our model more accurate.

For our SECOND question, we had to create a similar calculated field from the "Driver Substance Abuse" field. This field had 12 members, which included:
- ALCOHOL CONTRIBUTED
- ALCOHOL PRESENT
- COMBINATION CONTRIBUTED
- COMBINED SUBSTANCE PRESENT
- ILLEGAL DRUG CONTRIBUTED
- ILLEGAL DRUG PRESENT
- MEDICATION CONTRIBUTED
- MEDICATION PRESENT
- N/A
- NONE DETECTED
- OTHER
- UNKNOWN
Since we wanted to compare impaired car accidents versus non-impaired car accidents, we created a calculated field named "Impaired or Non-Impaired" with two members that included:
- NO IMPAIRMENT
- IMPAIRED 
The calculation to arrive at this result is as follows:

IF [Driver Substance Abuse] = 'UNKNOWN' OR [Driver Substance Abuse] = 'N/A' THEN NULL
ELSEIF[Driver Substance Abuse] = 'NONE DETECTED'
THEN 'NO IMPAIRMENT'
ELSE 'IMPAIRED'
END

When applying this calculated field to our models, we filtered out "N/A", "OTHER", "UNKOWN", and any null values to make the results more accurate.

## Analysis & Results
![Screenshot 2023-12-04 at 5 39 21 PM](https://github.com/NickKalenik/MIST4610GroupProject2/assets/148160069/c37d04ec-745a-4bec-8f86-d08226635640)
The most obvious result of this analysis is that the frequency of non-constant speed car crashes is always higher than the frequency of constant speed crashes. This result makes sense, as it is much more likely for a car to be turning, accelerating, or decelerating as opposed to driving at a constant speed when in an accident. 

The only correlation we see between injury severity and car movement is that "Possible Injury" is generally slightly higher in car accidents with non-constant speeds. 

Finally, the visualization shows us that car accidents tend to occur more in the winter months of the year. This makes sense in Maryland, as driving conditions are most likely more dangerous in the winter, leading to more accidents.

![Screenshot 2023-12-04 at 5 46 30 PM](https://github.com/NickKalenik/MIST4610GroupProject2/assets/148160069/beccc3e6-9040-4bdb-9ee7-a155a073b8a1)
In our second data visualization, the most noticible trend is that car crashes are much more frequent in areas closer to D.C., which makes sense as many more cars would be driving in this area as opposed to further outside of the city.

A second observation that can be made from this data is that there is a relatively high number of accidents caused by driver impairment when compared to preexisting notions. While  there are more non-impaired driver accidents, there is a very noticeable and measurable amount of impaired driver accidents among the data.

While this is a high overview of the entire data map, a closer observation allows for crash data visualization along specific roads, which can be seen on some parts of the map already. It is evident that impaired driver accidents concentrate closer to the city, and taper off along roads that lead further away. This is likely due to the fact that many more bars, restaurants, and alcohol serving locations are located closer to D.C. as opposed to further away.

# Honors Option Third Question
3. What manufacturing years of cars are most frequently involved in accidents and tend to sustain the highest level of damage?

I chose this question to model because I wanted to look at the damage sustained by the different manufacutring years of cars in an attempt to see if there were any noticeable trends that arose around these different years of cars. This visualization could help to determine if any particular year of manufacturing showed poor safety and quality, or if a particular year resulted in less damages due to a new regulation or safety standard. I also wanted to view the body types of cars involved in accidents those years, in order to determine if an increase in a particular body type may have an impact on whether or not the overall damages of cars made in that year increased.

## Data Set Manipulation and Filters
In order to accomplish the first part of this data visualization, the combined bar and line chart, I first filtered the Vehicle Manufacturing Year by a range of dates from 1995 to 2019. I found that not enough data was available on either side of this range to provide enough evidence for determining trends in damage extent.
I then filtered the data based Vehicle Damage Extent. I only used crashes that had reported some form of damages, and removed crashes with N/A, OTHER, or UNKOWN damages incurred.

To accomplish the second part of this data visualization, a bar chart of when the crashes occurred, I used the same two filters as above.

For the third part of this visaulization, the pie chart of vehicle body types, I used the same filters as above, with a slider based filter on the Vehicle Year, as well as a new calculated field. In order to summarize all Vehicle Body Types into a a few similar categories, I had to use a calculated field to aggregate them based on similarities. I grouped all vehicles into 6 Groups, PASSENGER CAR, TRUCK, EMERGENCY VEHICLE, MOTORCYCLE, BUS, and OTHER. I used this code to do that.

IF \
   [Vehicle Body Type] = "ALL TERRAIN VEHICLE" OR \
   [Vehicle Body Type] = "AUTOCYCLE" OR \
   [Vehicle Body Type] = "FARM VEHICLE" OR \
   [Vehicle Body Type] = "LOW SPEED VEHICLE" OR \
   [Vehicle Body Type] = "N/A" OR \
   [Vehicle Body Type] = "OTHER" OR \
   [Vehicle Body Type] = "RECREATIONAL VEHICLE" OR \
   [Vehicle Body Type] = "SNOWMOBILE" OR \
   [Vehicle Body Type] = "UNKNOWN" \
THEN "OTHER" \
ELSEIF \
   [Vehicle Body Type] = "AMBULANCE/EMERGENCY" OR \
   [Vehicle Body Type] = "AMBULANCE/NON EMERGENCY" OR \
   [Vehicle Body Type] = "FIRE VEHICLE/EMERGENCY" OR \
   [Vehicle Body Type] = "FIRE VEHICLE/NON EMERGENCY" OR \
   [Vehicle Body Type] = "POLICE VEHICLE/EMERGENCY" OR \
   [Vehicle Body Type] = "POLICE VEHICLE/NON EMERGENCY" \
THEN "EMERGENCY VEHICLE" \
ELSEIF \
   [Vehicle Body Type] = "CARGO VAN/LIGHT TRUCK 2 AXLES (OVER 10,000LBS (4,536 KG))" OR \
   [Vehicle Body Type] = "MEDIUM/HEAVY TRUCKS 3 AXLES (OVER 10,000LBS (4,536 KG))" OR \
   [Vehicle Body Type] = "OTHER LIGHT TRUCKS (OVER 10,000LBS (4,536 KG))" OR \
   [Vehicle Body Type] = "PICKUP TRUCK" OR \
   [Vehicle Body Type] = "TRUCK TRACTOR" \
THEN "TRUCK" \
ELSEIF \
   [Vehicle Body Type] = "CROSS COUNTRY BUS" OR \
   [Vehicle Body Type] = "SCHOOL BUS" OR \
   [Vehicle Body Type] = "OTHER BUS" OR \
   [Vehicle Body Type] = "TRANSIT BUS" \
THEN "BUS" \
ELSEIF \
   [Vehicle Body Type] = "PASSENGER CAR" OR \
   [Vehicle Body Type] = "LIMOUSINE" OR \
   [Vehicle Body Type] = "STATION WAGON" OR \
   [Vehicle Body Type] = "VAN" OR \
   [Vehicle Body Type] = "SPORT UTILITY VEHICLE (SUV)" \
THEN "PASSENGER CAR" \
ELSEIF \
   [Vehicle Body Type] = "MOTORCYCLE" OR \
   [Vehicle Body Type] = "MOPED" \
THEN "MOTORCYCLE" \
ELSE "OTHER" \
END 

## Analysis and Results
<img width="1406" alt="Screenshot 2023-12-04 at 10 06 53 PM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/b0e6ab28-7263-4908-903a-bc1e5ceee409">

<img width="1312" alt="Screenshot 2023-12-04 at 10 04 22 PM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/30054d8f-32c3-448e-9cbd-bc74b6c2585e">

<img width="1247" alt="Screenshot 2023-12-04 at 10 04 45 PM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/71b787ac-7c7b-48e5-80c8-bb0869b41b6e">

<img width="1409" alt="Screenshot 2023-12-04 at 10 05 04 PM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/2f164fc9-3f0d-40e7-a996-9b6de59e95c9">

To create this analysis, I first used a dashboard to combine all of these different models into one comprehensive. I also included each individual sheet as its own photo.

The first trend that is noticeable is that the majority of accidents occur on vehicles that were made in 2015. When looking at the bar graph of when crashes took place, this trend makes sense as the majority of car crashes that are recorded took place in 2016, one year after these cars manufactured in 2015 would have been released. 

One thing that can be looked at with the pie chart is that a large majority of the 2015 made cars involved in these accidents are PASSENGER CARS. This can be looked at in conjuction with the fact that 2015 had the largest number of DISABLING damages recorded. If the pie chart is shifted either a year up or down, it can be seen that the percent of PASSENGER CARS goes down, as well as the number of DISABLING damages recorded. Overall, it seems as though 2015 cars are involved in the most accidents and sustain the most damages, while also having one of the relatively lowest number of cars without damages. One assumption that can be made from this is that 2015 cars werebuilt before newer safety regulations and standards were introduced.

Overall, the trend is that newer cars are involved in crashes less, and tend to sustain less damages as well. While this may be due to the fact these cars have been on the road less, some of the variability may be explained by increased safety regulations and quality standards implemented throughout time.

# Tableau Packaged Workbook
The tableau workbook which includes the group work and my personal Honors Option Work is included within the ELC Dropbox.






