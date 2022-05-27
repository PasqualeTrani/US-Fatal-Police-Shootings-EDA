# US-Fatal-Police-Shootings-EDA
The goal of this work is to analyze the dataset of fatal police shootings in the US, edited by The Washington Post. Specifically, we will focus on racial distinctions because, as we will see, there is a huge difference between the different races. In particular, we will see that in proportion black people are the "most killed". 

The work is organized as follows:

1) First of all we will observe some generic plots concerning the data and then we will introduce the problem concerning the "surplus" of black people killed by US police.

2) Second of all we will study how this problem manifests itself in the various US states, by introducing some other data concerning the states. In particular, we will see which are the states where there are the highest numbers of black people killed per million. 

3) After that we will focus on a specific subdataframe containing the "unfair" cases, i.e. the cases where probably the police could have avoided shooting. 

4) Then we will see which are the states where the difference between the black people and the other races is more pronunced, namely the states where the problem of the "surplus" of black people killings is more relevant. We will call these states "problematic states".

5) After that we will see if the things are getting better, by studying the temporal trend of the phenomenon. 

6) Lastly, we will look for possible correlations between some socio-demographic variables, such as poverty rate and the level of education, and the parameter black_ratio which, as we will see, is the best parameter for measuring the racial distinctions between black race and the others. Moreover, we will find some interesting properties of these "problematic states". In specific, one of them may furnish a possible explanation to the huge "surplus" of black people killings that we observe in these states.  




##### Here there are all the links where you can find the data used in this work:

- US Police Fatal Shootings: https://github.com/washingtonpost/data-police-shootings/blob/master/fatal-police-shootings-data.csv

- US States Races Data: https://www.kff.org/other/state-indicator/distribution-by-raceethnicity/?dataView=0&currentTimeframe=0&sortModel=%7B%22colId%22:%22Location%22,%22sort%22:%22asc%22%7D

- US States Population: https://en.wikipedia.org/wiki/List_of_U.S._states_and_territories_by_population

- US States Poverty Rate: https://en.wikipedia.org/wiki/List_of_U.S._states_and_territories_by_poverty_rate

- US States Level of Education: https://en.wikipedia.org/wiki/List_of_U.S._states_and_territories_by_educational_attainment

- US States Gun Ownership Rate: https://worldpopulationreview.com/state-rankings/gun-ownership-by-state

- US States Avarage Police Officier Salary: https://www.forbes.com/sites/andrewdepietro/2020/04/23/police-officer-salary-state/?sh=347d63692010

- US States Value of a Dollar: https://taxfoundation.org/real-value-100-state-2019/

- Us States Violent Crime Rate: https://en.wikipedia.org/wiki/List_of_U.S._states_and_territories_by_violent_crime_rate

- US States Requirements to Become a Policeman: https://www.cga.ct.gov/2001/rpt/2001-r-0092.htm


##### Here there is an overview of all the variables that are used:
##### In The Washington Post Us Police Killings Dataframe:

|  Variable Name 	|   Variable Description	|   Type	|   Values	|
|---	|---	|---	|---	|
|  'id' 	|   It is a number that identificate the relative killing	|   discrete numerical 	|   	|
|   'name'	|   It is the name of the person killed	|  categorical 	|   	|
|   'date'	|   It is the date of the relative killing	| categorical  	|   	|
|   'manner_of_death'	|   how the person was killed 	|   categorical	| shot: the person was shooted  <br> shot and Tasered: the person was shooted and Tesered |
|   'armed'	|   the arm used by the criminal	| categorical   	|   	|
|   'age'	|   the age of the killed person	|  discrete numerical  	|   	|
|   'gender'	|   the gender of the killed person	|   categorial	|   	|
|   'race'	|   the race of the killed person	|  categorical 	|    W: White <br> B: Black <br> H: Hispanic <br> A: Asian <br> N: Native <br> O: Other	|
|   'city'	|   the city where the person was killed	|   categorical 	|   	|
|   'signs_of_mental_illness'	|   if the person had signs of mental illness	|   Boolean	|   True: the person had sign of mental illness <br> False: the person had not signs of mental illness	|
|   'threat_level'	|  the threat level for the police 	|   categorical 	|  attack: the criminal was attacking the police <br> other: the criminal was not attacking the police <br> undetermined : the threat level is undetermined	|
|   'flee'	|   how the criminal was fleeing	|   categorical  	| Not fleeing: the criminal was not fleeing <br> Car : the criminal was using a car to flee <br> Foot : the crimal was fleeing by foot <br> Other : the criminal was fleeing in different ways 	|
| 'body_camera'  	|   if the police had a body camera installed	|  Boolean 	| True: the police had a body camera <br>   False: the police had not a body camera	|
|  'longitude' 	|   the longitude of the place where the person was killed	| continuous numerical  	|   	|
|  'latitude' 	|   the latitude of the place where the person was killed	|  continuous numerical 	|   	|
|   'is_geocoding_exact'	|  accuracy of the coordinates  	| Boolean   	|  True: coordinates are for the location of the shooting <br>  False: coordinates are for the centroid of a larger region (such as city or county)	|


##### In the Us States stats dataframe, which contains all the data concerning the states  :


| Variable Name  	|   Variable Description	|   Type	|   Values	|
|---	|---	|---	|---	|
|  'state' 	|   the name of the state considered 	|   categorical	|   	|
|   'abbreviation'	|  the abbreviation of the state 	|   categorical	|   	|
|   'White'	|  the rate of white people in the state  	|  continuous numerical 	|   	|
|  'Black' 	|  the rate of black people in the state 	|   continuous numerical	|   	|
|  'Hispanic' 	|   the rate of hispanic people in the state 	|   continuous numerical	|   	|
|   'Asian'	|   the rate of asian people in the state	|   continuous numerical	|   	|
|   'American Indian/Alaska Native'	|  the rate of native people in the state 	|   continuous numerical	|   	|
|   'population'	|   the population of the state 	|   discrete numerical	|   	|
|   'poverty_rate'	|    the parameter that measures the poverty level in the state	|   continuous numerical	|   	|
|   'high_school'	|  the rate of persons who has a high school diploma 	|   continuous numerical	|   	|
|   'bachelor_degree'	|   the rate of persons who has a bachelor degree	|   continuous numerical	|   	|
|  'advanced_degree' 	|   the rate of persons who has an advanced degree	|   continuous numerical	|   	|
|   'gun_ownership'	|   the rate of people who has a gun	|   continuous numerical	|   	|
|  'avg_pol_income' 	|  the avarage police officier salary 	|   continuous numerical	|   	|
|   'value_of_a_dollar'	|   the value of a dollar in the state, i.e. the parameter that measures the cost of living	|   continuous numerical	|   	|
|   'violent_crime_rate'	| the rate of violent crime, for example murder, rape and gang violence, per million   	|  continuous numerical 	|   	|
|  'requirements_to_become_a_policeman' 	|   the requirements to become a police officier	|   categorical	|   High school diploma: the only requirement is the high school diploma <br> More than High school diploma: there are more requirements then just the high school diploma, like a bachelor degree or a minimal amount of university credit	|
