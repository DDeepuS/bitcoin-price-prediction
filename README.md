# Bitcoin Price Directional Prediction
**Authors:** Deepesh Singhal, Yuxin Lin

This project was done as a part of the Erdos Institute Deep Learning Bootcamp

## 🚀 Project Overview
Bitcoin’s price exhibits both a long-term trend/halving-cycle seasonality and shorter-term fluctuations driven by macroeconomic forces. This project studies the bitcoin price series through time series analysis and modeling the effects of exogenous factors. We seek to make predictions about whether the bitcoin price will increase or decrease over the following time horizons: 2 weeks, 1 month and 2 months.
We first create an ordinary least squares (OLS) model that captures long-term trend and the seasonality induced by the bitcoin halving cycle. However, residuals often contain valuable information driven by macroeconomic factors and higher-order temporal dependencies. We therefore model these residues by a LSTM network using macro-economic features as well as price movement of other assets.


## 📂 Repository Structure
```text
bitcoin-price-prediction/
├── Data/                               # Raw input files (CSV downloads of on-chain and macro series)
├── Processed_data/                     # Cleaned & merged datasets (e.g. Main_df.csv)
├── Notebooks/                          # Jupyter notebooks for EDA, model development, and final results
│   ├── Download data.ipynb             # Downloads raw datasets
│   ├── data_cleaning.ipynb             # Cleans and merges these datasets to create Main_df.csv
│   ├── Trend and seasonality.ipynb     # Creates an OLS model to capture the trend and seasonality in bitcoin price movements 
│   ├── Autocorrelation.ipynb           # Studies the autocorrelation in the residues of trend+seasonality model      
│   └── Final_network.ipynb             # Has the final model which consists of trend+seasonality OLS and LSTM trained on its residues.
└── README.md             Project overview
```

## 📈 Results
| Horizon  | Best Baseline | Trend + Seasonality | + LSTM  | p-value          |
|:--------:|:-------------:|:-------------------:|:-------:|:----------------:|
| 14 days  | 53.58 %       | 51.81 %             | 55.55 % | 0.014            |
| 30 days  | 53.96 %       | 53.47 %             | 58.63 % | &lt; 0.0001      |
| 60 days  | 55.31 %       | 60.90 %             | 62.54 % | &lt; 0.0001      |


Over 14 day and 30 day horizons, the Trend+Seasonality models underperform the baseline, indicating that short term fluctuations are more dominant than the trend and seasonality for these shorter horizons. However, adding LSTM residual yields a statistically significant improvement.

For the 60 day time horizon, the trend+Seasonality model performs significantly better than the baseline. Adding LSTM residual yields a further improvement.