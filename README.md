# SOEN6111-Project-proposal
Abstract:

Today, forecasting and predicting is one of the hottest trends in the industry. One of the industries that produce a huge amount of data every day is retailing. This data could be exploited to gain strategic insights for setting up appropriate inventory, achieving benchmark service levels, and so on. It is a challenge to handle and analyze this magnificent amount of data produced by the market giants. These companies invest a lot of their money and time to improve their forecasting solutions for achieving accurate predictions and estimating the levels of uncertainty in these predictions to avoid costly mistakes and maximize their revenue. So, we decided to work on this hot trend by choosing one of the biggest companies in the world, Walmart, where 95% of US shoppers spent their money.

Introduction:

•	Context:

In this project, our analysis will revolve around the unit sales of various products sold across the United States available in the form of a grouped time series. The dataset further includes item level, department, product categories, and store details. Also, we have other details like promotions and special events happening around, which could be employed to further improve the predictions.

•	Objective and Problem to Solve:

Giant companies like Walmart produce a significant amount of valuable data. In this project, our main objective is to exploit this data to implement a prediction system to estimate the unit sales of Walmart retail goods at stores in various locations for the next 28 days. We will further aim to improve the accuracy of our prediction system using explanatory variables such as price, promotions, day of the week, and special events (e.g., Super Bowl, Valentine’s Day, and Orthodox Easter) that significantly affect sales.
Calculating the unit sales can be as hard as forecasting weather. For instance, a wrong prediction for the weather may result in us wearing a warm jacket or carrying around an umbrella on a sunny day. Similarly, an inaccurate prediction in a business scenario may result in financial losses or loss of opportunities. So, we will be analyzing the dataset from various perspectives and implementing various algorithms to finally compare the results of all these methods to determine the method that provides the most accurate predictions. Being aware of the uncertainties in the predictions is equally important for making the right decisions. So, we will be further making uncertainty estimates for these forecasts.

•	Related Work:

1.	The M5 Accuracy competition: Results, findings and conclusions: 
https://www.researchgate.net/publication/344487258_The_M5_Accuracy_competition_Results_findings_and_conclusions

2.	Time Series Forecasting-EDA, FE & Modelling:
https://www.kaggle.com/anshuls235/time-series-forecasting-eda-fe-modelling/

Material and Methods:

•	Dataset:

The M5 dataset provides the unit sales of various products sold in the USA, organized in the form of grouped time series. This dataset consists of 3049 products, classified into 3 categories (Hobbies, Foods, and Households) and 7 product departments. These products are sold across 10 stores in 3 states (California, Texas, and Wisconsin). With this dataset, we can do an exploratory data analysis across different aggregation levels. Besides the time series data, this dataset also includes explanatory variables such as price, promotions, day of the week, and special events (e.g., Super Bowl, Valentine’s Day, and Orthodox Easter), which will also allow us to analyze how these events affect sales. The results obtained from the analysis of this dataset will be scalable as the same methods could be applied to gain insights for other products, departments, stores, and regions.

The dataset comprises of:

1.	calendar.csv - Contains information about the dates on which the products are sold. [1]

•	date: The date in a “y-m-d” format.

•	wm_yr_wk: The id of the week the date belongs to.

•	weekday: The type of the day (Saturday, Sunday, …, Friday).

•	wday: The id of the weekday, starting from Saturday.

•	month: The month of the date.

•	year: The year of the date.

•	event_name_1: If the date includes an event, the name of this event.

•	event_type_1: If the date includes an event, the type of this event.

•	event_name_2: If the date includes a second event, the name of this event.

•	event_type_2: If the date includes a second event, the type of this event.

•	snap_CA, snap_TX, and snap_WI: A binary variable (0 or 1) indicating whether the stores of CA, TX or WI allow SNAP purchases on the examined date. 1 indicates that SNAP purchases are allowed.

2.	sales_train_validation.csv - Contains the historical daily unit sales data per product and store [1]

•	item_id: The id of the product.

•	dept_id: The id of the department the product belongs to.

•	cat_id: The id of the category the product belongs to.

•	store_id: The id of the store where the product is sold.

•	state_id: The State where the store is located.

•	d_1, d_2, …, d_i, … d_1941: The number of units sold at day i, starting from 2011-01-29.

3.	sell_prices.csv - Contains information about the price of the products sold per store and date. [1]

•	store_id: The id of the store where the product is sold. 

•	item_id: The id of the product.

•	wm_yr_wk: The id of the week.

•	sell_price: The price of the product for the given week/store. The price is provided per week (average across seven days). If not available, this means that the product was not sold during the examined week. Note that although prices are constant at weekly basis, they may change through time (both training and test set).

4.	sales_train_evaluation.csv - Includes sales. [1]

•	Methods:

The first step in the process is data pre-processing, which comprises melting data, combining data from various sources, handling the missing values, and so on. There is no concept of input and output variables in a time series. The given time series must be first reframed as a supervised machine learning problem by using feature engineering techniques like but not limited to mean or median encodings, lag featuring, rolling window featuring, expanding window featuring, and so on. The next step is the application of supervised machine learning algorithms for generating predictions. We will be training models using machine learning techniques like but not limited to linear regression, random forest regression, light gradient boosting machine regression, and so on. We will be using Dask or Apache Spark for data pre-processing. We will be working with scikit-learn for modeling and prediction.

References: 

[1]. https://mofc.unic.ac.cy/m5-competition/

