density estimate at a variety of truncation points. You can use the following

```
```r
x = gen.sigplusnoise.wge(n = 250, coef = c(3,1), freq =
c(.1,.52),
psi = c(0,1), phi = 0, vara = 1)
pz = plotts.parzen.wge(x,m2 = c(10,50))
```
```

produces a plot of the periodogram in dB, Parzen spectral estimate with truncation point $M = 2\sqrt{250} = 31.6$ (rounds down to $M = 31$), along with the Parzen spectral estimators with truncation points $M = 10$ and $M = 50$. All plots are in dB. Also output are pz$freq which is a vector containing the frequencies at which the Parzen spectral estimates are calculated (in our case 1/250, 2/250, ..., 125/250) along with the vectors pz$db and pz$dbz1, which contain the periodogram and the Parzen spectral density at truncation point $M = 31$, respectively, evaluated at the frequencies in pz$freq. Also output in this example are the vectors pz$dbz2 and pz$dbz3 which contain the Parzen spectral density estimates using truncation points $M = 10$ and $M = 50$, respectively.

# EXERCISES

# Applied Problems

Use R to work problems 1.2 through 1.7.

1.1  The following data are annual sales of a hypothetical company in millions of dollars:

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