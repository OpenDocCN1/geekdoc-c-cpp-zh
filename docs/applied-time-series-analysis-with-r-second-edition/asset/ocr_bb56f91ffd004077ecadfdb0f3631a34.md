ii. Find Var[X_t]

iii. For an α₀, β₀, and β₁ that you select, plot a realization you have generated from each model, and describe the appearance of typical realizations

b. Consider the transformation Z_t = X_t − X_{t−1}

i. Discuss the properties of Z_t (stationarity, what model is satisfied by Z_t, etc.) if X_t actually follows Model A. Also discuss the properties of Z_t if X_t satisfies Model B.

ii. Discuss how one could use the properties obtained above to distinguish between the two types of models.

c. Consider the data in files prob9.6c1, prob9.6c2, prob9.6c3, and prob9.6c4. These data were generated using either Model A or Model B. Based on what you learned in (a) and (b), decide which of these two models was used to generate the data.

# 9.7

The log-lynx data (11ynx in tswge) was modeled by Tong (1977) using an AR(11) model. In Example 8.3 an ARMA(2,3) model selected by BIC was considered. Fit the data in 11ynx using AR(11) and ARMA(2,3) models. Use ML estimates for both models (in which case your AR(11) model will differ somewhat from Tong's. Using 1jung.wge and other assessment criteria you choose to use to decide which (of these two ARMA models) is more appropriate.

# 9.8

Consider the British wage data in tswge file wages. In Example 8.6 it was noted that the differenced wage data looked fairly “white” and the sample autocorrelations were “small.” However, since the first two sample autocorrelations were on or outside the 95% limit lines, the decision was made to continue modeling, and an ARMA(2,1) model was fit to the differenced data.

a. Use 1jung.wge to assess the differenced data for white noise. What do you conclude?

b. Fit the ARMA(2,1) model used in Example 8.6 to the differenced data and use 1jung.wge to assess the whiteness of the residuals. Also examine plots of the residuals. Does the ARIMA(2,1,1) model in Example 8.6 seem to be an appropriate model for the wages data?