'Dowd' original code can be downloaded from www.kevindowd.org/measuring-marketrisk/.

It should be noted that 'Dowd' offers both 'MMR2' and 'MMR1' toolboxes. Only 'MMR2' was ported to R. 'MMR2' is more recent version of 'MMR1' toolbox and they both have mostly similar function. The toolbox mainly contains different parametric and nonparametric methods for measurement of market risk as well as back-testing risk measurement methods.

| Depends | R (>= 3.0.0), bootstrap, MASS, forecast |
| Suggests | PerformanceAnalytics, testthat |
| License | GPL |
| Needs Compilation | no |
| Repository | CRAN |
| Date/Publication | 2016-03-11 00:45:03 |

# Worked Example (a):

[6] `AmericanPutESBinomial` Estimates **Expected Shortfall (ES)** of American Vanilla *put* Using Binomial Tree.

# Description

Estimates ES of American Put Option using binomial tree to price the option and historical method to compute the Value-at-Risk (VaR).

# Usage

```
AmericanPutESBinomial(amountInvested, stockPrice, strike, r, volatility, maturity, numberSteps, cl, hp)
```

# Arguments

| amountInvested | Total amount paid for the Put Option. |
| stockPrice | Stock price of underlying stock. |
| strike | Strike price of the option. |
| r | Risk-free rate. |
| volatility | Volatility of the underlying stock. |
| maturity | Time to maturity of the option, in days. |
| numberSteps | The number of time-steps considered for the binomial model. |
| cl | Confidence level for which VaR is computed. |
| hp | Holding period of the option in days. |