# NLP_Seasonal-Energy-Consumption-Forecasting-Using-SARIMAX
The SARIMAX model's performance on forecasting monthly electricity consumption showed a Mean Absolute Percentage Error (MAPE) of 45.86%, a Root Mean Squared Error (RMSE) of 1,941,622.14, and a Mean Absolute Error (MAE) of 866,383.08. The visual inspection of forecasts against actual values indicated that while the model captures the overall trend, its predictions are not consistently close to the actual values, particularly during peak consumption periods.

Strong seasonal patterns with a 12-month period were clearly identified through seasonal decomposition and influenced the selection of seasonal orders for the SARIMAX model. The model incorporated seasonal differencing (D=1) and seasonal autoregressive/moving average components (P=1, Q=1) with a seasonality of 12.

The AEP_hourly.csv dataset did not contain any explicit temperature data. Therefore, the SARIMAX model was developed and trained without an exogenous temperature variable. This means there was no impact from temperature on the model's predictions because it was not included in the model.

Overall, the monthly electricity consumption forecasting using the SARIMAX model demonstrates a foundational approach to time series analysis. While the model captures the seasonality and overall trend, the high MAPE suggests that its accuracy for precise monthly predictions is limited, potentially due to the absence of key external factors like temperature or other uncaptured complexities in the data.

Data Analysis Key Findings
The raw dataset AEP_hourly.csv contained hourly electricity consumption (AEP_MW) and Datetime information, but no temperature data or other exogenous variables.
Hourly data was successfully resampled to monthly frequency by summing AEP_MW values, resulting in df_monthly with 167 observations ranging from 2004-10-31 to 2018-08-31. No missing values were found after resampling.
Seasonal decomposition revealed a clear additive seasonality with a 12-month period in the monthly electricity consumption.
The initial Augmented Dickey-Fuller (ADF) test showed the original monthly AEP_MW series was non-stationary (p-value = 0.9667). After first-order differencing, the series became stationary (p-value = 0.0057).
The data was split into training (133 observations, 2004-10-31 to 2015-10-31) and testing (34 observations, 2015-11-30 to 2018-08-31) sets.
A SARIMAX model was trained with non-seasonal orders (1, 1, 1) and seasonal orders (1, 1, 1, 12), with seasonal differencing (D=1) effectively addressing initial convergence warnings. The model summary reported a Log Likelihood of -1551.391, AIC of 3112.782, and BIC of 3126.099. A "Covariance matrix is singular or near-singular" warning persisted.
Residual diagnostics using the Ljung-Box test indicated that while residuals largely resembled white noise at lags 24 and 36 (p-values 0.1468 and 0.4415 respectively), there was a statistically significant autocorrelation at lag 12 (p-value = 0.0498), suggesting the model might not have fully captured all seasonal dependencies.
Model evaluation on the test set yielded a Mean Absolute Error (MAE) of 866,383.08, a Root Mean Squared Error (RMSE) of 1,941,622.14, and a Mean Absolute Percentage Error (MAPE) of 45.86%.
Insights or Next Steps
Refine Seasonal Model Parameters: The Ljung-Box test indicated remaining autocorrelation at the 12-month lag. Further tuning of the seasonal orders (P, D, Q) in the SARIMAX model, potentially by exploring a wider range of values or using automated parameter selection methods, could improve the model's ability to capture the remaining seasonal patterns.
Incorporate Exogenous Variables: Given the significant impact temperature typically has on electricity consumption, integrating external temperature data (if available from other sources) as an exogenous variable in the SARIMAX model could significantly improve forecasting accuracy and provide a more robust model.
