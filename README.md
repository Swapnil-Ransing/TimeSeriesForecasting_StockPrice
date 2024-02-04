# Stock Price Prediction Using LSTM
## Overview
A stock market is a public market where you can buy and sell shares for publicly listed companies. The stocks, also known as equities, represent ownership in the company. 

Stock Price Prediction helps to discover the future value of company stock. The entire idea of predicting stock prices is to gain significant profits. Predicting how the stock market will perform is a hard task to do. There are other factors involved in the prediction, such as physical and psychological factors, rational and irrational behavior, and so on. All these factors combine to make share prices dynamic and volatile. This makes it very difficult to predict stock prices with high accuracy. 

There are multiple statistics, mathematical, machine learning etc. models to predict the stock price. In this project long short term memory (LSTM) network deep learning model is being explored to accurately predict the stock price on the time series data. Along with the prediction, extrapolation is also being demonstrated.

## ICICIBANK stock price prediction
### Getting the historical data
ICICIBANK is NSE listed stock. Yahoo finance [yfinance](https://pypi.org/project/yfinance/) api is being used to get the stocks historical data. This consisted of open, high, low, close, adj. close prices and volume for each trading date. If we are extrapolation the data for future date, the only reference we will have in time series generator is of previous day close price. For this reason, we will only use Close price of stock.

### Data preprocessing and featurization
Model is trained on the recent two years data. This is because the historical price trend will not be useful in predicting the trend and training the model. Model developed on the recent data has shown a good match for predictions.
Then data is checked for any Nan values and any Nan value rows if present, are deleted. 

![ICICIBANK Close Price Image](https://github.com/Swapnil-Ransing/TimeSeriesForecasting_StockPrice/blob/main/Images/ICICIBankClosePrice.JPG)

For featurization following technical indicators were used:
1. 7 day moving average
2. 21 day moving average
3. 50 day moving average
4. 26 day exponential moving average
5. 50 day exponential moving average
6. 12 day exponential moving average
7. Moving average convergence divergence (MACD)
8. Bollinger band: 20 day standard deviation
9. Bollinger bands upper band : 20 day mean + (20 day standard deviation *2 )
10. Bollinger bands lower band : 20 day mean - (20 day standard deviation *2 )
11. Exponentioal moving average
12. momentum

Following is a final featurized dataframe:
![ICICIBankFeaturizaedDf](https://github.com/Swapnil-Ransing/TimeSeriesForecasting_StockPrice/blob/main/Images/ICICIBankFeaturizaedDf.JPG)

### Train test data split and normalization
Last one months data is considered to be test data, rest is considered as the train data.
Also as we will be generating the time series, last 30 days of train observations are also concatednated at the top of test data. This 30 days are the look back period. Details about time series generator and look back period is mentioned in the next section.

Close price is the target variable. Further y_train, y_test consists of target variable and rest of the columns are present in the X_train and X_test dataframes.
Data normalization is performed using MinMaxScaler. MinMaxScaler is used for X_train dataframe and is transformed on the X_test dataframe.

### Time series generator
[Keras time series generator](https://www.tensorflow.org/api_docs/python/tf/keras/preprocessing/sequence/TimeseriesGenerator) is used to generate the structured data for predicting the target. Basic idea is to look X_train samples equals to look back period to predict a single target. Look back period value of 30 is being used which indicates, 30 X_train samples are used to predict the 31st y_train target. This data structure is formed using the time series generator for train and test datasets. This was also the reason of adding last 30 samples from the train dataset at the test dataset top.

### Model training
Following sequential model is being used to train the model:
![LSTMModelSummary](https://github.com/Swapnil-Ransing/TimeSeriesForecasting_StockPrice/blob/main/Images/LSTMModelSummary.JPG)
Following mean squared error and mean absolute error were obtained after the model train:
![LSTMModelTrain](https://github.com/Swapnil-Ransing/TimeSeriesForecasting_StockPrice/blob/main/Images/LSTMModelTrain.JPG)

### Model Predictions and Extrapolating the results
Model predictions were computed on the test data from the trained model. For model predictions we used the actual close (target) price from the historical data. However in the actual scenario close price also should be predicted from the model. Extrapolation is refered to the procedure where each day close price is predicted based on the trained model fitted on the previous samples and once the close price is obtained, it is being integrated in the extrapolation sample data for next day prediction.

Following are the model prediction and extrapolation results were obtained:
![PredictionResults](https://github.com/Swapnil-Ransing/TimeSeriesForecasting_StockPrice/blob/main/Images/PredictionResults.JPG)
![PredictionAndExtrapolationResults](https://github.com/Swapnil-Ransing/TimeSeriesForecasting_StockPrice/blob/main/Images/PredictionAndExtrapolationResults.JPG)

## Observations and Conclusions :
1. Time series generator is being used to generate the data suitable for time series forecast and LSTM model.
2. LSTM model is being used for price prediction.
3. mean squared error and mena absolute error, did not show  much improvement with the training for higher epochs.
4. Model prediction shown a trend match with the true values however, extrapolation results were not in alignment with true values.




