# Residential Power Usage Prediction


[![Check Report](https://github.com/cybertraining-dsc/fa20-523-314/workflows/Check%20Report/badge.svg)](https://github.com/cybertraining-dsc/fa20-523-314/actions)

Siny P Raphel, [fa20-523-314](https://github.com/cybertraining-dsc/fa20-523-314/), [Edit](https://github.com/cybertraining-dsc/fa20-523-314/blob/master/project/project.md)

{{% pageinfo %}}

## Abstract

Electricity is an inevitable part of our day today life. Most of the electric service providers like duke, dominion provide customers their consumption data so that customers are aware of their usages. Some providers give predictions on their future usages so that they are prepared. This project is based on the dataset Residential Power Usage 3 years data in Kaggle datasets[^1]. The dataset contains data of hourly power consumption of a 2 storied house in Houston, Texas from 01-06-2016 to August 2020. It includes data during the Covid-19 lockdown and are marked as well. We are planning to build a model to predict future usage from available data. 

Contents

{{< table_of_contents >}}

{{% /pageinfo %}}

**Keywords:** power usage, big data, regression 

## 1. Introduction

Most of the houses in USA are equipped with lightings and refrigerators using electricity. The usage of air conditioners is also increasing. From Figure 1, we can see that top three categories for energy consumption are air conditioning, space heating, water heating as of 2015.

![Figure 1](https://github.com/cybertraining-dsc/fa20-523-314/raw/master/project/images/chart.png)

**Figure 1:** Residential electricity consumption by end use, 2015[^2].

## 2. Datasets

Data is spread across two csv files.

*	`power_usage_2016_to_2020.csv`

This file contains basic details of the data like startdate with hour, value of power consumption in kwh, day of the week and notes. It has 4 features and 35953 instances. 

![Figure 2](https://github.com/cybertraining-dsc/fa20-523-314/raw/master/project/images/fig-1.png)

**Figure 2:** First five rows of power_usage_2016_to_2020 data

Day of the week is an integer value with 0 being Monday. Notes gives us details like whether that day is weekend, weekday, covid lockdown or vacation. The Figure 2 shows retrieval and first few rows of the data.

![Figure 3](https://github.com/cybertraining-dsc/fa20-523-314/raw/master/project/images/fig-2.png)

**Figure 3:** Details in "notes" column

*	weather_2016_2020_daily.csv

This file contains the weather conditions of that particular day. It has 19 features and 1553 instances. Figure 4 shows retrieval and first few rows and columns of this file.

![Figure 4](https://github.com/cybertraining-dsc/fa20-523-314/raw/master/project/images/fig-3.png)

**Figure 4:** First few rows of weather_2016_2020_daily data

Units of features are given as follows:

* Temperature    - F deg
* Dew Point      - F deg
* Humidity       - %age
* Wind           - mph
* Pressure       - Hg
* Precipitation  – inch

## 3. Merge datasets

The 'StartDate' feature of power_usage dataset and 'Date' feature of the weather dataset are used as key to merge the two datasets. But the format of both features is different. StartDate feature is the combination of date and hour. Whereas, 'Date' feature of weather is just the date. So first 'StartDate' column is split into 'Date' and 'Hour' columns. Since the 'StartDate' column is in Pandas Period type, the function strftime() is used for converting to the required format.

## 4. Exploratory Data Analysis

Here we analyse different features, their relation with each other and target. 

![Figure 5](https://github.com/cybertraining-dsc/fa20-523-314/raw/master/project/images/dow.png)

**Figure 5:** Average power usage by day of the week

![Figure 6](https://github.com/cybertraining-dsc/fa20-523-314/raw/master/project/images/tod.png)

**Figure 6:** Average power usage by type of the day

## 5. Planning

We will be using python to develop the model. Since the expected outputs are real numbers(power consumption in kWh) we might be using linear regression or similar ones. We will try using gradient descent for optimization. Since the weather data has 19 features we might use feature selection methods to select best features that increase the accuracy of the model. 
The data spread across two files will have to be merged according to date. For that the StartDate feature will have to be first split to date and time. Then the two datasets will have to be merged according to the date only. From the initial inspection of the data, the date feature of datasets have some date format issues which will have to be resolved before starting cleaning. 

In this project we will be planning the following steps:

1.	Analyze and clean the data
2.	Visualize the data- study the relationships between features etc.
3.	Plan one or two algorithms that can be used to model
4.  Optimize or feature selection of features
5.	Calculate accuracy of each model
6.	Conclusion on which algorithm will be best suited to use and the reason for it.

## 6. Reason to choose this dataset

This dataset is chosen because,

1.	There were datasets similar to this one. But this one has latest power usage data till August this year.
2.	It has marked covid lockdown, vacations, weekdays and weekends which is a challenge for prediction.


## 7. Project Timeline:

 * EDA and preprocessing - 11/09/2020
 * First set of result    - 11/11/2020
 * Hyperparameter tuning, pipelines/ final setup - 11/15/2020
 
## 8. Conclusion

Will be added on completion
 
## 9. References

[^1]: Residential Power Usage dataset, <https://www.kaggle.com/srinuti/residential-power-usage-3years-data-timeseries>

[^2]: Use of energy explained - Energy use in homes, <https://www.eia.gov/energyexplained/use-of-energy/electricity-use-in-homes.php>
