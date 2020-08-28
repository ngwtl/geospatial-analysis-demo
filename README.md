## Project 4 - West Nile Virus Prediction
---
   Leonard | Melvin | Pallavi
    
---

### Introduction and problem statement

West Nile virus (WNV) is the leading mosquito-borne disease in the United States ([CDC, 2009](https://www.cdc.gov/westnile/index.html)). It is a single-stranded RNA virus from the family Flaviviridae, which also contains the Zika, dengue, and yellow fever virus. It is primarily transmitted by mosquitoes (mainly <i>Culex</i> spp.), which become infected when they feed on birds, WNV's primary hosts. Infected mosquitos then spread WNV to people and another animals by biting them. Cases of WNV occur during mosquito season, which starts in the summer and continues through fall ([CDC, 2009](https://www.cdc.gov/westnile/index.html)). 

While WNV is not extremely virulent and only about 1 in 5 people who are infected develop West Nile fever and other symptoms, about 1 out of every 150 infected develop a serious and sometimes fatal illness ([CDC, 2009](https://www.cdc.gov/westnile/index.html)). There is currently no vaccine against WNV.

In view of the recent outbreak of WNV in Chicago, the Chicago Department of Public Health (CDPH) has set up a surveillance and control system to trap mosquitos and test for the presence of WNV. The goal of this project is to use these surveillance data to predict the occurrence of WNV given time, location, and mosquito species. Findings from this project will guide and inform decisions on where and when to deploy pesticides throughout the city, to maximise pesticide effectiveness and minimise spending.

### Executive Summary
For this project, we will consider 4 datasets, namely, train, test, spray and weather.

Once the datasets are imported, we will explore each feature. Feature engineering comes next as we transform the date and weather features. Categorical features are also transformed to dummy variables.

Finally, we will train our model using GridSearch, of which, the best model will be used for our Kaggle submission.

### Data Dictionary
---

|Feature|Type|Dataset|Description|
|---|---|---|---|
|Id            |int      |train.csv/test.csv |ID number of the record
|Date           |datetime      |train.csv/test.csv |date the WNV test is performed
|Address      |datetime |train.csv/test.csv| approximate trap address; sent to GeoCoder
|Species         |str      |train.csv/test.csv| mosquito species in trap
|Block         |str      |train.csv/test.csv| block number of address
|Street        |str      |train.csv/test.csv| street of address
|Trap          |str    |train.csv/test.csv| ID number of the trap
|AddressNumberAndStreet|str|train.csv/test.csv| approximate address retrieved from GeoCoder
|Latitude            |float|train.csv/test.csv| latitude retrieved from GeoCoder
|Longitude            |float|train.csv/test.csv| longitude retrieved from GeoCoder
|AddressAccuracy      |int|train.csv/test.csv| accuracy of information returned from GeoCoder
|NumMosquitos        |int      |train.csv/test.csv| number of mosquitoes in a sample
|WnvPresent           |int      |train.csv/test.csv| whether or not WNV is present in a sample (1 = present; 0 = absent)
|Date |datetime |spray.csv| date of spray
|Time         |datetime      |spray.csv| time of spray
|Latitude|float|spray.csv| latitude of spray
|Longitude        |float|spray.csv| longitude of spray
|Station  |int|weather.csv| weather station (1 or 2)
|Date     |datetime|weather.csv| date of measurement
|Tmax     |int|weather.csv| maximum daily temperature (F)
|Tmin     |int|weather.csv| minimum daily temperature (F)
|Tavg  |int|weather.csv| average daily temperature (F)
|Depart     |int|weather.csv| departure from normal temperature (F)
|Dewpoint    |int|weather.csv| average dewpoint (F)
|WetBulb  |int|weather.csv| average wet bulb
|Heat     |int|weather.csv| heating degree days
|Cool  |int|weather.csv| cooling degree days
|Sunrise     |int|weather.csv| time of sunrise (calculated)
|Sunset     |int|weather.csv| time of sunset (calculated)
|CodeSum     |str|weather.csv| code of weather phenomena 
|Depth     |int|weather.csv| unknown
|Water1  |int|weather.csv| unknown
|SnowFall     |int|weather.csv| snowfall (inch)
|PrecipTotal     |str|intweather.csv| total daily rainfall (inch)
|StnPressure     |int|weather.csv| average atmospheric pressure (inch Hg)
|SeaLevel     |int|weather.csv| average sea level pressure (inch Hg)
|ResultSpeed  |float|weather.csv| resultant wind speed (mph)
|ResultDir     |int|weather.csv| resultant wind direction (degrees)
|AvgSpeed     |int|weather.csv| average wind speed (mph)


### Modelling
---

Using XGBoost (our best performing model), we achieved an ROC_AUC of **0.8511**. GridSearchCV and cross_val_score were used to tune the respective classifier with the optimised hyperparameters and then check if the learning algorithm is capable of yielding high mean score and low variances as we would want the selected learning algorithm to be capable of producing similar performance on unseen data. In this case it will be the test set provided by kaggle.

By comparing the above scores, the final learning algorithm that is choosen is XGBoost. Using the best parameters selected are `colsample_bytree = 0.2`, `gamma = 0.03`, `learning_rate = 0.1`, `max_depth = 3`, `reg_alpha = 0`, `reg_lambda = 1`, `subsample = 0.5`.
    
    

### Summary of Findings & Recommendations

Examination of the the total costs of spraying the whole of Chicago compared against the benefits show that the costs far outweigh the benefits in monetary terms. At best, accounting for inflation or even a pessimistic outcome of having 50% more WNV infections, the total monetary benefit to Chicago as a society may only be 16%-25% of the total cost of spraying.

However, our model does not take into account any non-monetary benefits to reducing the mosquito population. These include the emotional costs from loss of life, the reduction in the need for enhanced testing for suspected WNV cases and public confidence in the government.

From previous geospatial analysis of spray data, there is a distinct lack of evidence to support the claim that mosquito spraying had any effect on the reduction of WNV-infected mosquitos. Furthermore, the spray data pointed towards highly fragmented and haphazardous spraying operations that did not seem to be driven by the evidence if the presence and severity of WNV mosquito infestations. Traps such as the T900 trap at O'Hare International airport which proved to capture the most WNV-infected mosquitos by far were not sprayed.

Given the high costs required to conduct spraying operations, we hence recommend the following action points:

- Re-examine the effectiveness of spraying Zenivex™ E4 as a means to control the mosquito population. Evidence points towards the ineffectiveness of the chemical and it is likely that other kinds of non-toxic mosquito sprays should be explored.

- Re-direct mosquito spraying operations in a more organised and evidence-driven manner whereby severe hotspots such as O'Hare International Airport are sprayed first at the beginning of summer in order to prevent large populations of mosquitos forming. In addition, spraying operations should be accurately logged and routes planned to make sure mosquito breeding sites are properly covered.

- Examine new ways of controlling the mosquito population that may arguably cost less than spraying the whole of Chicago. Innovative ways of doing so may include 'anti-mosquito' campaigns done in places such as Singapore or encouraging citizens of Chicago to get rid of stagnant water sources.


### Folder Organisation:
---
    |__ code
    |   |__ 01_eda.ipynb   
    |   |__ 02_modeling.ipynb    
    |__ assets
    |   |__ train.csv
    |   |__ test.csv
    |   |__ processed.zip    
    |   |__ weather.csv
    |   |__ spray.csv
    |   |__ mapdata_copyright_openstreetmap_contributors.txt
    |__ chicago_geodata
    |   |__ geo_export_55fcb48c-7621-4c8a-999c-9fb3c86e8950.dbf
    |   |__ geo_export_55fcb48c-7621-4c8a-999c-9fb3c86e8950.prj
    |   |__ geo_export_55fcb48c-7621-4c8a-999c-9fb3c86e8950.shp
    |   |__ geo_export_55fcb48c-7621-4c8a-999c-9fb3c86e8950.shx
    |__ planning_doc.xlsx
    |__ group_presentation.pdf
    |__ README.md
