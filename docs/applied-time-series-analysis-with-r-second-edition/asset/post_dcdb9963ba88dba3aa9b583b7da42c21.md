
b1 is the slope of a linear regression component (default = 0)
coef is a 2-component vector specifying the coefficients (if only one cosine term is desired define coef[2] = 0) (default = c(0,0))
freq is a 2-component vector specifying the frequency components (0 to .5) (default = c(0,0))
psi is a 2-component vector specifying the phase shift (0 to 2π) (default = c(0,0))
phi is a vector containing the AR model for the noise process (see Chapter 3). (default = 0) For white noise just use the default values for phi.
vara is the variance of the noise (default = 1).
NOTE: a(t) is a vector of N(0,vara) white noise generated within the function
plot is a logical variable. plot = TRUE (default) produces a plot of the generated realization.
sn determines the seed used in the simulation. (default = 0) (see Note below)

NOTE: sn = 0 (default) produces results based on a randomly selected seed. If you want to reproduce the same realization on subsequent runs of gen.sigplusnoise.wge then set sn to the same positive integer value on each run.

## Example: The command

```
x = gen.sigplusnoise.wge(n = 100, coef = c(1.5,3.5),
freq = c(.05,.2), psi = c(1.1,2.8), phi = .7, vara = 2)
```

calculates

x(t) = 1.5cos(2π(0.05)t + 1.1) + 3.5cos(2π(.2)t + 2.8) + z(t), t = 1, 2, ..., 100

where z(t) is a realization from the AR(1) process z(t) = (1 - .7B)a_t where σ_a^2 = 2. The realization is based on a randomly selected seed, and the resulting signal-plus-noise realization is placed in the vector x.

## 2. Combination Plot Routines for Chapter 1

- a. plotts.sample.wge(x, lag.max, trunc, arlimits) is a tswge R function that plots a realization, sample autocorrelations, periodogram, and smoothed periodogram based on the Parzen window (both plotted in dB).

density estimate at a variety of truncation points. You can use the following

```r
x = gen.sigplusnoise.wge(n = 250, coef = c(3,1), freq =
c(.1,.52),
psi = c(0,1), phi = 0, vara = 1)
pz = plotts.parzen.wge(x, m2 = c(10,50))
```

produces a plot of the periodogram in dB, Parzen spectral estimate with truncation point $M = 2\sqrt{250} = 31.6$ (rounds down to $M = 31$), along with the Parzen spectral estimators with truncation points $M = 10$ and $M = 50$. All plots are in dB. Also output are pz$freq which is a vector containing the frequencies at which the Parzen spectral estimates are calculated (in our case 1/250, 2/250, ..., 125/250) along with the vectors pz$db and pz$dbz1, which contain the periodogram and the Parzen spectral density at truncation point $M = 31$, respectively, evaluated at the frequencies in pz$freq. Also output in this example are the vectors pz$dbz2 and pz$dbz3 which contain the Parzen spectral density estimates using truncation points $M = 10$ and $M = 50$, respectively.

## EXERCISES

### Applied Problems

Use R to work problems 1.2 through 1.7.

1.1 The following data are annual sales of a hypothetical company in millions of dollars:

| Period | Sales |
|---:|---:|
| 1 | 76 |
| 2 | 70 |
| 3 | 66 |
| 4 | 60 |
| 5 | 70 |
| 6 | 72 |
| 7 | 76 |
| 8 | 80 |

Compute by hand (i.e., calculator) the estimates $\hat{\gamma}_0$, $\hat{\gamma}_1$, $\hat{\rho}_0$, and $\hat{\rho}_1$.

- 1.2 **Figure 1.1a** shows a plot of West Texas intermediate crude oil prices from January 2000 to October, 2009, and **Figure 1.1b** shows monthly average temperatures for Pennsylvania for January, 1990 to December, 2009. These two data sets in `tswge` are `wctude` and `patem`, respectively. For each of these realizations, plot the sample autocorrelations, periodogram, and a Parzen window-based spectral density estimate at the truncation point \(M = 2\sqrt{n}\). Explain how these plots describe (or fail to describe) the behavior in the data.

- 1.3 **Figure 1.25c** shows an AR spectral estimator (in dB) for the log airline data (the “non-log” data is in data set `airline` and the log data are in data set `airlog`). Plot the periodogram and windowed spectral density estimators for these data using a Parzen window-based spectral density estimates at truncation points \(M = 2\sqrt{n}\), \(M = 10\), and \(M = 75\). (All in dB.) Compare and contrast the four spectral density estimates you obtain and also compare them with the AR spectral density estimator in **Figure 1.25** regarding the ability to see the less dominant spectral peaks associated with the higher frequencies.

- 1.4 Following are displayed three sets of figures each containing four plots. The first set shows four realizations of length \(n = 100\) each generated from a time series model. The second set contains four autocorrelation functions based on the models used to generate realizations (in random order), and the third set displays the four spectral densities. Match each realization with the corresponding autocorrelations and spectral density. Explain your answers.

![](img/a0e0259119deb8c7b41dfd4f664e541d_80_0.png)

1.5 The data set fig1.21a in the R package tswge contains the realization of length n = 250 shown in Figure 1.21a. Notice that the data and the spectral density (but not the autocorrelations) show evidence of two frequencies, a lower one at about f = 0.05 and a higher frequency of about f = 0.33. Find the Parzen spectral density estimate for this realization with M = 31. Plot this spectral density estimate in dB (10 log 10) and again without taking the logarithms. Comment on the information visible in the spectral density estimates concerning the two dominant frequencies. What impact has plotting the logarithm (as dB) had?

1.6 Generate a realization of length n = 100 from the signal-plus-noise model

$X_t = 3\cos(2\pi(0.05)t) + 1.5\cos(2\pi(0.35)t + 2) + a(t),$

where $a_t$ is $N(0,1)$ white noise. For these data, plot the

- a. Realization
- b. Sample autocorrelations
- c. Periodogram
- d. Parzen window spectral density estimator with default truncation point

Discuss cyclic features of the data that can be seen from each of the plots. Which of these plots provide the best indication of the two dominant frequencies (i.e., 0.05 and 0.35) in the data?

NOTE: A realization from the model

$X_t = c_1\cos(2\pi f_1 t) + c_2\cos(2\pi f_2 t) + N_t,$

where $N_t$ is normal (0,1) white noise can be obtained using the tswge R function gen.sigplusnoise.wge(n, b0, b1, coef, freq, psi, phi, vara, plot, sn). See Appendix 1B for details.

1.7 Find a time series data set (on the internet, etc.) not discussed in the book or in class. For this time series:

- a. Plot the time series realization
- b. Plot the sample autocorrelations. Write code (in R or otherwise) to calculate the sample autocorrelations (i.e., do not use a prewritten function for this.)
- c. Describe the behavior (wandering, periodic, etc.) in the realization and how that behavior manifests itself in the sample autocorrelations
- d. Plot the periodogram
- e. Plot the Parzen spectral density estimate using the default truncation point $2\sqrt{n}$. Describe the behavior (wandering, periodic, etc.) in the realization and how that behavior manifests itself in the spectral estimators

Hint: You can use the tswge function plotts.sample.wge.

### Theoretical Problems

1.8 Using the definition of autocovariance of a stationary process, show that it does not matter whether we look backward or forward in time; that is $\operatorname{Cov}(Z_t, Z_{t+k}) = \operatorname{Cov}(Z_t, Z_{t-k}) = \gamma_k.$

1.9 Consider the stochastic process $Z_t = a_t$ where $a_t$ is drawn independently for any $t$ and where the distribution of $a_t$ is given by $a_t = \begin{cases} c \text{ with probability } \frac12 \\ -c \text{ with probability } \frac12 \end{cases}$ for $c > 0.$

- a. Is the process $Z_t$ stationary? Why or why not?

b. What are the values of the parameters $\mu$, $\gamma_0$, $\gamma_1$, and $\gamma_j$, with $j>1$ for this process?

1.10 Show that the sum of $k$ uncorrelated covariance stationary processes is also covariance stationary

1.11 Let $X(t)=\cos(2\pi(0.025t)+\psi_1)+1.5\cos(2\pi(0.1t)+\psi_2)+2\cos(2\pi(0.15t)+\psi_3)$ be the time series given in Example 1.7b, Equation 1.35. Show that $X(t)$ is covariance stationary and (using the results in Example 1.3) find expressions for

- a. $\gamma(h)$  
- b. $\sigma_X^2$  
- c. $\rho(h)$

1.12 Let $Y_t$ be given by

$$Y_t=C_1\cos(2\pi f_1t+\psi_1)+N_t,\qquad t=0,\ \pm1,\ \ldots,$$
$$=H_t+N_t,$$

where  
$N_t$ is discrete white noise  
$\psi_1$ is distributed uniform $[0,2\pi]$  
$N_t$ and $\psi_1$ are uncorrelated for each $t$

Show that $Y_t$ is covariance stationary and that the autocovariance of $Y_t$ is given by

$$\gamma_k=\frac{C_1^2}{2}\cos 2\pi f_1k,\qquad k\ne0$$
$$=\frac{C_1^2}{2}+\sigma_N^2,\qquad k=0.$$

1.13 Let $Z_t$, $t=0,\ \pm1,\ \ldots$, be independent normal random variables each with mean 0 and variance $\sigma^2$, and let $a$, $b$, and $c$ be constants. Which, if any, of the following processes are stationary? For each stationary process, specify the mean and covariance function

- a. $X_t=a+bZ_t+cZ_{t-1}$  
- b. $X_t=a+bZ_0$  
- c. $X_t=Z_t\cos(ct)+Z_{t-1}\sin(ct)$
