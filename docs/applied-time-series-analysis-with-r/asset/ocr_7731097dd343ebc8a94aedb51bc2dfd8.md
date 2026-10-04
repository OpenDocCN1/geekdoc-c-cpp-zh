# Long-Memory Processes

3. This function finds $p$ and $q$ as the length of phi and theta respectively. If either $phi = 0$ or $theta = 0$ (default) the values for $p$ and $q$ are set to zero, respectively.

Example: The command

```
traut =true.forma.aut.wge(d=4,phi=c(1,6,-8),lag.max=25)
```

calculates the true autocorrelations, up to lag 25, shown in Figure 11.4b associated with the FARMA model $(1-0.9B)(1-2.9B+B^2)^{45}X_t$. Because the default PLOT=TRUE is selected, the true autocorrelations will be plotted. The autocorrelations $ho_k$, $k=0,1,...,25$ are stored in the vector traut$acf Similarly the covariances $\gamma_k$, $k=0,1,...,25$ are stored in the vector traut$acv. The process variance is in traut$acv[1].

+   b. traut.gamma.aut.wge(u,lambda,phi,theta,lag.max,vara,vara,plot) calculates the true autocorrelations and autocovariances associated with a given GARMA model of the form in Equation 11.6.

u and lambda are the parameters of the Gegenbauer factor in Equation 11.16

phi is a vector of AR parameters (using signs in this text) theta is a vector of MA parameters (using signs in this text) lag.max is the maximum lag at which the autocorrelations and autocovariances will be calculated (default=25) vara is the white noise variance (default=1)

vara is the white noise variance (default=1)

plot is a logical variable: TRUE (default)=plot autocorrelations, FALSE=no plot

The function outputs

```
acf (the true autocorrelations from lags 0 to lag.max)
acv (the true autocovariances from lags 0 to lag.max)
```

NOTES:

+   1. You may want to use the utility function mult.wge if you know the factors of the AR or MA model instead of the coefficients.

+   2. max(p,q+1) $\le$25.

+   3. This function finds $p$ and $q$ as the length of phi and theta respectively. If either $phi=0$ or $theta=0$ (default) the values for $p$ and $q$ are set to zero, respectively.

Example: The command