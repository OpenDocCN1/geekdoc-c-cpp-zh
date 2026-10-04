# Model Identification 335

identifies the possible need for differencing (one time) that is also suggested by the classical Box-Jenkins procedure. However, for data from model in Equation 8.13, the overfitting problem also identifies analogous nonstationary-like behavior associated with complex roots on the unit circle.

# 8.3.3 Decision Between a Stationary or a Nonstationary Model

For the two models considered in the previous example, it is important to note that AIC based on ML (and Burg) estimates selects the correct order (p=3) in both cases. However, the resulting model is stationary. In order to select a nonstationary model, you should make a conscious decision (a) such a model is identified and (b) that such a model makes sense. For example, if stock prices have a wandering behavior and other indicators suggest a possible root of +1, your decision to use a factor 1−B should be based on your assessment concerning whether there is or not some sort of attraction to a mean level, where an attraction would suggest the use of a stationary (non-stationary) model. However, it is often the case that the $X_t = X_{t-1} + a_t$ is physically more appealing than, for example, $X_t = 0.98X_{t-1} + a_t$.

# 8.3.4 Deriving a Final ARUMA Model

After we have determined that one or more nonstationary factors should be included in the model, we are ready to perform the final two steps mentioned in the ARUMA modeling outline. Specifically, we transform the data to stationary (Step b) and model the stationary data with ARMA(p,q) model (Step c) using model identification using techniques of Section 8.2 and model estimation discussed in Chapter 7. These two steps will be illustrated in Example 8.5 using the two data sets considered in Example 8.4.

# EXAMPLE 8.5: FINAL MODELS FOR THE DATA IN FIGURES 8.3A AND 8.4A

Suppose that for each of the realizations in Example 8.4, the decision is to include a nonstationary factor in the model, that is, a factor of 1−B for the realization in Figure 8.3a and a factor of $1−1.62B + B^2$ for the data in Figure 8.4a. We illustrate steps (b) and (c) of the ARUMA model-outline.

+   1. Final model for Figure 8.3a: Since we have concluded that a factor of 1−B is included in the model, the next step is to differ the data (i.e., transform using the operator 1−B) to obtain stationary data. Figure 8.5a shows these differenced data. That is, Figure 8.5a is a plot of length $n−1=199$ of the