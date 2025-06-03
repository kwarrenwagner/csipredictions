# csipredictions
Forecasting Consumer Sentiment Index
Using Google Trends and Macroeconomic Data
Jacob Richman, Kenji Wagner, Andrew Ye
University of Michigan

1 Introduction
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
