## Abstract:
<p align="justify">
Today, forecasting and predicting is one of the hottest trends in the industry. One of the industries that produce a huge amount of data every day is retailing. This data could be exploited to gain strategic insights for setting up appropriate inventory, achieving benchmark service levels, and so on. It is a challenge to handle and analyze this magnificent amount of data produced by the market giants. These companies invest a lot of their money and time to improve their forecasting solutions for achieving accurate predictions and estimating the levels of uncertainty in these predictions to avoid costly mistakes and maximize their revenue. So, we decided to work on this hot trend by choosing one of the biggest companies in the world, Walmart, where 95% of US shoppers spent their money.
</p>

## Introduction:

### Context:
<p align="justify">
In retail stores like Walmart with a rapid transaction rate, maintaining a balance between customer demand and inventory is a crucial task. If we could achieve optimal forecasts of product sales for the stores spread across various regions, it would enable the decision-makers to make the best use of limited inventory space and maximize the profits. Following on these lines, we will analyze the unit sales of products across the Walmart stores in the United States and try to make optimal predictions that could aid this decision making.
</p>

### Objective and Problem to Solve:
<p align="justify">
In this project, we will analyze the unit sales of products across the Walmart stores in the United States to first explore the factors that have a significant effect on the sales. Exploiting these factors, along with the corpus of historical sales data, we will implement a prediction system to estimate the unit sales of products at various stores for the next 28 days. In the process, we will analyze and exploit the explanatory variables like weekly prices, promotions, day of the week, special events (such as Super Bowl, Valentine’s Day, and Orthodox Easter), and so on.
</p>
<p align="justify">
Predicting unit sales can be as challenging as forecasting weather. For instance, a wrong prediction for the weather may result in us wearing a warm jacket or carrying around an umbrella on a sunny day. Similarly, an inaccurate prediction in a business scenario may result in financial losses or loss of opportunities. To address this problem, we will do an exploratory data analysis of the dataset incorporating various perspectives. Using the information gained, we will implement various machine learning algorithms and compare their results to determine the method that provides the most accurate predictions.
</p>

### Related Work:
1. The M5 Accuracy competition: Results, findings and conclusions: https://www.researchgate.net/publication/344487258_The_M5_Accuracy_competition_Results_findings_and_conclusions
2. Time Series Forecasting-EDA, FE & Modelling: https://www.kaggle.com/anshuls235/time-series-forecasting-eda-fe-modelling

<p align="justify">
Contrary to most of the previous work, we will attempt to produce a more scalable solution to this problem with the application of Dask and PySpark.
</p>

## Material and Methods:

### Technologies:
<p align="justify">
In this project, we have primarily used Dask and PySpark, apart from the common python libraries. In the first phase of the project, that is, the exploratory data analysis, we have used Dask for data processing and Plotly for visualization. While in the second phase, that is, feature engineering and forecasting with machine learning, we have used PySpark. Although Dask sufficed for the exploratory data analysis, which mostly involved summarizing the data to generate a small-sized output, we saw an explosion of data size in the feature engineering phase. When we melted the time series data to obtain a long format, merged it with other details, and tried to add features, the data size exploded. While Dask was unable to handle it, PySpark performed satisfactorily. At a later stage, when we tried to further improve the performance of the predictions, we sought refuge in LightGBM.
</p>

### Dataset:
<p align="justify">
The M5 dataset provides the unit sales of 3049 products sold by Walmart stores in the United States over 1941 days, organized in the form of grouped time series. These products are classified into 3 categories and 7 product departments. These products are sold across 10 stores in 3 states of the United States. Besides the historical time series data, this dataset also includes further information like weekly price changes, SNAP days, festivals, and special events, which will also allow us to analyze how these factors affect sales.
</p>

<p align="center">
    <kbd><img src="https://github.com/samansoltani/SOEN6111-Project/blob/6cf8098eba3d5bdb963881b97252dbce4a4f1099/Images/Dataset%20Hierarchy.jpg" width="650"></kbd>
</p>

The three files that we used from the dataset are:

1. calendar.csv - Contains information about the dates on which the products are sold. [1]
2. sales_train_evaluation.csv - Contains the historical daily unit sales data per product and store (d_1 - d_1941). [1]
3. sell_prices.csv - Contains information about the price of the products sold per store and date. The price is provided per week. [1]

### Exploratory Data Analysis:
<p align="justify">
It is vital to visualize and understand the data to develop intuition about the significance of various features in the dataset. The dataset that we used had great potential for exploration, and we found a lot of interesting patterns which equipped us with the knowledge required for feature selection and engineering. A major part of the efforts towards this project has been put into this exploratory data analysis.
</p>

Please find our work here: [M5 Exploratory Data Analysis](https://nbviewer.jupyter.org/github/samansoltani/SOEN6111-Project/blob/ddb61e700dcfa76332b9a23bf94dc494946c2682/M5%20Exploratory%20Data%20Analysis.ipynb)

### Approach:
Our approach comprises of three main phases as follow:

#### Pre-processing phase:
<p align="justify">
This phase is comprised of the following follows:
</p>

1. <p align="justify">Splitting and Melting: We split the sales data by stores, apply melt to convert the data from wide format to long format, and create separate files for each store.</p>
2. <p align="justify">Merging: We merge the data from all three files so that we have everything in one place.</p>
3. <p align="justify">Downcasting: We downcast the column types to the smallest possible data type that can store all the values of the column to reduce the amount of memory usage, which proved to be very efficient.</p>

#### Feature engineering Phase:
<p align="justify">
In one of the most crucial steps of the process, to reframe the time series data as a regression problem, we introduced various features to the dataset as specified below:
</p>

1. <p align="justify">Lag features: We have introduced lags of 28, 35, 42, 49, 56, 63, and 70 days. Since we aim at making forecasts for the next 28 days, we need to have a minimum lag of 28 days, to ensure that we will not have null values in the features of the final 28 days we make the forecast for.</p>
2. <p align="justify">Rolling mean features: We have introduced rolling mean features using window sizes of 7, 15, and 30 days, lagged by 28 days.</p>
3. <p align="justify">Expanding mean features: We have an expanding mean feature with a lag of 28 days.</p>
4. <p align="justify">Mean features: We have used item mean, department mean, category mean, and store mean.</p>

#### Regression Phase:
<p align="justify">
We applied three Machine Learning algorithms from the PySpark's ML library, which are, Linear Regression, Random Forest Regression, and Gradient Boosted Tree Regression. For evaluating the results, we used RMSE and NRMSE (normalized with standard deviation) metrics. We trained the models for one store and obtained the best results from Random Forest Regression. So, we tried to further optimize this model by performing hyperparameter tuning. However, it was inefficient and PySpark would crash if we tried to perform an exhaustive hyperparameter search. Also, there is no time series cross-validation functionality in PySpark.
</p>

### Approach Improvement:
<p align="justify">
We realized that PySpark’s ML library is not very efficient for the task at hand, and our results could further be improved. So, we decide to add a few tweaks to our approach, which are:
</p>

* Implementing a recursive forecasting model, which would allow us to add lag features with lags lesser than 28 days.
* Introducing:
  * A classical lag feature of 7 days.
  * Rolling mean features with window sizes 7 and 365 days, lagged by 7 days
* Introducing rolling mean features for price in addition to units sold.
* Applying LGBM Regressor in the vanilla python environment.

<p align="justify">
Since we are using lags of 7 days, we need to follow a recursive approach to determine forecasts for 28 days. We can calculate the forecasts for the first 7 days at once since we have all lag features populated. Now, for the next 7 days, we need to recalculate the features using the forecasts of the first 7 days before we can make a forecast for them, and so on.
</p>

<p align="justify">
We did the feature engineering in PySpark and took our final dataset to the vanilla python environment. This allowed us to exploit the scikit-learn library's TimeSeriesSplit and RandomizedSearchCV for hyperparameter tuning, and the LightGBM framework for machine learning. With this approach, we were able to obtain a better result.
</p>

## Results:
1. Linear Regression model (PySpark ML Library):
    * Hyperparameters:
        * max_Iter = 15
        * reg_Param = 0.3
    * Result:
        * RMSE : 2.29
        * NRMSE : 0.637
2. Random Forest Regression (PySpark ML Library):
    * Hyperparameters:
        * maxDepth = 10
        * numTrees = 15 
        * subsampling Rate = 1
    * Result:
        * RMSE: 2.28
        * NRMSE: 0.635 
3. Gradient Boosted Tree (PySpark ML Library):
    * Hyperparameters: 
        * maxDepth = 10
    * Result:
        * RMSE: 2.32
        * NRMSE: 0.646
4. Light GBM (LightGBM Framework):
    * Hyperparameters: 
        * objective = tweedie,
        * tweedie_variance_power = 1.3,
        * n_estimators = 1000,
        * num_leaves = 100,
        * max_depth = 30,
        * learning_rate = 0.03,
        * feature_fraction = 0.7,
        * bagging_fraction = 0.7,
    * Result:
        * RMSE: 2.18
        * NRMSE: 0.6

In conclusion, LightGBM gave the best performance.

<p align="center">
    <kbd><img src="https://github.com/samansoltani/SOEN6111-Project/blob/6017562065398b5769505f8b9379a48846722a82/Images/RMSE%20Comparison.jpeg" width="450"></kbd>
</p>

## Conclusion and Future Work:
We were able to develop a scalable prediction system to generate unit sales predictions for the next 28 days with satisfactory performance. In the process, we experimented with various features and machine learning algorithms in an attempt to improve the performance of the model. As we developed the project on personal computers, we faced several challenges with lack of memory being the most significant one. Dask did exceptionally well in summarizing the data for exploratory data analysis, however, it was not suited for data processing on our infrastructure. At the same time, while PySpark did exceptionally well for data processing and feature engineering, its machine learning library was very restrictive, especially for time series analysis. Also, an exhaustive hyperparameter search with PySpark on our infrastructure was close to impossible. As we moved from PySpark to scikit-learn and LightGBM, our lives were instantly made easier with their machine learning capabilities. In the future, we can further improve the performance of our model by experimenting with feature engineering in PySpark and machine learning algorithms in scikit-learn.
 
## References:
1. https://mofc.unic.ac.cy/m5-competition
2. https://www.researchgate.net/publication/344487258_The_M5_Accuracy_competition_Results_findings_and_conclusions
2. https://www.kaggle.com/anshuls235/time-series-forecasting-eda-fe-modelling

___
**We have added a comprehensive report as 'Report.pdf' in the repository.**
___
