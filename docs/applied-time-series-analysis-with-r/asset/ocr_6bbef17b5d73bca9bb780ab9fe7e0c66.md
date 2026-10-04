# Nonstationary Time Series Models 223

n is the realization length

phi is a vector of AR parameters (of the stationary part of the model)
(default = 0)

theta is a vector of MA parameters (using signs as in this text)
(default = 0)

d specifies the number of factors of (1 - B) in the model. For station-ary models, you could use either gen.arma.wge or use gen.arima.wge with d=0.

vara is the white variance (default = 1)
plot = TRUE (default) produces a plot of the realization generated
sn determines the seed used in the simulation (see Note (4) below).

# NOTES:

+   1. It will be useful to use the utility function mult.res if you know the factors of the model instead of the coefficients.

+   2. By the white noise is zero mean, normal noise with vari-ance.

+   3. This function uses a call to the R function arima.sim which uses the same signs as this text for the parameters but opposite signs for MA parameters. The appropriate adjustments are made within gen.arima.sim so that input vectors phi and theta for gen.arima.sim should contain parameters using the signs as in this text. However, if you use arima.sim directly (which has options not employed in gen.arima.sim), then you must remember that the signs needed for the MA parameters have opposite signs from those in gen.arima.wge.

+   4. sn = 0 produces results based on a randomly selected seed. If you want to repeat the same realization on sub-quents of gen.arima.wge then set sn to the positive integer value each run.

> Example: the command
x = gen.arima.wge(n=200,phi=c(1.6,-9),theta=.9,d=2,
vara=1) generates and plots a realization from the model
(1-1.6B+0.9B^2),X=(1-0.9B), and stores it in the vector
x$data. The white noise was normally distributed with mean
zero and variance 1 and a random seed is used.

+   b. gen.arima.wge(n,phi,theta,d,s,lambda,vara,sn) is a function that generates a realization of length n from a given AR, MA,
ARIMA, ARMA, ARUMA, or seasonal model.

n is the realization length

phi (default = 0) is a vector of AR parameters