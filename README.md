# 📈 Forecasting Consumer Sentiment Index Using Google Trends and Macroeconomic Data By Kenji Wagner, Jacob Richman, and Andrew Ye

This project applies time series modeling techniques to forecast the University of Michigan's Consumer Sentiment Index (CSI) using a combination of Google Trends search volume data and macroeconomic indicators. By integrating unconventional data sources (Google Trends) with traditional economic variables (FRED, Yahoo Finance), the project demonstrates how consumer behavior and public interest can enhance economic forecasting accuracy. 

# Explanation of other files:
gf_analysis.ipynb was for searching for trends in the data. trends_analysis.Rmd was used for fitting the time series model. trim.ipynb. forecastingcsi.pdf illustrated our findings in an interpretable manner.




# 🔧 Key Features
Data sources: Google Trends, FRED, and Yahoo Finance
Time series models: ARIMA, VAR, and MIDAS
Feature engineering and lag selection for economic indicators
Achieved high forecast accuracy (R² = 0.972 with VAR model)
📊 Tools & Technologies
Python (pandas, statsmodels, pmdarima, sklearn)
Jupyter Notebooks
Google Trends API
FRED & Yahoo Finance data ingestion
Time series cross-validation & model diagnostics
