+   - **Plot Actual by Predicted** displays the observed values by the predicted values of Y. This is the leverage plot for the whole model.
+   - **Plot Effect Leverage** produces a leverage plot for each effect in the model showing the point-by-point composition of the test for that effect.
+   - **Plot Residual By Predicted** displays the residual values by the predicted values of Y. You typically want to see the residual values scattered randomly about zero.
+   - **Plot Residual By Row** displays the residual value by the row number of its observation.
+   - **Durbin-Watson Test** displays the Durbin-Watson statistic to test whether or not the errors have first-order autocorrelation. The autocorrelation of the residuals is also shown. The Durbin-Watson table has a popup command that computes and displays the exact probability associated with the statistic. This Durbin-Watson table is only appropriate for time series data when you suspect that the errors are correlated across time.

# Save Commands

The Save submenu offers the following choices. Each selection generates one or more new columns in the current data table titled as shown, where colname is the name of the response variable:

**Prediction Formula** creates a new column, called Pred Formula colname, containing the predicted values computed by the specified model. It differs from the Save Predicted Values column in that the prediction formula is saved with the new column. This is useful for predicting values in new rows or for obtaining a picture of the fitted model.

Use the Column Info command and click the Edit Formula button to see the prediction formula. The prediction formula can require considerable space if the model is large. If you do not need the formula with the column of predicted values, use the Save Predicted Values option.

**Predicted Values** creates a new column called Predicted colname that contain the predicted values computed by the specified model.

**Residuals** creates a new column called Residual colname containing the residuals, which are the observed response values minus predicted values.

**Mean Confidence Interval** creates two new columns called Lower 95% Mean colname and Upper 95% Mean colname. The new columns contain the lower and upper 95% confidence limits for the line of fit.

Note: If you hold down the Shift key and select Save Mean Confidence Interval, you are prompted to enter an α-level for the computations.

**Individual Confidence Interval** creates two new columns called Lower95% Indiv colname and Upper95% Indiv colname. The new columns contain lower and upper 95% confidence limits for individual response values.

Note: If you hold down the Shift key and select Save Individual Confidence Interval, you are prompted to enter an α-level for the computations.

**Studentized Residuals** creates a new column called Studentized Resid colname. The new column values are the residuals divided by their standard error.

**Std Error of Predicted** creates a new column, called StdErr Pred colname, containing the standard errors of the predicted values.