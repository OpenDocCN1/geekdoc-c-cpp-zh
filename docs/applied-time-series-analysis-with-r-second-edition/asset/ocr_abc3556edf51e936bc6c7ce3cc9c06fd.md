should contain parameters using the signs as in this text. However, if you use arima.sim directly (which has options not employed in gen.arima.sim), then you must remember that the signs needed for the MA parameters have opposite signs from those in gen.arima.wge.

4. sn = 0 (default) produces results based on a randomly selected seed. If you want to reproduce the same realization on subsequent runs of gen.arima.wge then set sn to the same positive integer value on each run.

Example: The command

```
x = gen.arima.wge(n = 200, phi = c(1.6, -.9), theta = .9, d = 2, vara = 1)
```

generates and plots a realization from the model (1 − 1.6B + 0.9B²)(1 − B)²X_t = (1 − 0.9B)a_t. and stores it in the vector x$data. The white noise was normally distributed with mean zero and variance 1 and a random seed is used.

b. gen.aruma.wge(n, phi, theta, d, s, lambda, vara, sn) is a function that generates a realization of length n from a given AR, MA, ARMA, ARIMA, ARUMA, or seasonal model.

+   - n is the realization length
+   - phi (default = 0) is a vector of AR parameters
+   - theta (default = 0) is a vector of MA parameters (using signs as in this text).
+   - d (default = 0) specifies the number of factors of (1 − B) in the model.
+   - s (default = 0) specifies the order of the seasonal factor (1 − B^s).
+   - lambda (default = 0) is the nonstationary operator, λ(B), in Equation 5.8 of this text (technically designed to contain nonstationary factory factors other than differences and seasonal factors). However, see Note 1 below for discussion regarding difference and seasonal factors.
+   - vara is the white noise variance (default = 1).
+   - plot = TRUE (default) produces a plot of the realization generated.
+   - sn determines the seed used in the simulation (default = 0) (see Note (5) below).

# NOTES:

1. gen.aruma.wge is the most general