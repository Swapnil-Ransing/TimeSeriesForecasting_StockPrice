# Stock Price Prediction Using LSTM
## Overview
A stock market is a public market where you can buy and sell shares for publicly listed companies. The stocks, also known as equities, represent ownership in the company. 

Stock Price Prediction helps to discover the future value of company stock. The entire idea of predicting stock prices is to gain significant profits. Predicting how the stock market will perform is a hard task to do. There are other factors involved in the prediction, such as physical and psychological factors, rational and irrational behavior, and so on. All these factors combine to make share prices dynamic and volatile. This makes it very difficult to predict stock prices with high accuracy. 

There are multiple statistics, mathematical, machine learning etc. models to predict the stock price. In this project long short term memory (LSTM) network deep learning model is being explored to accurately predict the stock price on the time series data. Along with the prediction, extrapolation is also being demonstrated.

## ICICIBANK stock price prediction
### Getting the historical data
ICICIBANK is NSE listed stock. Yahoo finance [yfinance](https://pypi.org/project/yfinance/) api is being used to get the stocks historical data. This consisted of open, high, low, close, adj. close prices and volume for each trading date. If we are extrapolation the data for future date, the only reference we will have in time series generator is of previous day close price. For this reason, we will only use Close price of stock.

## Data preprocessing and featurization
Model is trained on the recent two years data. This is because the historical price trend will not be useful in predicting the trend and training the model. Model developed on the recent data has shown a good match for predictions.
Then data is checked for any Nan values and any Nan value rows if present, are deleted. 




