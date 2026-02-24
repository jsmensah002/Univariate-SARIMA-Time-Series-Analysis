Brief Overview:
- This project explores the application of Seasonal Autoregressive Integrated Moving Average (SARIMA) modeling to forecast electricity consumption, with the goal of identifying the optimal model configuration for accurate and reliable predictions.

Method:
- The stationarity of the time series data was first assessed using the Augmented Dickey-Fuller (ADF) test.
- Optimal SARIMA parameters were then identified using Auto-ARIMA to streamline model selection. 
- The dataset was split into a 80/20 train-test ratio, with the model trained on 80% of the data and evaluated on the remaining 20%. 
- Model performance was assessed using Root Mean Squared Error (RMSE) for both the training and test sets.
- Forecast results were then visualized alongside confidence intervals to illustrate prediction uncertainty.

SARIMA Results:
- p value from the ADF test = 0.1862 (> 0.05, non-stationary)
- The Auto-ARIMA selection process identified an initial SARIMA(1, 1, 3)(0, 1, 1)[12] model.
- (Auto-Regression Lag1) AR.L1: p = 0.000 (< 0.05, significant)
- (Moving Average Lag1) MA.L1: p = 0.000 (< 0.05, significant)
- (Moving Average Lag2) MA.L2: p = 0.641 (> 0.05, not significant)
- (Moving Average Lag3) MA.L3: p = 0.039 (< 0.05, significant)
- (Moving Average Seasonal Lag12) MA.S.L12: p = 0.000 (< 0.05, significant)
- (Ljung-Box Test) Prob(Q): p = 0.87 (> 0.05, no autocorrelation)
- (Jarque-Bera Test) Prob(JB): p = 0.000 (< 0.05, residuals not normally distributed)
- (Heteroskedasticity Test) Prob(H): p = 0.000 (< 0.05, heteroskedastic)

Discussion:
- Since MA.L2 was not significant (p = 0.641 > 0.05), the q parameter was reduced from 3 to 2, resulting in a updated SARIMA(1, 1, 2)(0, 1, 1)[12] model. The new model results showed that all remaining parameters were now statistically significant:
- (Auto-Regression Lag1) AR.L1: p = 0.018 (< 0.05, significant)
- (Moving Average Lag1) MA.L1: p = 0.000 (< 0.05, significant)
- (Moving Average Lag2) MA.L2: p = 0.021 (< 0.05, significant)
- (Moving Average Seasonal Lag12) MA.S.L12: p = 0.000 (< 0.05, significant)
- (Ljung-Box Test) Prob(Q): p = 0.85 (> 0.05, no autocorrelation)
- (Jarque-Bera Test) Prob(JB) = 0.000 (< 0.05, residuals not normally distributed)
- (Heteroskedasticity Test) Prob(H): p = 0.000 (< 0.05, heteroskedastic)
- The Prob(JB) and Prob(H) still did not meet the 0.05 threshold, indicating that the residuals remained non-normally distributed and heteroskedastic.
- However, the train and test RMSE were calculated to assess whether the model performance was still acceptable despite these issues: Train RMSE = 5.02, and
Test RMSE = 4.20
- The lower test RMSE compared to the train RMSE suggests that the model generalizes well to unseen data, indicating a good fit overall despite the unresolved JB and H diagnostics.

Graph plotting:
- The plot displays the SARIMA(1, 1, 2)(0, 1, 1)[12] model's electricity consumption forecast from 1985 to 2023. The training data (red) captures the historical upward trend with clear seasonal patterns. The forecast (green) was first plotted alongside the test data (yellow) to evaluate model performance, before continuing to forecast beyond the test period into the future. The shaded confidence interval widens over time, reflecting increasing uncertainty further into the future.

Key Insights:
- While the SARIMA(1, 1, 2)(0, 1, 1)[12] model performed well in terms of RMSE, the Jarque-Bera ( prob(JB) ) and Heteroskedasticity ( prob(H) ) results indicated that the residuals were not normally distributed and the variance was not constant, suggesting the model could be further improved. Future work could explore additional transformations or alternative models to better handle these issues.
