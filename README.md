This project uses spatio-temporal and demographic data to predict which category of crime is most likely to have occurred, given a time, place and the demographics of the place. 

### Dataset
The dataset contains incidents derived from Atlanta Metropolis Crime Incident Reporting system.
|Feature | Description|
| ------------- |:-------------:|
|incident datetime | time and the date that an incident happened.|
|incident cord x |x-coordinate of the location that the incident happened.|
|incident cord y |y-coordinate of the location that the incident happened.|
|num victims |Number of victims in the incident|
|location type |Type of location the incident happened, correspond to different points such as residential, roads, public etc|
|Crime Type |Type of the crime that took place|

***
## [Data Pre-processing](https://github.com/siddhantmaharana/atlanta-crime-prediction/blob/master/Data_Preprocessing.ipynb) 


### Data Imputation

Missing values in the ‘num victims’ field for the crime type ‘Homicide’ are imputed with the mode value.
Missing values for the 'location type' are imputed using the following steps
1. Search for the exact location match and impute the corresponding location type. 
2. Round off the location co-ordinates to 2 significant figures and impute the mode value.

***
## [Feature Engineering](https://github.com/siddhantmaharana/atlanta-crime-prediction/blob/master/Feature_Engineering.ipynb)

#### Features related to Date and Time

|Feature|Description
| ------------- |:-------------:|
|Week Day|numbers from 1-7 to describe the day of the week
|Week of the year| Number to represent the week of the year
|Hour of the day |Number representing the hour of the day (0 - 24)
|Work hour |Binary Flag representing working hours 1 for 9AM- 7PM and 0 - otherwise
|Sunlight|Binary Flag to represent the presence of Sunlight 1 for 7AM – 7PM and  0 - otherwise

#### Co-ordinate based Features
Clustering algorithms are used to cluster the co-ordinates.
KNN clustering is used to extract clusters from the co-ordinates . Mutiple iterations are performed on the baseline model (Random forest) to get the best cluster size.

#### Features to capture the ‘Hot-Spots’ of various crimes
Several crimes tend to happen more at specific spots of the city. Thus another set of features are developed that can capture the historical crime rates in various clusters which can help the model to detect the presence of ‘hot spots’ and thus aid in predicting better crime results.
1. Number of crimes prior to the incident: A feature to count the number of crimes in the previous week.
2. Crimes ensuing other crimes: A set of features are added that could tell the model if any crime has occurred in the past few hours/days.

***
## [Modelling](https://github.com/siddhantmaharana/atlanta-crime-prediction/blob/master/Modelling.ipynb)

Next step is to predict the response variable, Crime Type in this case.
The response variable consists of 10 labels and thus is a multiclass classification problem. Techniques Used:
1. Random Forest
2. KNN
3. QDA
4. SVC
5. Naive Baeyes
6. Voting Algorithms
7. Boosting techniques:
	1. ADA Boosting
	2. Gradient Boosting
	3. XG Boosting

#### Hyper parameter Tuning
XGB classifier is tuned further to improve the predictions.

