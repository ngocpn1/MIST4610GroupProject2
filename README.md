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
The dataset reports the details of crashes within Montgomery County of Maryland and was obtained from https://catalog.data.gov/dataset/crash-reporting-drivers-data. The dimensions of the dataset contain 43 columns and 170218 rows. The data is separated into different main categories - report information: report number, local case number, ACRS report type, and agency name; when and whereabouts of the crash: crash date/time, municipality, latitude, longitude, location, route type, road name, cross-street type, cross-street name, off-road description; involved parties: related non-motorist, person ID, driver at fault, driver substance abuse, non-motorist substance abuse, and injury severity, drivers license state, driver distracted by; collision details: collision type, vehicle damage extent, vehicle first impact locations, vehicle second impact location, vehicle body type, vehicle movement, vehicle continuing dir, and vehicle going dir; vehicle information: vehicle ID, vehicle year, vehicle make, vehicle model, equipment problems; environmental conditions: weather, surface condition, light, traffic control, speed limit; and special circumstances: circumstance, driverless vehicle, and parked vehicle.

Almost all of the columns have string data types except for local case number (whole number), crash date/time (Date/Time), speed limit (whole number), vehicle year (whole number), and longitude & latitude (decimal number).

This dataset provided an abundance of information and allowed us to thoroughly build detailed visualizations.

## Our Two Questions Explained
1. How do the frequency and severity of car crashes vary over different months in Maryland, and are there specific patterns associated with levels of injury severity to drivers when the cars are “moving at a constant speed” vs when they are not “moving at a constant speed”?

We chose this first question because it enables us to visualize the relationship between the injury severity, compared with non-constant/constant speed of cars, and frequency of car crashes and how it relates to the months throughout the year in the state of Maryland. From a public safety perspective, police departments can use the data from this question to create strategic plans to prioritize enforcement of traffic laws and road safety services in months of the year with high frequency and severity of car crashes in Maryland. The decision of whether there should be a greater personnel patroling the streets or emergency services readily available be supported by the data from this question. From a regulatory perspective, governmental bodies like the Federal Highway Administration or Maryland Department of Transportation can make adjustments to road infrastructure or traffic laws based on the months of the year that correlate with high crash frequency. Specifically, adjustment of speed laws of roads can be derived from the relationship of whether constant/non-constant speed on the road has led to greater or lower car crash severity on that particular road. An example would be that if there are high amounts of constant speed car crashes, there may be more stop lights. To conclude, this question allows for greater data-backed decisions in Maryland's public safety and highway management which overall make drivers more safe on the road.

2. What are the geographic hotspots for car crashes in Maryland, and how do these locations of crashes correlate with the driver of the vehicles being impaired or under the influence vs not being impaired?

We chose this second question because it enables us to visualize the geographical area of car crashes in Maryland and whether the car crash involved an impaired driver. Through this we are able to recognize patterns of where car crashes happen most or least and what locations involved high or low levels of impaired drivers involved in a crash. This visualization of data gives entities like police departments and emergency health services greater understanding to what geographical areas to focus their services and where their base locations should be held. Further, police departments are able to know to have greater enforcement of the use of substances for drivers in areas of greater car crashes involving impaired drivers. All in all, this question allows for more informed decision-making for police departments and emergency health services which lead to greater well-being of those in Maryland.
## Data Set Manipulations
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
The most obvious result of this analysis is that the frequency of non-constant speed car crashes is always higher than the frequency of constant speed crashes, indicating that variable speeds contribute to a higher risk of crashes across all severity categories. This result makes sense, as it is much more likely for a car to be turning, accelerating, or decelerating as opposed to driving at a constant speed when in an accident. The red segments, representing possible injury crashes, although smaller in comparison to other severities, are an important visual element. Their presence in the non-constant speed section underscores the critical nature of speed variation in the severity of accidents. The only correlation we see between injury severity and car movement is that "Possible Injury" is generally slightly higher in car accidents with non-constant speeds.

Finally, the visualization shows us that car accidents tend to occur more in the winter months of the year. This makes sense in Maryland, as driving conditions are most likely more dangerous in the winter, leading to more accidents. A more in-depth analysis of the data reveals that certain months, such as December and January, could show a marked increase in the incidence of non-constant speed crashes, which may be attributed to holiday travel and adverse weather conditions.

![Screenshot 2023-12-04 at 5 46 30 PM](https://github.com/NickKalenik/MIST4610GroupProject2/assets/148160069/beccc3e6-9040-4bdb-9ee7-a155a073b8a1)
In our second data visualization, the most noticible trend is that car crashes are much more frequent in areas closer to D.C., which makes sense as many more cars would be driving in this area as opposed to further outside of the city. It is evident that impaired driver accidents concentrate closer to D.C., and taper off along roads that lead further away. This is likely due to the fact that many more bars, restaurants, and alcohol serving locations are located closer to D.C. as opposed to further away. While this is a high overview, a closer view allows for distinction of crashes along individual roads.

<img width="1206" alt="Screenshot 2023-12-05 at 11 08 34 AM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/272896d5-badf-4055-b991-5e09b693b115">

A bar graph of the count of accidents within each category helps us to visualize that while the number of impaired driver accidents may seem high when looking at the overview map, they account for a relatively low number of accidents when compared to those of unimpaired drivers.

<img width="1399" alt="Screenshot 2023-12-05 at 11 07 58 AM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/8f889f0d-d2f0-4663-9e73-70e863033ef9">
As stated previously, a more zoomed in observation of this data map allows for crash data visualization along specific roads. In this particular section of the map, it is clear to see that accidents are happening with the greatest frequency on what appears to be main roads, which concentrate around a particular center of activity. This visualization lends to a city center with a highway loop around the outside. Crashes are interspersed along side roads and throughout the loop, but this visualization allows for these "highways" to be indentified as areas of high accident rates. Further, it can be seen that impaired accidents occur along these high traffic roads and in the center of activity at a higher rate than they occur when crashes are recorded off of these clearly identificable "highways".

# Tableau Packaged Workbook
The tableau workbook is included within the ELC Dropbox.









