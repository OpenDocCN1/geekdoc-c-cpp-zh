```
vdist <- list(distribution="unif", min = -0.02, max = 0)
views <- COPViews(pick, vdist, 0.2, c("SP", "FTSE", "CAC", "DAX"))
posterior <- COPPosterior(marketDistribution, views)
optimalPortfolios <- fPort(myPosterior, spec = NULL, optimizer = "minriskPortfolio", inputData = NULL, numSimulations = 100)
## End
```

# 5 The CRAN package PerformanceAnalytics—providing a number of useful programs for investment risk analysis and portfolio performance.

| Package 'PerformanceAnalytics' | February 19, 2015 |
| Type | Package |
| Title | Econometric tools for performance and risk analysis |
| Version | 1.4.3541 |
| Date | 2014-09-15 04:39:58-0500 (Mon, Sep 15, 2014) |
| Description | Collection of econometric functions for performance and risk analysis. This package aims to aid practitioners and researchers in utilizing the latest research in analysis of nonnormal return streams. In general, it is most tested on return (rather than price) data on a regular scale, but most functions will work with irregular return data as well, and increasing numbers of functions will work with P&L or price data where possible |
| Imports | zoo |
| Depends | R (>= 3.0.0), xts (>= 0.9) |
| Suggests | Hmisc, MASS, quantmod, gamlss, gamlss.dist, robustbase, quantreg, gplots |
| License | GPL-2 | GPL-3 |
| URL | http://r-forge.r-project.org/projects/returnanalytics/ |
| Copyright | (c) 2004-2014 |
| Authors | Brian G. Peterson [cre, aut, cph], Peter Carl [aut, cph] |