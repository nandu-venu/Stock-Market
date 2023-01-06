
# 1. Introduction

## 1.1	What are the stock exchanges? 
Stock exchanges are marketplaces in which U.S. financial securities, commodities, derivatives and other financial instruments are traded. While in the past,
traders and brokers used to meet physically in a stock exchange building to trade stocks, now most of the financial trading happens electronically and 
automatically. The two major U.S. financial securities markets are the New York Stock Exchange and Nasdaq. There are around hundreds of companies listed 
between these two exchanges.

## 1.2	Project Motivation
COVID-19 drastically impacted the stock exchanges and markets in almost all sectors of industry. Therefore, organizations had to adjust their strategies depending 
on their respective markets. Additionally, predicting stock prices over a longer time horizon became more challenging due to the impact of the pandemic creating 
variability in stock prices. Therefore, we aimed to use forecasting methods to develop a more precise short-term forecast for stocks. 

## 1.3	Project Goal
The goal of this project was to select four organizations, each from a different segment of industry. Then, we planned to build forecasting models to accurately 
predict stock prices for each organization in the short term. Finally, we planned to build an R Shiny application to provide real-time forecasts for the next 
trading period. 


## 1.4	Dataset Description and Preprocessing 
We first collected data via the Yahoo Finance API. This raw data was converted to XTS objects to ensure uniform handling of non-continuous temporal data. The 
datasets each contained the variables Date, Opening Price, Closing Price, High, Low, and Volume. We chose the Closing Price variable to build our respective models. 
Each team member focused on a different company’s stock: Google, Tesla, Amazon, and Ford. We discovered that each selected stock fell by a minimum of 50% upon the 
start of the pandemic in 2020 followed by a recovery several months later. Based on these observations, we chose to analyze post-COVID recovery data to ensure that 
a reliable model was produced. We carefully selected training and testing datasets for each stock to minimize noise. 

## 1.5	Selected Stocks

•	Amazon (AMZN)
•	Tesla (TSLA)
•	Google (GOOG)
•	Ford (F)


# 2. Analysis

## 2.1	Naive
The naïve forecasting method was found to produce reasonable forecasts within a small testing period (e.g. one week). However, this model cannot account for 
internal fluctuations in stock prices caused from buying and selling. Because of this, we determined that better models could be found to account for fluctuation
and short-term trends. 
  
## 2.2	Regression
We next looked at linear regression models for each stock. These models captured short-term trend but again did not account for volume of stocks exchanged. 
The naïve method was more accurate than the regression method for short term prediction. 

## 2.3	Rolling Arima
A rolling ARIMA model was used for each selected stock. The training window was two weeks, moving forward with each subsequent forecast. We found this
prediction accuracy to be much better than the naïve method for short- to medium-term forecasting. 

## 2.4	Simple Neural Networks
Using simple neural networks allowed us to capture short-term trend and daily buying/selling relatively well when compared to ETS and regression methods. It was 
found to be useful for medium- to short-term forecasts. 

## 2.5	Deep Learning
We fitted a deep learning model containing four layers and 16 to 32 nodes for each individual stock. For Ford and Google, the DL models captured short-term 
volume and trend quite well. However, for Amazon we noticed a potential risk in overfitting the data depending on the training period selected. 

## 2.6	Accuracy Table for Model Forecasts
Incorporating the feedback provided during the final project presentation, we computed the average MAPE values for each method by taking the average with 
rolling training and testing set. In essence, each model was tested with different training and test sets and the MAPE values were averaged. Consider the table 
below to view the average MAPE values.

Model	Google	Tesla	Ford	Amazon
Naive	3.46	8.27	5.05	5.8
Regression	4.38	14.53	7.85	8.1
Rolling Arima	3.40	8.30	4.24	5.21
Simple NN	4.16	9.55	5.95	8.61
Deep Learning	2.71	11.13	5.55	129.33

## 2.7	Selected Models for Each Stock
•	The best model for Google is Deep Learning
•	The best model for Tesla is Naive
•	The best model for Amazon is Rolling Arima
•	The best model for Ford is Rolling Arima

# 3. R Shiny App

## 3.1	What is R Shiny?
Shiny is an R package that enables building interactive web applications that can execute R code on the backend. With Shiny, you can host standalone applications 
on a webpage, embed interactive charts in R Markdown documents, or build dashboards. An R Shiny application has three major components. Shiny applications have two 
components, a user interface object and a server function, that are passed as arguments to the shinyApp function that creates a Shiny app object from this UI/server 
pair. 

## 3.2	Building Stock Predictor R Shiny
The user interface was built to accommodate the design our group agreed upon. After the UI code was done, we moved to create the server side of the application. 
As most of the graphs require model definition and forecasting, we decided to create stand-alone functions for each graph. Once each function was defined, we 
utilized if else statements to run a function if user input was established. The application has three sections. The first section opens up an interactive plot 
with the actual stock prices. You may zoom and analyze the impact of Covid-19 on each of the four graphs. Furthermore, the interactive visualization updates itself 
every day with the updated stock price for that trading day. The second section of the application describes the analysis described in Chapter 2 of this report. 
Finally, the third section provides real-time forecasts for the current trading day’s closing price. By hitting the submit button, the backend code will compute 
the expected closing price. 

## 3.3	Completed R Shiny Application
Kindly refer to the figure below to view the completed application. You may also visit https://sirinabraham.shinyapps.io/Stock_Price_Predictor/ to explore and use 
the application.

# 4. Conclusion

## 4.1	Fulfilled Goals

A reliable model for forecasting short-term stock prices was found for each selected stock as seen in Chapter 2. Furthermore, an R Shiny web application was 
deployed to provide real-time forecasts for the next trading day.

https://sirinabraham.shinyapps.io/Stock_Price_Predictor/


## 4.2	Lessons Learned

Our team learned quite a few valuable lessons from our semester project. First, it is important to choose appropriate training periods when looking at data 
due to constantly changing stock trends. Models with shorter training periods are generally more accurate than those with longer training periods due to 
inherent data fluctuation. Additionally, the inherent volatility of the market is proven by naïve forecasts which provide acceptable MAPE values. 
Furthermore, stock prices are impacted by external factors including macroeconomic trends, sentiment, government policies, and more. Finally, a good prediction 
model should serve as a decision support tool rather than a decision-making tool for the analyst. 

## 4.3	Next Steps

For potential future applications of this project, models could be built incorporating other features such as the company’s historic growth rate, future expected earnings, macroeconomic trends, etc. to improve model accuracy. Also, more sophisticated deep learning models could be explored such as long short-term memory (LSTM) algorithms. Additionally, day trading data could be back-tested with the prediction models to simulate profitability. Deep learning models could be added to the R Shiny app as well. 
