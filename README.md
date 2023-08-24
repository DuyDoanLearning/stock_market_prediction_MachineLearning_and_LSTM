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

### Correlation test
![](https://github.com/DuyDoanLearning/stock_market_prediction_MachineLearning_and_LSTM/blob/Stock-Prediction/Images/Correlation_Test_1.png)

After EDA, the two most potential variables are **_SP500_** and **_Spot price of Palladium_**. We will also include SHSZ_CSI_300 in a representative of China's stock indices.

![](https://github.com/DuyDoanLearning/stock_market_prediction_MachineLearning_and_LSTM/blob/Stock-Prediction/Images/Correlation_Test_2.png)

The Ridge and Lasso will be added to avoid multicollinearity in the regression task.

### Feature Extraction
To confirm the proposed variables are meaningful in predicting tomorrow's price and the cointegration form a long-run linear relationship, we will test at price and lag levels (from 1 to 5). We will also add differencing and returns of variables.

Set of variables include:
- Natural logarithm of return and 1 - 5 days diffs (predict log return then transfer back to price)
- Diff / Return / Lag of 1 - 5 of input features
- Lag version only from 1 - 5
- Univariate (only target variable) and multivariate (combination of input features and extracted features)

I hypothesize that the linear will perform best, as Engle-Granger (1987) stated that the relationship should be linear.

## Results of ML models
- Use lag/return/diff of 5
![](https://github.com/DuyDoanLearning/stock_market_prediction_MachineLearning_and_LSTM/blob/Stock-Prediction/Images/results_log%20ret%20diff.png)

- Use Lag only
![](https://github.com/DuyDoanLearning/stock_market_prediction_MachineLearning_and_LSTM/blob/Stock-Prediction/Images/results_img_lag%20only.png)

- Use original values (Without any extract features)
![](https://github.com/DuyDoanLearning/stock_market_prediction_MachineLearning_and_LSTM/blob/Stock-Prediction/Images/Original_values.png)

The models perform better when we input lag, return, and price differencing of relevant international stock indices and commodity prices
![](https://github.com/DuyDoanLearning/stock_market_prediction_MachineLearning_and_LSTM/blob/Stock-Prediction/Images/results_img_prediction_multi.png)

Taking a closer look, we can see it performs quite well on replicating the stock movements:
![](https://github.com/DuyDoanLearning/stock_market_prediction_MachineLearning_and_LSTM/blob/Stock-Prediction/Images/results_img_lag%20only_closer.png)

- Use the natural logarithm of return and differencing
![](https://github.com/DuyDoanLearning/stock_market_prediction_MachineLearning_and_LSTM/blob/Stock-Prediction/Images/result_img_coint_prediction.png)

The error is deficient, and the result nearly fits 100% with a very small error:
![](https://github.com/DuyDoanLearning/stock_market_prediction_MachineLearning_and_LSTM/blob/Stock-Prediction/Images/results_table_log_diff%20version.png)

This proved that the Engle-Granger models in predicting the delta of the target variable can be achieved through the delta of predictors and its' coefficient. 

## Results of DL models
LSTM models do not work well due to being too complicated, while the long-run relationship between cointegrated variables is simple and linear. Furthermore, adding more global financial market variables will not improve the model performance but worsen it it.

- Univariate predictions:
![](https://github.com/DuyDoanLearning/stock_market_prediction_MachineLearning_and_LSTM/blob/Stock-Prediction/Images/results_lstm_uni.png)

- Multivariate predictions:
![](https://github.com/DuyDoanLearning/stock_market_prediction_MachineLearning_and_LSTM/blob/Stock-Prediction/Images/results_img_multi_lstm.png)

## Conclusions
ML models can recognize simple relationships better than DL. Linear regression performs best in predicting tomorrow's stock price. The proposed features can achieve low errors. The technical indicators generated directly from the price give us lower error results.

However, the log_diff version gave us excellent results, proving that based on the error correction model by Engle-Granger (1987), we should predict the log return of the price instead of directly predicting the true absolute price.

