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
2 Related Work
In exploring methodology to ultimately predict
CSI, our research has been informed by a selection
of literature, closely related to our approach. Three
research stood out in providing guidance for our
model, those being “Using Machine Learning
Methods to Predict Consumer Confidence”,
“Consumer Sentiment with Google Trends”, and
“Predicting the Present with Google Trends”
.
In “Using Machine Learning Methods to Predict
Consumer Confidence”
, Han, Li, and Li (2023)
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
model.
1
“Consumer Sentiment with Google Trends” was
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
3 Data
Our data come from three different sources:
Google Trends, Federal Reserve Economic Data
(FRED), and Yahoo Finance. They were collected
in the first week of April 2024 from 2004 to 2024.
A total of 60 variables were collected, and 3 were
used in the final Vector Auto Regression model.
Table 1 provides an overview of all variables
tested. We selected these variables based on the
2
questions of the CSI survey and prior research
works. We also selected these variables based on
the understanding of the domains.
Sources Variables Tested
Google
Trends
“inflation”, “unemployment”, “interest rate”,”
rental housing”
, “job opening”, “economy”
,
“tourism”, “layoff”, “employment”, “debt
management”, “rent”, “wages”, “real estate”,
“used car”, “gas price”, “recession”, “housing
market”, “tax cut”, “federal reserve”
FRED
Monthly
Total Healthcare Construction Spending, One-
Y ear Real Interest Rate, Two Y ear Expected
Inflation Rate, Inventory to Sales Ratio, Total
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
FRED
W eekly
Federal Funds Rate, US Regular Conventional
Gas Price, US Regular Reformulated Gas Price,
Insured Unemployment Rate, Chicago Fed
National Financial Conditions Leverage
Subindex, St. Louis Fed Financial Stress Index
Yahoo
Finance
S&P 500, CBOE VIX
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
4 Methods
We employed various techniques to select the best
variables for our model. Two statistical tests were
performed, in addition to a visual analysis.
4.1 Visual Analysis
We performed a visual analysis for variable itself
by plotting CSI with each variable of interest to
qualitatively understand if a potential variable
would be useful for making predictions. Some
variables were removed from this test due to
confounding factors from other events. For
example, the outbreak of the COVID-19 influences
the “employment” keyword and unemployment
rate. “gas price” was also influenced by the
outbreak of the Ukraine war. Using the domain
knowledge combining the relevant news we
removed the candidates that had significant
confounding influences.
The ideal candidate will show an either negative
or positive correlation with the CSI variable. As
demonstrated by Figure 1. To quantify this impact,
we performed the cross-correlation test.
4.2 Cross-Correlation Test
We used the sample cross-correlation function
(CCF) to identify correlating lags of our candidate
variables to CSI. We set the maximum lag to 30 to
be as exhaustive as possible. We operated this after
understanding the stationarities of the candidates,
i.e., the mean, variance, and autocorrelation
structure do not change over time. The CCF
function will output an array of values that are
between -1.0 and 1.0, where an ideal candidate will
have a value closer to the boundary and has a
negative association when closer to lag 0. This is
an indication of a lagging variable having the
potential of predicting a future variable, which is
consistent with what can be done in real life (using
past data to predict the future data) Figure 2 shows
the "mortgage-rate" from Google Trends that has a
potential of predicting the CSI and serves as a
reference of what an ideal candidate looks like.
Figure 2: CCF Result of Mortgage Rate and CSI
4.3 Granger’s Causality Test
Granger’s Causality is a test to determine if a
candidate has the potential of being used to forecast
a time series. This statistical test uses the prior
values of the candidate time series to test the causal
effects on the future CSI values. We used lags = 1,
2, 3 for the purpose of testing lags and obtained the
F-statistics by comparing these two time series.
For null hypothesis:
Figure 1: Visual Analysis of CSI and Mortgage Rate
𝑦! = 𝑎" + 𝑎#𝑦!$# + 𝑎%𝑦!$% + ⋯ 𝑎&𝑦!$& + 𝜀!
(1)
For alternative hypothesis:
𝑦! = 𝑎" + 𝑎#𝑦!$# + 𝑎%𝑦!$% + ⋯ 𝑎&𝑦!$&
+ 𝑏'𝑥!$' + ⋯ 𝑏'𝑥!$( + 𝜀!
(2)
3
The alternative hypothesis includes augmented
variables from the candidate series, where p
stands for the nearest lag and q stands for the
furthest lag.
We set the p-value threshold to 0.05, and Table
2 lists the variables we found to be statistically
significant.
Variable Mean p-value
Mortgage Rate (Google Trend) 0.002
Bankruptcy (Google Trend) 0.019
Employment (Google Trend) 0.023
Used Car (Google Trend) 0.026
Rental Housing (Google Trend) 0.029
Total Vehicle Sales (FRED) 0.003
Table 2: Granger’s Causality Test
understanding and interpretation of our
parameters, which is crucial for an initial
exploratory analysis. Secondly, starting with a
baseline ARIMA model allows for the
establishment of a benchmark against which the
performance of more complex models can be
measured.
In evaluating our model, we employed a 1-step
ahead forecasting system, where after each
forecast is made, the model parameters are refit
with all the previous data. This method of
forecasting best simulates the monthly forecasting
that would be made if this model were ultimately
implemented for predictions. Figure 3 shows a plot
of the forecasted data, along with 95% confidence
intervals, as well as the ground truth data. The
model achieved Residual Standard Error of 5.31
and an R^2 value of 0.810.
5 Algorithms
We constructed 3 different models for our data: an
ARIMA baseline model, a VAR model for monthly
data, and a MIDAS model for weekly data. We will
present the methodology as well as the results
below. We plan to use R^2 and RSE to evaluate our
model. All models are trained follow strict
test/train split temporal separation to prevent future
data leaking to the model. Training are performed
using data from 2004-2020 and all models are
evaluated from 2020 to 2024.
5.1 ARIMA Model
The first model that we used as our baseline model
for univariate time series data is the Autoregressive
Integrated Moving Average (ARIMA). ARIMA is
particularly effective in capturing the patterns and
inherent structures in historical data to predict
future values. The ARIMA model is characterized
by three parameters: (p, d, q), where p is the
number of autoregressive terms, d is the number of
differences needed to make the series stationary,
and q is the number of lagged forecast errors in the
prediction equation.
For the analysis of CSI, we selected an ARIMA
(2,0,2) based on maximizing Akaike’s Information
Criterion (AIC), while also keeping the model
relatively small to ensure numerical stability when
estimating its parameters.
The ARIMA (2,0,2) model was selected as the
baseline for our study for several reasons. First, as
a relatively simple model, it facilitates
Figure 3: Forecast of ARIMA (2,0,2) with original data
and 95% CI
5.2 Vector Autoregression (VAR) Model
We then moved on to Vector Autoregression (VAR)
to capture the dependencies between CSI and our
other predictive data. Vector Autoregression
(VAR) is a multivariate model that is used to
capture the linear interdependencies between
multiple time series. The VAR model is a
generalization of the univariate Autoregression
4
model that allows for more than one evolving
variable.
Our VAR model is structured as follows, with
regression results shown in Figure 4:
𝐶𝑆𝐼 = 𝐶𝑆𝐼. 𝑙1 + 𝑒𝑚𝑝𝑙𝑜𝑦𝑚𝑒𝑛𝑡. 𝑙1
+ 𝑚𝑜𝑟𝑡𝑔𝑎𝑔𝑒𝑅𝑎𝑡𝑒. 𝑙1
+ 𝑡𝑜𝑡𝑎𝑙𝑉𝑒ℎ𝑖𝑐𝑙𝑒𝑆𝑎𝑙𝑒𝑠. 𝑙1
+ 𝑐𝑜𝑛𝑠𝑡 + 𝑡𝑟𝑒𝑛𝑑
where l1 indicates a one-month lag
occur at different frequencies. This type of
modeling is particularly useful in our case where
we had weekly Google search trend and
macroeconomic data as our predictive variables
but monthly target variables in CSI. MIDAS
allows high-frequency data to inform predictions
of low-frequency outcomes without the need to
aggregate the high-frequency data into lower
frequencies, thus preserving much of the
information in the data.
Below is the structure of our model:
𝐶𝑆𝐼 = 𝑖𝑛𝑡𝑒𝑟𝑐𝑒𝑝𝑡 + 𝐶𝑆𝐼. 𝑙4 + 𝑒𝑚𝑝𝑙𝑜𝑦𝑚𝑒𝑛𝑡. 𝑙1
+ 𝑒𝑚𝑝𝑙𝑜𝑦𝑚𝑒𝑛𝑡. 𝑙2
+ 𝑟𝑒𝑛𝑡𝑎𝑙𝐻𝑜𝑢𝑠𝑖𝑛𝑔. 𝑙1
+ 𝑟𝑒𝑛𝑡𝑎𝑙𝐻𝑜𝑢𝑠𝑖𝑛𝑔. 𝑙2
+ 𝑚𝑜𝑟𝑡𝑔𝑎𝑔𝑒𝑅𝑎𝑡𝑒. 𝑙1
+ 𝑚𝑜𝑟𝑡𝑔𝑎𝑔𝑒𝑅𝑎𝑡𝑒. 𝑙2
+ 𝑡𝑜𝑡𝑎𝑙𝑉𝑒ℎ𝑖𝑐𝑙𝑒𝑆𝑎𝑙𝑒𝑠. 𝑙1
Figure 4: Summary of VAR
Unsurprisingly, the lag of CSI had the lowest p-
value of all our variables at 2e^-16. The Google
search trend of the term “mortgage rate” and data
on US total vehicle sales were also highly
predictive of CSI. We didn’t find that any of our
variables had significance beyond 1 lag.
The model was able to forecast our data very
effectively, using the same forecasting
methodology as the ARIMA model. The model
was able to achieve a Residual Standard Error of
2.08 and an R^2 of 0.972. Both metrics are vast
improvements upon our baseline ARIMA model.
Figure 5 displays the forecasting results.
Unfortunately, the MIDAS model performed
much worse than the VAR model and only slightly
better than the baseline model, with a Residual
Standard Error of 4.93 and an R^2 of 0.836. Figure
6 shows the forecast results on the test data, along
with the ground truth data, forecasted with the
same methodology as the previous two models.
Figure 5: Forecast of VAR With Original Data
5.3 Mixed Data Sampling (MIDAS) Model
Although the VAR model was able to explain the
data very well, we hoped to forecast weekly CSI,
rather than monthly, to give a timelier forecast of
this important metric. The Mixed Data Sampling
Figure 6: Forecast of MIDAS With Original Data
6 Results and Discussion
Our first key takeaway from our modeling process
was the effectiveness and simplicity of the VAR
model in forecasting monthly Consumer Sentiment
Index. Using only 6 parameters, we were able to
achieve an R^2 of 0.972 and an RSE of 2.08. A key
reason for that is the feature selection of our
variables that can effectively capture the changes
in CSI. Additionally, VAR is very capable at
capturing variable-temporal relationships and
maximizing parameter likelihood.
(MIDAS) model is an econometric approach
designed to handle datasets where observations
5
Our second key takeaway from our modeling
process was how poorly MIDAS performed
relative to our simpler baseline ARIMA model and
the better VAR model, with R^2 and RSE only
slightly better than the ARIMA model. We have
two hypotheses as to why this was the case. The
first is that the parameter estimation methods for
VAR may be more effective at maximizing the
likelihood than that of MIDAS. VAR commonly
relies on Ordinary Least Squares (OLS), whereas
MIDAS often relies on Non-linear Least Squares
or gradient based optimizations. Due to this, the
parameter estimation methods for these respective
models may lead to VAR providing more
effectively maximized parameters than MIDAS.
The second hypothesis for why MIDAS wasn’t as
successful is that there is less information
contained in weekly data, especially weekly data
that is only 1-2 weeks before the target date, than
in monthly data from the previous month. This
might lead to more information being captured
more succinctly in the VAR modeling process than
in MIDAS.
Model ARIMA VAR MIDAS
RSE 5.31 2.08 4.39
R^2 0.81 0.973 0.836
Predictors 4 6 9
p-value <2.2e-16 <2.2e-16 <2.2e-16
Table 3: Model Evaluation Results
7 Ethical Implications
7.1 Sampling Bias
Given that Google is used by most of the
population, and our word selection seems to
encompass the general US population, it would
appear likely that our system will perform well in
a heterogeneous population. However, the people
who don’t have internet access (approximately 7%
of the adult population; via Pew Research),
whether that be because they are from an older
generation, have poor financial situations, or they
live in rural areas, might be under-represented in
our model. If that is the case, this could lead to bias
in our model. We will further explore whether the
sample of Google users is representative of the US
population.
Furthermore, while Google commands a
substantial 87.48% share of the search engine
market in the U.S. (gs.statcounter.com), it is
important to recognize that a significant number of
users still opt for alternative search engines like
Bing. The model may not fully capture the
behaviors of those who prefer other search engines,
which introduces a potential lack of representation.
7.2 Caveat Emptor
The consequences of inaccurate predictions in a
CSI prediction model can be significant. If the
system makes mistakes, individuals may form
incorrect perceptions about the economy, which
could influence major financial decisions,
investment choices, and overall consumer
behavior. Our model only uses previous CSI
V alues, Total US Car Sales, and the Google Search
Trends of “mortgage rate” and “employment” so it
isn’t all encompassing of the economy and price of
household items, so we strongly advise against
using our model to make any major financial
decisions, as its purpose is to be predictive and
provide insight into what factors influence
consumer sentiment.
8 Conclusion
Using Google Trends and macroeconomic data, we
were able to effectively model future Consumer
Sentiment Index values very effectively, capturing
the underlying factors that motivate change in
consumer sentiment on a national level. Without a
doubt, our work was a success in its ability to
forecast future values of CSI with exceedingly high
accuracy. Vector Autoregression proved to be an
effective statistical method to model the temporal
structure of CSI. It was highly revealing that
employment, mortgage rate, and total vehicle sales
were highly predictive of CSI.
Additional work in the future can be focused on
two areas. The first being additional feature
selection to incorporate other variables (whether it
be Google Trends, macroeconomic data, or other)
to predict CSI that would add additional insight
into the factors that affect CSI and that would
further increase the model’s predictive ability. The
second area of future focus would be working with
MIDAS and other mixed-frequency modeling
methods that could forecast CSI on a weekly basis.
It would be incredibly useful to a variety of
bankers, politicians, manufacturers, and other
6
working positions to have forecasts of CSI at a
higher frequency so they can make real-time
decisions in their line of work with up-to-date
forecasts.
References
Armesto, M. T., Engemann, K. M., & Owyang, M. T.
(2010). Forecasting with Mixed Frequencies.
Review, 92(6).
https://doi.org/10.20955/r.92.521-36
Choi, H. (n.d.). Consumer Sentiment - with Google
Trends. Federal Reserve Bank of San
Francisco. https://www.frbsf.org/wp-
content/uploads/sites/4/Varian-part_2.pdf
Choi, H., & Varian, H. (2011). Predicting the Present
with Google Trends. Berkeley School of
Information.
https://people.ischool.berkeley.edu/~hal/Paper
s/2011/ptp.pdf
Federal Reserve Bank of St. Louis. (n.d.). Welcome to
FRED, Federal Reserve Economic Data. Your
Trusted Source for Economic Data Since
1991. FRED. https://fred.stlouisfed.org/
Han, H., Li, Z., & Li, Z. (2023). Using Machine
Learning Methods to Predict Consumer
Confidence from Search Engine Data.
Sustainability, 15(4), 3100.
https://doi.org/10.3390/su15043100
Schmitz, M. (2019, December 6). Using Google
Trends Data to Leverage Your Predictive
Model. Medium.
https://towardsdatascience.com/using-google-
trends-data-to-leverage-your-predictive-
model-a56635355e3d
Survey of Consumers. (n.d.). Index of Consumer
Sentiment.
https://data.sca.isr.umich.edu/fetchdoc.php?do
cid=24770
7
