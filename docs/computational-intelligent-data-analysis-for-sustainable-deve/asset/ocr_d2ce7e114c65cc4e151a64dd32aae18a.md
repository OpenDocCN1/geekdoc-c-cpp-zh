![](bbox=[0.17, 0.08, 0.87, 0.47])

FIGURE 8.7  Lucheroni model for the 3 sample days.

The Lucheroni model (Figure 8.7) is good at picking up the peak, and the AR(2) model (Figure 8.6) is good at forecasting in the main regions of the series, because when the AR(2) model reaches the peak, it is converging to the mean faster than the Lucheroni model. Is there evidence for this other than eyeballing the graphs? Combining the AR(2) model with the Lucheroni model could solve those problems. We can also add a second derivative component (a proxy for curvature) that adds even more to the predictability (Figure 8.8).

# 8.3.4  Estimating Volatility

Traditional methods for forecasting volatility are indirect by necessity because the volatility is unobservable in a time series. These indirect methods include generalized autoregressive conditional heteroscedastic (GARCH) [9] and Hidden Markov Models (HMMs) [40]. We have developed a method for estimating the volatility using high-frequency data [1], and then use the resonating model [26] for forecasting the volatility at the 5-minute and 30-minute timescales required by the electricity market. These forecasting methods can also be used to delineate the level and variability of output. We are thus able to make these estimations for any proposed individual wind or solar installation.