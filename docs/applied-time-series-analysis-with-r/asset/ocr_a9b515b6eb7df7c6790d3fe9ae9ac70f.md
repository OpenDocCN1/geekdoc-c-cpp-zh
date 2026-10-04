# ARMA Time Series Models

NOTES:

+   1. This function finds p and q as the length of phi and theta, respectively. If either phi = 0 or theta = 0 (default) the values for p and q are set to zero, respectively.

+   2. gen.arma.wge calls the base R function arma.sim which uses the same signs as this text for the AR parameters but opposite signs for MA parameters. The appropriate adjustments are made within gen.arma.wge so that input parameters phi and theta for gen.arma.wge should contain parameters using the signs in this text. However, if you use arma.sim directly (with options not employed in gen.arma.wge), then you must remember that the MA parameters have opposite signs as those in gen.arma.wge.

+   3. arma.sim allows for nonstationary models (covered in Chapter 5) with a factor (1 - B) where d can take on a positive integer value. However, gen.arma.wge is designed specifically for stationary AR models.

+   4. It will be useful to call the utility mult.wge if you know the factors of the model instead of the coefficients.

+   5. By the default white noise is zero, normal noise with variance = 1.

+   6. sn = 0 (default) produces results based on a randomly selected seed. If you want to reproduce the same realization on subsequent runs of gen.arma.wge then set sn to the same integer value over each run.

Example: The command

```
x = gen.arma.wge(n = 100, c = c(1.6,-.9), theta = .9,
vara = 1) generates and plots the projection from the model
Xi-1 + 0.9Xi-2 = -0.9Xi-1, and stores it in the vector xdata.
The white noise is normally distributed with mean zero and variance 1 and the seed is randomly selected.
```

+   b. true.arma.aut(wge(phi,lag,max,vara)) calculates the true autocorrelations and autocovariances associated with a given MA, AR, or AR model.
phi is a vector of AR parameters (using signs as in this text)
theta is a vector of MA parameters (using signs as in this text)
lag.max is the maximum lag at which the autocorrelations and autocovariances will be calculated (default = 25)
 is the white noise variance (default = 1)
plot is a logical variable: TRUE = plot autocorrelations, FALSE = no
plot (default is plot = TRUE)