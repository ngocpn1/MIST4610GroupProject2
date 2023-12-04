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
## Our Two Questions Explained
## Data Set Manipulations
For our first question, we had to create a calculated field utilizing the "Vehicle Movement" field. This field had 23 domains, which included: 
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

For our second question, we had to create a similar calculated field from the "Driver Substance Abuse" field. This field had 12 members, which included:
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
