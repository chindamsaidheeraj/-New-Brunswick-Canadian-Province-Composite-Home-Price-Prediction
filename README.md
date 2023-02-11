# -New-Brunswick-Canadian-Province-Composite-Home-Price-Prediction

# 1. Introduction

Prediction of home prices helps real estate companies and government entities to reinforce 
their existing strategies with respect to their goals and expectations. For provincial or 
central governments in order to release any welfare schemes or help citizens to reduce the 
housing prices load it is essential to understand the outcomes that might happen in future 
and be prepared in advance. For businesses like real estate and housing their business 
models are driven by the future predictions in the industry.

# 2. Problem Statement

Develop a best performing machine learning model which can effectively predict Composite 
HPI (Home price index) with minimal error for the province New Brunswick.

# 3. Approach

In order to solve this use case temporal data sets are utilized and two time series models 
were developed and evaluated against each other in order to obtain best working model 
that solves the problem.
Data sets utilised in this project:

 Since the project goal is to predict HPI data so Composite HPI Data [1] for the
province New Brunswick from January 2005 to November 2022 was utilized.

 Since the CPI and HPI are directly related so static total cpi change data [2] from 
January 2005 to November 2022 was utilised.

Time Series models utilized in this implementation are as follows

 ARIMA (Auto regressive moving average model)

 VAR (Vector auto regression model).

# 4. Analysis and implementation

In general, home price index helps to understand the variations involved in builder’s selling 
prices of residential houses where in the specifications will remain same between two 
consecutive periods. This will be analysed based on a monthly series. The Consumer Price 
Index (CPI) [2] is an indicator of changes in consumer prices experienced by Canadians. It is 
obtained by comparing, over time, the cost of a fixed basket of goods and services 
purchased by consumers. The CPI is widely used as an indicator of the change in the general 
level of consumer prices or the rate of inflation [2]. Since the purchasing power of money is 
affected by changes in prices, the CPI is useful to virtually all Canadians.

## 4.1 Reasons for choosing time series models

Since the data points involved vary across time in this use case which indicates temporal 
data so time series models are implemented.

## 4.2 Implementation of ARIMA model

### 4.2.1. Why ARIMA Model was used?

ARIMA works better on temporal data which have stationary characteristics. ARIMA takes in 
to consideration of time component by regressing previous time stamps and errors of time 
stamps this would help to have good predictions for temporal data.
Main components involved for ARIMA are as follows:

AR: The time series is regressed with its previous values i.e., y(t-1), y(t-2) etc. The order of 
the lag is denoted as p.

I: The time series uses differencing to make it stationary. The order of the difference is 
denoted as D.

MA: The time series is regressed with residuals of the past observations i.e., error ε(t-1), 
error ε(t-2) etc. The order of the error lag is denoted as q.

### 4.2.2. Data set for ARIMA Implementation:

Composite HPI Data [1] for the province New Brunswick.

Training Data Set: 202 months, Test Data Set Size: 12 months

Selection of p and q was done by using 2 approaches, best p and q values are obtained from 
grid search.

 PACF and ACF graphs.

 Grid search using BIC and AIC values.

Features utilised from the dataset are “Date” and “Composite_HPI_S.”

Results

RMSE- 9.756
Normalised RMSE-0.328

In ARIMA, Univariate data was utilised in order to build prediction model for SPI.

## 4.3. Vector auto regression Model implementation (VAR)

### 4.3.1. Reason for using VAR

Although ARIMA gives good results on stationary data but one of the disadvantages of simple ARIMA model is it can handle only univariate data. In many real-world predictions use cases there can be one variable affecting the cause of another variable or predictions are affected by external data so in order to handle this scenarios vector auto regression can be used. This implementation helps to understand whether if there is any external effect on HPI predictions and helps to improve overall predictions.

In VAR, each variable depends not only on its own values but also has some dependency on other variables. This dependency is used for forecasting future values. Let us consider below bi variate equation.

### 4.3.2. Data sets utilized for Implementation: Composite HPI Data [1] for the province New Brunswick and CPI Data [2].

Training Data Set size: 200 months Test Data Set Size:  13 months

Features Utilized from the datasets are “Date”, “Composite_HPI_S” and “STATIC_TOTAL_CPI_CHANGE” (T5otal cpi percentage change)

### 4.3.3. Granger Causality Tests [3]:  These tests will help to understand whether one variable granger causes another variable in time series modelling. This hypothesis can be evaluated by many statistical tests.

### 4.3.4. Relation between CPI and HP (why to use CPI Data?):

Increase in home costs would have direct impact on neighbourhood affordability and house hold wealth. CPI mainly involves in measuring overall prices of house hold basket of services of services and goods in which housing is a larger component. So, CPI and HPI are directly proportional to each other. Results of granger causality tests have the p values less than alpha which rejects the null hypothesis of static total cpi change does not granger cause HPI and proves that there is some (cause and effect) relationship between them.

![image](https://user-images.githubusercontent.com/46736656/218235313-a7adb6f1-590a-413a-8d48-5c11d7b6cffb.png)

 
 Stationarity was obtained after first order differencing. After random exploration for finding optimal results lag 4 provided optimal results.
 
 ### Results

![image](https://user-images.githubusercontent.com/46736656/218235345-5da04236-dcb3-49ff-9e2a-e244e6f64da3.png)

# 5. Conclusion and Evaluation of results

![image](https://user-images.githubusercontent.com/46736656/218235400-2c3f39e8-0648-4f78-b829-79cf3519dbcc.png)


In this specific use case based on above results in table 3. Vector auto regression model performed better than ARIMA. Since ARIMA has utilised univariate data, it did not consider external data which resulted in less performance. The granger causality tests ‘p’ values less than the alpha (rejecting null hypothesis of CPI does not granger cause HPI) clearly indicates the impact of CPI on HPI so model was developed with consideration of external variables along with its own values which eventually helped VAR model perform better than ARIMA.

# 6. References

[1] https://www.crea.ca/housing-market-stats/mls-home-price-index/hpi-tool/
[2] https://www.bankofcanada.ca/rates/price-indexes/cpi/#cpi-total
[3] https://www.analyticsvidhya.com/blog/2018/09/multivariate-time-series-guide-forecasting-modeling-python-codes/




