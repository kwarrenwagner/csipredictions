# Forecasting Consumer Sentiment Index Using Google Trends and Macroeconomic Data
By Kenji Wagner, Jacob Richman, Andrew Ye

# 1 Introduction

The University of Michigan Consumer Sentiment
Index (CSI) is a survey that measures how
consumers feel about their future financial
situation. CSI is a popular economic indicator that
serves as a proxy estimate of future economic
growth. Implicitly, the more confident that
consumers are in the economy, their job, and their
income, the more likely they are to spend money
in the economy. Our project intends predict the
United States Consumer Sentiment Index
(CSI) using both Google search trends and
economic indicators, with the intent of
understanding underlying factors of a
consumer’ confidence in the economy and to
give highly precise CSI estimates. The
Consumer Sentiment Index is a measurement of
human behavior and how consumers feel about
the economy, not necessarily how the current
economic condition is from an objective
perspective. The metric of Consumer Sentiment is
highly relevant to human behavior as a reaction to
economic and financial conditions. Hence, we
believe that with the right selection of keywords
in Google search trends and macroeconomic
indicators, we can leverage time series regression
models such as AutoRegressive Integrated
Moving Average (ARIMA), Vector Auto
Regression (VAR), and Mixed Data Sampling
(MIDAS) models to extract the underlying
sentiment of the average consumer on their
current and future economic position. While
others (Choi H. (n.d.)) have worked in similar
designs before, this will be the first model to using
both Google Trends and Economic Indicators in
the United States with contemporary keywords
selection. We developed a highly accurate model
using VAR and 6 predictors with an R^2 of 0.972
and RSE of 2.08 for 2020 to 2024 testing. This
paper will first provide an overview for other
work, then dive into how we extract the data and
developed the model. Then we will discuss their
performance and some potential ethical concerns.

# 2 Related Work
In exploring methodology to ultimately predict
CSI, our research has been informed by a selection
of literature, closely related to our approach. Three
research stood out in providing guidance for our
model, those being “Using Machine Learning
Methods to Predict Consumer Confidence”,
“Consumer Sentiment with Google Trends”, and
“Predicting the Present with Google Trends”.
In “Using Machine Learning Methods to Predict
Consumer Confidence”, Han, Li, and Li (2023)
present an analysis of the Consumer Confidence
Index (CCI) in China, utilizing a variety of
machine learning and deep learning techniques,
including several neural network architectures and
Random Forest, with data sourced from search
engines. This study proved valuable in offering a
diverse set of computational methods and in
suggesting important search term categories that
might correlate with consumer sentiment metrics.
While CCI and CSI differ—CCI being more
focused on economic confidence and CSI on
purchasing attitudes towards household goods—
the overlap between them has informed our
selection of relevant search terms for our predictive
model. “Consumer Sentiment with Google Trends” was
a Google study that constructed a CSI prediction
model utilizing Google Trends data. In said piece,
Choi H. (n.d.) split Google Search Trends data
into categories corresponding to the five
underlying questions of the CSI. By identifying
search queries with strong correlations to the time
series data of each question, they were able to
regress these trends to forecast the CSI,
potentially employing autoregressive models.
This approach parallels our utilization of Google
Trends for CSI prediction. However, our model is
distinct in its use of varying regression techniques
and the integration of macroeconomic data to
enrich the analysis.
Lastly, we examined a paper “Predicting the
Present with Google Trends”, that leveraged
Google Trends data for real-time (“nowcasting”)
predictions of various economic indicators. In this
work, Choi and Varian demonstrated the potential
for timely estimations of economic conditions
such as unemployment rates, tourism statistics,
and general consumer confidence by carefully
curating categories provided by Google Trends.
While there are similarities to our approach in
terms of employing time series regression and the
predictive use of Google Trends, our methodology
diverges by incorporating macroeconomic
variables and favoring Vector Autoregression,
MIDAS regression over simpler autoregressive
models to enhance the accuracy and robustness of
our predictions.
These studies reviewed have provided
foundational insights that guide our approach to
predicting CSI; they underscore the significance
of selecting pertinent search terms, the value of
incorporating real-time search data, and the need
for sophisticated modeling techniques to account
for the multifaceted nature of economic
indicators. Our model aims to utilize these
learnings with our own innovations to produce a
reliable predictive tool for CSI.

# 3 Data
Our data come from three different sources:
Google Trends, Federal Reserve Economic Data
(FRED), and Yahoo Finance. They were collected
in the first week of April 2024 from 2004 to 2024.
A total of 60 variables were collected, and 3 were
used in the final Vector Auto Regression model.
Table 1 provides an overview of all variables
tested. We selected these variables based on the
questions of the CSI survey and prior research
works. We also selected these variables based on
the understanding of the domains.

Sources         Variables Tested

Google Trends   “inflation”, “unemployment”, “interest rate”,”rental housing” , “job opening”, “economy”, “tourism”, “layoff”, “employment”, “debt management”, “rent”, “wages”, “real estate”, “used car”, “gas price”, “recession”, “housing market”, “tax cut”, “federal reserve”

FRED Monthly   Total Healthcare Construction Spending, One-Year Real Interest Rate, Two Year Expected Inflation Rate, Inventory to Sales Ratio, Total
Utility Capacity Index, AP Grade A Egg Price,
12-Month Moving Average of Unweighted
Median Hourly Wage Growth: Age: 16-24
Years, Inflation Expectation, 30-Day AA
Financial Commercial Paper Interest Rate, 60-
Day AA Financial Commercial Paper Interest
Rate, 90-Day AA Financial Commercial Paper
Interest Rate, 30-Day AA Nonfinancial
Commercial Paper Interest Rate, 60-Day AA
Nonfinancial Commercial Paper Interest Rate,
AD&Co US Mortgage High Yield Index,
Credit-and-Option-Adjusted Spread: Mid-Tier,
AD&Co US Mortgage High Yield Index,
Credit-and-Option-Adjusted Spread: Tier 0 (1
,2,3), 12-Month Moving Average of
Unweighted Median Hourly Wage Growth:
Wage Distribution: 1st to 25th (25th-50th, 50th-
75th, 75th-100th) Wage Percentile, Total
V ehicle Sales, 3-Month Median Salary,
AD&Co US Mortgage High Yield Index: Tier 0
(1)


Table 1: Overview of All Tested Variables
*parentheses contain extra variables

We utilized different techniques to extract
information from various sources. Google Trends
limits the download of keywords to 5 for each
request and performs a normalization between
them to make it more comparable for use.
However, this process can make the data less useful
for machine learning algorithms. A
denormalization process was performed using the
R package gtrendsR with anchor terms “white,”
“blue,” “coca cola,” “seaweed,” and
“perspicacious,” which remain relatively constant
on Google Trends over time. These variables
provide a reference to denormalize data and make
them more comparable and approximate the
absolute interests.
For Yahoo Finance data, we calculated the
absolute difference between each trading period,
defined as a week or month. We used the simple
calculation of close - opening to gather information
on the fluctuation of the market. We did not
perform additional manipulation on FRED data.
