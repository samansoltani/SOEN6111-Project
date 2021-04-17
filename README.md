**We have added a comprehensive report as 'Report.pdf' in the repository.**

## Abstract:
Today, forecasting and predicting is one of the hottest trends in the industry. One of the industries that produce a huge amount of data every day is retailing. This data could be exploited to gain strategic insights for setting up appropriate inventory, achieving benchmark service levels, and so on. It is a challenge to handle and analyze this magnificent amount of data produced by the market giants. These companies invest a lot of their money and time to improve their forecasting solutions for achieving accurate predictions and estimating the levels of uncertainty in these predictions to avoid costly mistakes and maximize their revenue. So, we decided to work on this hot trend by choosing one of the biggest companies in the world, Walmart, where 95% of US shoppers spent their money.

## Introduction:

### Context:
In retail stores like Walmart with a rapid transaction rate, maintaining a balance between customer demand and inventory is a crucial task. If we could achieve optimal forecasts of product sales for the stores spread across various regions, it would enable the decision-makers to make the best use of limited inventory space and maximize the profits. Following on these lines, we will analyze the unit sales of products across the Walmart stores in the United States and try to make optimal predictions that could aid this decision making.

### Objective and Problem to Solve:
In this project, we will analyze the unit sales of products across the Walmart stores in the United States to first explore the factors that have a significant effect on the sales. Exploiting these factors, along with the corpus of historical sales data, we will implement a prediction system to estimate the unit sales of products at various stores for the next 28 days. In the process, we will analyze and exploit the explanatory variables like weekly prices, promotions, day of the week, special events (such as Super Bowl, Valentine’s Day, and Orthodox Easter), and so on.
Predicting unit sales can be as challenging as forecasting weather. For instance, a wrong prediction for the weather may result in us wearing a warm jacket or carrying around an umbrella on a sunny day. Similarly, an inaccurate prediction in a business scenario may result in financial losses or loss of opportunities. So, we will do an exploratory data analysis of the dataset incorporating various perspectives. We will further implement various machine learning algorithms and compare their results to determine the method that provides the most accurate predictions, also stating the uncertainties associated with it.

### Related Work:
1. The M5 Accuracy competition: Results, findings and conclusions: https://www.researchgate.net/publication/344487258_The_M5_Accuracy_competition_Results_findings_and_conclusions
2. Time Series Forecasting-EDA, FE & Modelling: https://www.kaggle.com/anshuls235/time-series-forecasting-eda-fe-modelling

Contrary to most of the previous work, we will attempt to produce a more scalable solution to this problem with the application of Dask and PySpark.

## Material and Methods:

### Technologies:
In this project, we have primarily used Dask and PySpark, apart from the common python libraries. In the first phase of the project, that is, the exploratory data analysis, we have used Dask for data processing and Plotly for visualization. While in the second phase, that is, feature engineering and forecasting with machine learning, we have used PySpark. Although Dask sufficed for the exploratory data analysis, which mostly involved summarizing the data to generate a small-sized output, we saw an explosion of data size in the feature engineering phase. When we melted the time series data to obtain a long format, merged it with other details, and tried to add features, the data size exploded. While Dask was unable to handle it, PySpark performed satisfactorily. At a later stage, when we tried to further improve the performance of the predictions, we sought refuge in LightGBM.

### Dataset:
The M5 dataset provides the unit sales of various products sold by Walmart stores in the United States over 1941 days, organized in the form of grouped time series. This dataset consists of 3049 products, classified into 3 categories (hobbies, foods, and households) and 7 product departments. These products are sold across 10 stores in 3 states (California, Texas, and Wisconsin). Besides the historical time series data, this dataset also includes further information like weekly price changes, SNAP days, and special events (such as, Super Bowl, Valentine’s Day, Orthodox Easter, and so on), which will also allow us to analyze how these factors affect sales. The results obtained from the analysis of this dataset will be scalable as the same methods could be applied to gain insights for other products and stores.

The three files that we used from the dataset are:
1. calendar.csv - Contains information about the dates on which the products are sold. [1]
2. sales_train_evaluation.csv - Contains the historical daily unit sales data per product and store (d_1 - d_1941). [1]
3. sell_prices.csv - Contains information about the price of the products sold per store and date. The price is provided per week (average across seven days). If not available, this means that the product was not sold during the examined week. Note that although prices are constant on a weekly basis, they may change through time (both training and test set). [1]

### Exploratory Data Analysis:
It is vital to visualize and understand the data to develop intuition about the significance of various features in the dataset. The dataset that we used had great potential for exploration, and we found a lot of interesting patterns which equipped us with the knowledge required for feature selection and engineering. A major part of the efforts towards this project has been put into this exploratory data analysis. Please find our work here: [M5 Exploratory Data Analysis](https://nbviewer.jupyter.org/github/samansoltani/SOEN6111-Project/blob/ddb61e700dcfa76332b9a23bf94dc494946c2682/M5%20Exploratory%20Data%20Analysis.ipynb)

### Approach:
Our approach comprises of three main phases as follow:

![alt text](https://github.com/samansoltani/SOEN6111-Project/blob/3a5fee7ca10c393c49e0559f622de069e5ac2706/Images/Workflow.jpg)






