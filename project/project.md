# Residential Power Usage Prediction

[![Check Report](https://github.com/cybertraining-dsc/fa20-523-314/workflows/Check%20Report/badge.svg)](https://github.com/cybertraining-dsc/fa20-523-314/actions)
[![Status](https://github.com/cybertraining-dsc/fa20-523-314/workflows/Status/badge.svg)](https://github.com/cybertraining-dsc/fa20-523-314/actions)
Status: in progress


Siny P. Raphel, [fa20-523-314](https://github.com/cybertraining-dsc/fa20-523-314/), [Edit](https://github.com/cybertraining-dsc/fa20-523-314/blob/main/project/project.md)

{{% pageinfo %}}

## Abstract

We are living in a technology-driven world. New innovations make human life easier. As the science advances, the usage of electrical and electronic gadgets are leaping. This leads to the shoot up of power consumption. Weather plays an important role in the power usage. Even the outbreak of Covid-19 has impacted daily power utilization. Similarly, many factors influence the use of electricity driven appliances at homes. Monitoring these factors and consolidating will result in humungous amount of data. But analyzing this data will help to keep track of power consumption. This system provides a prediction of usage of electric power at residences in the future and will enable people to plan ahead of time and not surprised by the monthly electricity bill.

Contents

{{< table_of_contents >}}

{{% /pageinfo %}}

**Keywords:** power usage, big data, regression 

## 1. Introduction

Electricity is an inevitable part of our day-to-day life. The residential power sector consumes about one-fifth of the total energy in the U.S. economy[^1]. Most of the appliances in a household uses electricity for its working. The usage of electricity in a residence depends on the standard of living of the country, weather conditions, family size, type of the residence etc[^2]. Most of the houses in USA are equipped with lightings and refrigerators using electric power. The usage of air conditioners is also increasing. From Figure 1, we can see that the top three categories for energy consumption are air conditioning, space heating, water heating as of 2015.

![Figure 1](https://github.com/cybertraining-dsc/fa20-523-314/raw/main/project/images/chart.png)

**Figure 1:** Residential electricity consumption by end use, 2015[^3].

Climate change is one of the biggest challenges in our current time. As a result, temperatures are rising. Therefore, in order to analyze energy consumption, understanding weather variations are critical[^4]. As the temperature rises, use of air conditioners are also rising. As shown in Figure 1, air conditioning is the primary source of power consumer in households. Weather change has also resulted in drop of temperatures and variation in humidity. These results in secondary power consumers.

Even though weather plays an important role in power usage, factors like household income, age of the residents, family type etc also influence consumption. During holidays many people tend to spend time outside which reduces power utilization at their homes. Similarly, during weekend, since most people have work off, the appliances will be frequently consumed compared to weekdays when they go to work. Our world is currently facing an epidemic. Most of the countries had months of lockdown periods. Schools and many work places were closed. People were not allowed to go out and so they were stuck at their homes. As a result, power expending reduced drastically everywhere other than residences. But during lockdown period the energy consumption of residences spiked.

Most of the electric service providers like duke, dominion provide customers their consumption data so that customers are aware of their usages. Some providers give predictions on their future usages so that they are prepared.

## 2. Reason to choose this dataset

There were many datasets on residential power usage analysis in Kaggle itself. But most of them were three or four years old. This dataset has the recent data of power consumptions together with weather data of each day. Since the pandemic hit the world in 2019-2020, the availability of recent data is considered to be significant for the analysis. 

This dataset is chosen because,

1.	It has the latest power usage data - till August 2020.
2.	It has marked covid lockdown, vacations, weekdays and weekends which is a challenge for the prediction.

## 3. Datasets

This project is based on the dataset, _Residential Power Usage 3 years data_ in Kaggle datasets[^5]. The dataset contains data of hourly power consumption of a 2 storied house in Houston, Texas from 01-06-2016 to August 2020 and also weather conditions of each day like temperatures, humidity wind etc of that area. Each day is marked whether it is a weekday, weekend, vacation or COVID-19 lockdown. 

The project is intending to build a model to predict future power consumption of a house with similar environments from the available data. Python[^8] is used for the development and since the expected output is a continuous variable, linear regression is considered for baseline model. Later the performance of the base model is compared to one or two other models like tuned linear regression, gradient boosting, Light Gbm or random forest.

Data is spread across two csv files.

*	power_usage_2016_to_2020.csv

This file depicts the hourly electricity usage of the house for three years, from 2016 to 2020. It contains basic details like startdate with hour, value of power consumption in kwh, day of the week and notes. It has 4 features and 35953 instances. 

![Figure 2](https://github.com/cybertraining-dsc/fa20-523-314/raw/main/project/images/fig-1.png)

**Figure 2:** First five rows of power_usage_2016_to_2020 data

Figure 2 provides a snapshot of the first few rows of the data. Day of the week is an integer value with 0 being Monday. The column _notes_ lay out details like whether that day was weekend, weekday, covid lockdown or vacation, as shown in Figure 3.

![Figure 3](https://github.com/cybertraining-dsc/fa20-523-314/raw/main/project/images/fig-2.png)

**Figure 3:** Details in notes column

*	weather_2016_2020_daily.csv

The second file or the weather file imparts the weather conditions of that particular area on each day. It has 19 features and 1553 instances. Figure 4 is the snapshot of the first few rows and columns of this file.

![Figure 4](https://github.com/cybertraining-dsc/fa20-523-314/raw/main/project/images/fig-3.png)

**Figure 4:** First few rows of weather_2016_2020_daily data

Each feature in this data has different units and the units of the features are given in Table 1.

**Table 1:** Feature units

| Feature names| Units |
| ------------ | ----- |
| Temperature  | F deg |
| Dew Point    | F deg |
| Humidity     | %age  |
| Wind         | mph   |
| Pressure     | Hg    |
| Precipitation| inch  |

Weather file has additional features like _date_ and _day_ of the date.

## 4. Data preprocessing

The data has to be preprocessed before modelling for predictions.

### 4.1 Data download and load

The data in this project is directly downloaded from _Kaggle_. The downloaded file is then unzipped and loaded to two dataframes using python codes. For more detailed explanation and codes for download and load of data, see [python code](https://github.com/cybertraining-dsc/fa20-523-314/blob/main/project/code/residential_power_usage_prediction.ipynb) _Download datasets_ and _Load datasets_ sections.

### 4.2 Data descriptive analysis

The data loaded has to be analysed properly before it can be preprocessed. Analysis is made on the existance of missing values, range of each features etc. On analysis, it is determined that there are no missing values and the date format in both tables are different. The _StartDate_ feature of power_usage dataset and _Date_ feature of the weather dataset are to be used as key to merge the two datasets. But the format of both features are different. StartDate feature is the combination of date and hour. Whereas, _Date_ feature of weather is just the date. Hence, these issues will have to be taken care of before merging data. 

### 4.3 Preprocessing data

In this step, the column name _Values (kWh)_  is renamed to _Value_ and also date format issue is addressed. First StartDate column is split into Date and Hour columns. Since the StartDate column is in Pandas Period type, the function strftime() is used for converting to the required format.

### 4.4 Merge datasets

For proper analysis of data, it is critical that the analyst should be able to analyse the relationships of each features with respect to the target feature(Value in kWh in this project). Therefore, both power_usage and weather tables are merged with respect to Date column. The resulting table has a total of 35952 instances and 22 features.

## 5. Exploratory Data Analysis

Here we analyse different features, their relation with each other and target. 

![Figure 5](https://github.com/cybertraining-dsc/fa20-523-314/raw/main/project/images/dow.png)

**Figure 5:** Average power usage by day of the week

In Figure 5, the average power usage by the day of the week is plotted[^6]. It is analyzed that Saturday and Friday has the most usage compared to other days of the week. Since day of th week represents values Sunday-Saturday, we can consider it as a categorical feature.
Similarly, from Figure 6, there is a huge dip in power usage during vacation. Other three occasions like covid lockdown, weekend and weekdays have almost same power usage, even though consumption during weekends outweigh.

![Figure 6](https://github.com/cybertraining-dsc/fa20-523-314/raw/main/project/images/tod.png)

**Figure 6:** Average power usage by type of the day

In Figure 7, we compare the monthly power consumption for three years - 2018, 2019, 2020[^7]. The overall power usage in 2019 is less compared to 2018. But in 2020 may be due to Covid-lockdown the power consumption shoots. Also, power consumtion peaks in the months June, July and August. 

![Figure 7](https://github.com/cybertraining-dsc/fa20-523-314/raw/main/project/images/monthly_power.png)

**Figure 7:** Average power usage per month for three years

![Figure 8](https://github.com/cybertraining-dsc/fa20-523-314/raw/main/project/images/corr_plot.png)

**Figure 8:** Correlation plot between features

The correlation plot in Figure 8, depicts the inter-correlation between features. We can see that features like temperature, dew and pressure has high correlation to our target feature. Also different temperatures and dew features are inter-correlated. Therefore, all the intercorrelated features except for temp_avg can be dropped during feature selection. 

## 6. Modelling

### 6.1 Split Data

For measuring the accuracy of the model, the main data is split into train and test. 20% of data is selected as test data and the remaining 80% is the train data. The proportion of notes(vacation, week day, weekend and covide lockdown) are different. Therefore, we stratify the data according to notes column. After split, train data has 28761 rows and test data has 7191 rows. 

### 6.2 Pipelines

Categorical variables and numeric variables are separated and processed in pipelines separately.
Categorical features are one hot encoded before feeding to the model. Similarly, numerical features are standardized before modelling. Later these two pipelines are joined and modelled used Linear regression and other models. 

### 6.3 Metrics

Out target is a continous variable and hence we implement regression models for prediction. In order to determine how accurate a regression model is, we use the following metrics.

#### 6.3.1 Mean squared error(MSE)

MSE is the average of squares of error. The larger the MSE score, the larger the errors are. Models with lower values of MSE is considered to perform well. But, since MSE is the squared value, the scale of target variable and MSE will be different. Therefore, we go for RMSE values.

#### 6.3.2 Root mean squared error(RMSE)

RMSE is the square root of MSE scores. The square root is introduced to make scale of the errors to be the same as the scale of targets. Similar to MSE, the lower scores for RMSE means the better model performance. Therefore, in this project, the models with lower RMSE values will be monitored[^9].

#### 6.3.3 R-Squared(R2) Score

R2 score is the goodness-of-fit measure. It's a statistical measure that ranges between 0 and 1. R2 score helps the analyst to understand how similar the fitted line is to the data it is fitted to. The closer it is to one, the more likely the model predicts its variance. Similarly, if the score is zero, the model doesn't predict any variance.
In this project the R2 score of the test data is calculated. The model with highest R2 scores will be considered[^9].

### 6.4 Baseline Linear Regression model

Wwe use linear regression as our baseline model. For baseline model, we are not hyperparameter tuning. For baseline model, the train RMSE score was 0.6783 and R2 for test set was 0.4460. These values are then compared to other regression models with hyperparameter tuning. 

### 6.5 Other regression models

After developing a baseline model, we are developing four other regression models and comparing the results. We implement feature selection and hyperparameter tuning. As we analysed in exploratory data analysis, some features have strong inter-correlation and these features are dropped. The parameters for the regression models are hypertuned and modelled in GridsearchCV of sklearn package. 

The models used for prediction are:

* Linear regression with hyperparamter tuning
* Gradient boosting
* XGBoost
* Light GBM

Similar to baseline model, the metrics like train RMSE, test RMSE and test R2 scores are calculated.

### 6.6 Results

![Figure 9](https://github.com/cybertraining-dsc/fa20-523-314/raw/main/project/images/result.png)

**Figure 9:** Performance of all regression models

Figure 9 documents the performance of all the regression models used. 

cloudmesh.common benchmark and stopwatch framework are used to monitor and record time taken for each steps in this project[^10]. Time taken for critical steps like downloading data, loading data, preprocessing data and execution of each models are recorded. The StopWatch recordings are shown in Table 2. StopWatch recordings played an important role in the selection of best model.

**Table 2:** StopWatch recordings

| Name                         | Status   |     Time |      Sum | Start               | tag   | Node         | User   | OS    | Version                             |
|------------------------------|----------|----------|----------|---------------------|-------|--------------|--------|-------|-------------------------------------|
| Data preprocessing           | ok       |   72.986 |  146.383 | 2020-11-30 08:10:16 |       | 756da8d039ed | collab | Linux | #1 SMP Thu Jul 23 08:00:38 PDT 2020 |
| Baseline Linear Regression   | ok       |    2.747 |    2.747 | 2020-11-30 08:11:31 |       | 756da8d039ed | collab | Linux | #1 SMP Thu Jul 23 08:00:38 PDT 2020 |
| Linear Regression            | ok       |    5.288 |   15.77  | 2020-11-30 08:11:34 |       | 756da8d039ed | collab | Linux | #1 SMP Thu Jul 23 08:00:38 PDT 2020 |
| Gradient Boosting            | ok       |  249.175 |  556.847 | 2020-11-30 08:11:39 |       | 756da8d039ed | collab | Linux | #1 SMP Thu Jul 23 08:00:38 PDT 2020 |
| XGBoost                      | ok       | 2947.85  | 6196.89  | 2020-11-30 08:15:48 |       | 756da8d039ed | collab | Linux | #1 SMP Thu Jul 23 08:00:38 PDT 2020 |
| Light GBM                    | ok       |  800.339 | 1564.25  | 2020-11-30 09:04:56 |       | 756da8d039ed | collab | Linux | #1 SMP Thu Jul 23 08:00:38 PDT 2020 |

For the baseline model, the RMSE values were high and R2 scores was small compared to all other regression models. The hyperparameter tuned linear regression model scores are better compared to basline model. But other three models outweigh both linear models. XGBoost has the lowest RMSE and highest R2 score of all other models. But the time taken for execution is too long. Therefore, XGBoost is computationally expensive which lead us to ignore its scores. Gradient boosting and Ligh GBM have similar scores and hence the time taken for execution has to be considered as the deciding factor here. Gradient boosting completed 135 fits in 249.175 seconds whereas LightGBM took around 1564.25 seconds for executing 1250 fits. Since per fit execution time for Light GBM is too small, we consider Light GBM as the best model for predicting daily power usage of a residence with similar background conditions.
 
## 7. Conclusion

As importance of electricity is increasing, the need to know how or where the power usage increase should also be understood. The model helps to predict the power usage when a set of parameters like weather conditions, weekdays, type of days etc are provided. 
Since the output is power consumption in kWh, we selected regression for modelling and prediction. After analysing the results, we concluded that the performance of Light GBM model is better and faster compared to all other models that we experimented.

## 8. Acknowledments

The author would like to express special thanks to Dr. Geoffrey Fox, Dr. Gregor Von Laszewski and all the associate instructors of Big Data Applications course(FA20-BL-ENGR-E534-11530) offered by Indiana University, Bloomington for the guidance and support throughout the project.
 
## 8. References

[^1]: Jia Li and Richard E. Just, Modeling household energy consumption and adoption of energy efficient technology, Energy Economics, vol. 72, pp. 404-415, 2018.
Available: <https://www.sciencedirect.com/science/article/pii/S0140988318301440#bbb0180>

[^2]: Domestic Power Consumption, [Online resource] <https://en.wikipedia.org/wiki/Domestic_energy_consumption>

[^3]: Use of energy explained - Energy use in homes, [Online resource] <https://www.eia.gov/energyexplained/use-of-energy/electricity-use-in-homes.php>

[^4]: Yating Li, William A. Pizer, and Libo Wu, Climate change and residential electricity consumption in the Yangtze River Delta, China, Research article, Available: <https://www.pnas.org/content/116/2/472#ref-1>

[^5]: Residential Power Usage dataset, <https://www.kaggle.com/srinuti/residential-power-usage-3years-data-timeseries>

[^6]: seaborn: statistical data visualization, <https://seaborn.pydata.org/index.html>

[^7]: Group by: split-apply-combine, <https://pandas.pydata.org/pandas-docs/stable/user_guide/groupby.html>

[^8]: Residential Power Usage Prediction script, <https://github.com/cybertraining-dsc/fa20-523-314/blob/main/project/code/residential_power_usage_prediction.ipynb>

[^9]: Mean Square Error & R2 Score Clearly Explained, [Online resource] <https://www.bmc.com/blogs/mean-squared-error-r2-and-variance-in-regression-analysis/>

[^10]: Gregor von Laszewski, Cloudmesh StopWatch and Benchmark from the Cloudmesh Common Library, <https://github.com/cloudmesh/cloudmesh-common>
