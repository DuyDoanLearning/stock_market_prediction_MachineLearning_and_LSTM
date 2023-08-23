# stock_market_prediction_MachineLearning_and_LSTM
A dissertation project for MSc Financial Technology at the University of Nottingham. This time series project takes input features cointegrated with the target variables and examines different ML models' performance.

## Overview of the project
This project aims to test the hypothesis of cointegration variables. Due to globalization, international financial markets are more cointegrated than ever. When one market experiences a shock or a growth, others are likely to co-move with it. Since there are differences in the closing times of markets' trading days, we can use this as an advantage to obtain meaningful information to predict tomorrow's price for our focused market. For example, the US closed its trading time 12 hours before the closing time of the Vietnam market. The question we are trying to answer here is whether global stock indices, commodities prices, and exchange rates can improve the performance of ML and DL models in predicting future prices. My main task in this project is regression, where I tried to predict the true price of VN-Index and examine how models perform with proposed variables.

## Some words about literature review
Much research has been done to explore the cointegration movement of the Vietnam stock index (VN-index) with the global financial markets:
- The VN-Index has a high correlation and is cointegrated with the stock indices of China, the US, and Singapore. However, the degree of cointegration varies through time.
- The VN-Index has some cointegration with the oil, gold, and palladium prices.
- The exchange rates between Vietnam and its major trading partners, China and the US, can influence the movement of the stock markets.
With this literature researched and reviewed, these variables can be meaningful in predicting tomorrow's price of the VN-Index. Furthermore, we can take this advantage for further trading due to differences in the market's closing time.

## Data
The data includes variables that fall into the following categories: Global stock indices, Commodity prices (precious metals and oil), and exchange rates. The data is downloaded from Bloomberg, from 02/02/2007 to 30/06/2023, with 16 input features.

## EDA and Feature selection
In this project, we will clean the data and take a look at variables that have these factors:
- Medium to high correlation with the target variable
- Survive the Augmented Dickey-Fuller test for stationarity and Granger's causality test

After EDA, the two most potential variables are **_SP500_** and **_Spot price of Palladium_**
