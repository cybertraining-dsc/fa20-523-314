# Residential Power Usage Prediction

- [ ] please use our trivial template posted in piazza
- [x] please never use sapces in image names
- [ ] please use footnotes for refernces, you must cite them
- [X] figure numbers are inconsitent, you have 3 figures
- [ ] document not checked on content graders will do that

Siny P Raphel, [fa20-523-314](https://github.com/cybertraining-dsc/fa20-523-314/), [sinypr@gmail.com](https://github.com/cybertraining-dsc/fa20-523-314/blob/master/project/project.md)

## Introduction

Electricity is an inevitable part of our day today life. Most of the electric service providers like duke, dominion provide customers their consumption data so that customers are aware of their usages. Some providers give predictions on their future usages so that they are prepared. 

This project is based on the dataset Residential Power Usage 3 years data in Kaggle datasets[^1]. The dataset contains data of hourly power consumption of a 2 storied house in Houston,Texas from 01-06-2016 to August 2020. It includes data during the Covid-19 lockdown and are marked as well. We are planning to build a model to predict future usage from available data. 

## Datasets

Data is spread across two csv files.

*	`power_usage_2016_to_2020.csv`

This file contains basic details of the data like startdate with hour, value of power consumption in kwh, day of the week and notes. It has 4 features and 35953 instances. 

![Figure 1](https://github.com/cybertraining-dsc/fa20-523-314/blob/master/project/images/fig-1.png)

**Figure 1:** First five rows of power_usage_2016_to_2020 data

Day of the week is an integer value with 0 being Monday. Notes gives us details like whether that day is weekend, weekday, covid lockdown or vacation. The Figure 1 shows retrieval and first few rows of the data.

![Figure 2](https://github.com/cybertraining-dsc/fa20-523-314/blob/master/project/images/fig-2.png)

**Figure 2:** Details in "notes" column

*	weather_2016_2020_daily.csv

This file contains the weather conditions of that particular day. It has 19 features and 1553 instances. Figure 3 shows retrieval and first few rows and columns of this file.

![Figure 3](https://github.com/cybertraining-dsc/fa20-523-314/blob/master/project/images/fig-3.png)

**Figure 3:** First few rows of weather_2016_2020_daily data

Units of features are given as follows:

* Temperature    - F deg
* Dew Point      - F deg
* Humidity       - %age
* Wind           - mph
* Pressure       - Hg
* Precipitation  – inch

## Planning

We will be using python to develop the model. Since the expected outputs are real numbers(power consumption in kWh) we might be using linear regression or similar ones. We will try using gradient descent for optimization. Since the weather data has 19 features we might use feature selection methods to select best features that increase the accuracy of the model. 
The data spread across two files will have to be merged according to date. For that the StartDate feature will have to be first split to date and time. Then the two datasets will have to be merged according to the date only. From the initial inspection of the data, the date feature of datasets have some date format issues which will have to be resolved before starting cleaning. 

In this project we will be planning the following steps:

1.	Analyze and clean the data
2.	Visualize the data- study the relationships between features etc.
3.	Plan one or two algorithms that can be used to model
4.  Optimize or feature selection of features
5.	Calculate accuracy of each model
6.	Conclusion on which algorithm will be best suited to use and the reason for it.

## Reason to choose this dataset

This dataset is chosen because,

1.	There were datasets similar to this one. But this one has latest power usage data till August this year.
2.	It has marked covid lockdown, vacations, weekdays and weekends which is a challenge for prediction.

## References

[^1]: <https://www.kaggle.com/srinuti/residential-power-usage-3years-data-timeseries>
