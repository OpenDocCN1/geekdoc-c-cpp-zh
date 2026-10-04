the spectral estimates are calculated (in our case 1/250, 2,250, ..., 125/250) along with the vectors p$db and p$dbz1, which contain the periodogram and the Parzen spectral density at truncation point M=31, respectively, at the frequencies in p$freq. Also output in this example are the vectors p$pz2 and p$dbz3 which contain the Parzen spectral density estimates using truncation points M=10 and M=50.

# EXERCISES

# Applied Problems

Use R to work problems 1.2 through 1.7.

+   1.1 The following data are annual sales of a hypothetical company in millions of dollars:

| Period | Sales |
|---||
| 1 | 76 |
| 2 | 70 |
| 3 | 66 |
| 4 | 60 |
| 5 | 70 |
| 6 | 72 |
| 7 | 76 |
| 8 | 80 |

Compute by hand (i.e., calculator) the estimates $\hat{\gamma}_0, \hat{\gamma}_1, \hat{ho}_0$, and $\hat{ho}_1$.

+   1.2 Figure 1.1a shows a plot of West Texas crude oil prices from January 2000 to October, 2009, and Figure 1.19b shows monthly average temperatures for Pennsylvania for January, 1990 to December, 2009. These two data sets in $tswage$ are $wcrude$ and $patemp$, respectively. For each of these realizations, plot the sample autocorrelations, periodogram, and a Parzen window-based spectral density estimator at the truncation point $M=2\sqrt{n}$. Explain how these plots describe (or fail to describe) the behavior in the data

+   1.3 Figure 1.2c shows an AR estimator (in dB) for the air line data (the "non-log" data is in set $airline$ and the log data are in set $airlog$). The periodogram and windowed spectral density estimators for these data using a Parzen window-based spectral density estimates at truncation points $M=2\sqrt{n}, M=10$, and $M=75$ (in dB). (All in dB) Compare and contrast the four spectral density estimates you obtain and also compare them with the AR spectral estimator in Figure 1.25 regarding the ability to see less dominant spectral peaks associated with the higher frequencies.

+   1.4 Following are displayed three sets of figures containing four plots. The first set shows four realizations of length $n=100$