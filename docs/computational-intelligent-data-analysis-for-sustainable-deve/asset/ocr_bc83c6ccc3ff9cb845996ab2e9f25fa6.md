![](bbox=[0.09, 0.07, 0.93, 0.51])

**FIGURE 8.5** Effect of beat frequencies—winter.

year. Note that in the examples we have tested, the amount of variance explained by the Fourier series is approximately 80% to 85%.

# 8.3.2 Box-Jenkins or ARMA Modeling

Once the seasonal component has been determined, we subtract its contribution from the data and work with the residual series r_t. The general form of an ARMA (p,q) model is

X_t - φ_1 X_{t-1} - φ_2 X_{t-2} - ... - φ_p X_{t-p} = Z_t + θ_1 Z_{t-1} - θ_2 Z_{t-2} + ... + θ_q Z_{t-q}

where {X_t} are random variables with X_t ~ (0,σ_X^2) and {Z_t} is white noise, independent and identically distributed with Z_t ~ (0,σ_Z^2). Figure 8.6 shows results from an AR(2) model.

# 8.3.3 A Resonating Model

Figure 8.6 shows that this AR(2) model works particularly well when solar radiation residuals are decreasing. However, the AR(2) model has underestimated all the high peaks of the data. So, it is important to find another model to help capture these peaks. Lucheroni [26] presented a resonating model for the power market that exploits the simultaneous