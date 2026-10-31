# Example 1 in Multivariate Data Analysis – (see the illustrative example in Section 4.2.1)

# ANOVA Analysis

ANOVA (Analysis of Variance) may be achieved using the R function `anova()`, which is in the CRAN package stats. The standard usage form of this function is

```
```r
> anova(object, ...)
with arguments:
object= an object for model fitting (e.g. lm or glm).
... = additional objects of the same type.
```
```

# Example 2 in Multivariate Data Analysis

Consider some real econometric data as illustrated in the CRAN package for financial engineering analysis:

| Field | Value |
|---|---|
| **Package:** | ‘quantmod’: |
| **Type:** | Package |
| **Title:** | Quantitative Financial Modelling Framework |
| **Version:** | 0.4-7 |
| **Date:** | 2016-10-24 |
| **Depends:** | `xts (>= 0.9-0)`, `zoo`, `TTR (>= 0.2)`, `methods` |
| **Suggests:** | `DBI`, `RMySQL`, `RSQLite`, `timeSeries`, `XML`, `downloader`, `jsonlite (>=1.1)` |
| **Description:** | Specify, build, trade, and analyze quantitative financial trading strategies. |
| **LazyLoad:** | yes |
| **License:** | GPL-3 |
| **URL:** | http://www.quantmod.com<br>https://github.com/joshuaulrich/quantmod |
| **BugReports:** | https://github.com/joshuaulrich/quantmod/issues |
| **NeedsCompilation:** | yes |
| **Authors:** | Jeffrey A. Ryan [aut, cph],<br>Joshua M. Ulrich [cre, ctb],<br>Wouter Thielen [ctb] |
| **Maintainer:** | Joshua M. Ulrich <josh.m.ulrich@gmail.com> |
| **Repository:** | CRAN |
| **Date/Publication:** | 2016-10-24 23:30:16 adjustOHLC |