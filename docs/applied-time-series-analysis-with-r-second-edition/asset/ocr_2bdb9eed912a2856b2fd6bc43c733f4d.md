transformation of the time axis produces stationary data that can be modeled using stationarity-based techniques. G-stationary models are the topic of Chapter 13, and further discussion will be deferred until then.

# Appendix 5A: R Commands

# 5A.1 Basic Computation and Plot Routines

+   a. `gen.arima.wge(n,phi,theta,d,lambda,vara,sn)` is a function that generates a realization of length n from a given AR, MA, ARMA, or ARIMA model.
+   
+      `n` is the realization length
+   
+      `phi` is a vector of AR parameters (of the stationary part of the model) (default = 0)
+   
+      `theta` is a vector of MA parameters (using signs as in this text) (default = 0)
+   
+      `d` specifies the number of factors of (1 − B) in the model. For stationary models, you could use either `gen.arma.wge` or use `gen.arima.wge` with d = 0.
+   
+      `vara` is the white noise variance (default = 1)
+   
+      `plot = TRUE` (default) produces a plot of the realization generated
+   
+      `sn` determines the seed used in the simulation (see Note (4) below).

# NOTES:

+   1. It will be useful to call the utility function `mult.res` if you know the factors of the model instead of the coefficients.
+   
+   2. By default the white noise is zero mean, normal noise with variance `vara`.
+   
+   3. This function uses a call to the base R function `arima.sim` which uses the same signs as this text for the AR parameters but opposite signs for MA parameters. The appropriate adjustments are made within `gen.arima.sim` so that input vectors phi and theta for `gen.arima.wge`