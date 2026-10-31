
```
> 
> #1 stockPortfolio-package
> # Build and manage stock models and portfolios
> 
> #===> two examples of downloading data <===#
> ## Not run: grEx1 <- getReturns(c('C', 'BAC'), start='2004-01-01', end='2008-12-31')
> ## Not run: grEx2 <- getReturns(c('KEY', 'WFC', 'JPM', 'AMR',
'BIIB', 'AMGN'))
> #===> build four models <===#
> data(stock99)
> data(stock94Info)
> non <- stockModel(stock99, drop=25, model='none',
+ industry=stock94Info$industry)
> sim <- stockModel(stock99, model='SIM',
+ industry=stock94Info$industry, index=25)
> ccm <- stockModel(stock99, drop=25, model='CCM',
+ industry=stock94Info$industry)
> mgm <- stockModel(stock99, drop=25, model='MGM',
+ industry=stock94Info$industry)
> #===> build optimal portfolios <===#
> opNon <- optimalPort(non)
> opSim <- optimalPort(sim)
> opCcm <- optimalPort(ccm)
> opMgm <- optimalPort(mgm)
> #===> test portfolios on 2004-9 <===#
> data(stock04)
> tpNon <- testPort(stock04, opNon)
Warning message:
In testPort(stock04, opNon) : Allocation X was standardized
> tpSim <- testPort(stock04, opSim)
Warning message:
In testPort(stock04, opSim) : Allocation X was standardized
> tpCcm <- testPort(stock04, opCcm)
Warning message:
In testPort(stock04, opCcm) : Allocation X was standardized
> tpMgm <- testPort(stock04, opMgm)
Warning message:
In testPort(stock04, opMgm) : Allocation X was standardized
> 
> #===> compare performances <===#
> plot(tpNon)
> # Figure 5.4b StockPortfolio-1
```

![](img/551ca8853d2ba8528201e7a57e5006b4_414_0.png)

Figure 5.6 StockPortfolio-3.

![](img/551ca8853d2ba8528201e7a57e5006b4_414_1.png)

Figure 5.7 StockPortfolio-4.

```
> # Figure 5.7 StockPortfolio-4
> legend('topleft', col=1:4, lty=1:4, legend=c('none', 'SIM',
+ 'CCM', 'MGM'))
> # Figure 5.8 StockPortfolio-5
```

## 5.6.3 Worked Example 3: The Black-Litterman Asset

![](img/551ca8853d2ba8528201e7a57e5006b4_414_2.png)

Figure 5.8 StockPortfolio-5. SIM (Grupo Simec SAB de CV) – Computing and Technology, CCM – Medical Services, and MGM – MGM Resorts International.

## Review Questions and Exercises

- 1. At the heart of traditional performance analysis are two factors $\alpha$ and $\beta$. Briefly describe these two factors, giving some common examples.

- 2. Describe and contrast investors who are
- a. risk-averse
- b. risk-neutral, and
- c. risk-loving

Suggest some useful approaches suitable for each one of these three types of investors.

- 3. *Literature Survey:*

A considerable amount of literature has been developed in the areas supporting the analytical approaches to assets allocation. Much of these materials are readily available in the Internet sources. A typical example is the following paper by Robert Merton (1973) available at [econpapers.repec.org/article/ecmemeetrp/default38.htm](https://econpapers.repec.org/article/ecmemeetrp/default38.htm).

- a. *Study* this online paper and
- b. *Comment* on the following issues:

> > “We use the structure imposed by Merton’s (1973) ICAPM to obtain monthly estimates of the market-level risk-return relationship from the cross-section of equity returns. Our econometric approach sidesteps the specification of time-series models for the conditional risk premium and volatility of the market portfolio. We show that the risk-return relation is mostly positive but varies considerably over time. It co-varies positively with counter-cyclical state variables. The relationship between the risk premium and hedge-related risk also exhibits strong time-varying, which supports the empirical evidence that aggregate risk aversion varies over time. Finally, the ICAPM’s two components of the risk premium show distinctly different cyclical properties. The volatility component exhibits a counter-cyclical pattern whereas the hedging component is less related to the business cycle and falls below zero for extended periods. This suggests the market serves an important hedging role for long-term investors.”

*These issues are found in a paper by*  
Brandt, M. W. and Wang, L. P. (2010) Measuring the time-varying risk-return relation from the cross-section of equity returns.

- c. *Do you agree, or disagree* with the conclusions in this paper? And why?

## 4 An exercise in financial modeling for assets allocation.

## The GARCH Process and the CRAN Package tseries

## The generalized autoregressive conditional heteroskedasticity process

The generalized autoregressive conditional heteroskedasticity (GARCH) process is an econometric term developed in 1982 by Robert F. Engle, an economist and the 2003 winner of the Nobel Memorial Prize for Economics, to describe an approach to estimate volatility in financial markets. There are several forms of GARCH modeling. The GARCH process is often preferred by financial modeling professionals because it provides a more real-world context than other forms when trying to predict the prices and rates of financial instruments.

The general process for a GARCH model involves three steps:

- 1) The first is to estimate a best-fitting autoregressive model.
- 2) The second is to compute autocorrelations of the error term.
- 3) The third is to test for significance.

GARCH models are used by financial professionals in several areas, including trading, investing, hedging, and dealing. Two other widely used approaches to estimate and predict financial volatility are as follows:

- - The classic historical volatility (VolSD) method
- - The exponentially weighted moving average volatility (VolEWMA) method.

## The GARCH Process

GARCH models help to describe financial markets in which volatility can change, becoming more volatile during periods of financial crises or world events and less volatile during periods of relatively calm and steady economic growth. On a plot of returns, for example, stock returns may look relatively uniform for the years leading up to a financial crisis such as the one in 2007. In the time period following the onset of a crisis, however, returns may swing wildly from negative to positive territory. Moreover, the increased volatility may be predictive of volatility going forward. Volatility may then return to levels resembling that of precrisis levels or be more uniform going forward. A simple regression model does not account for this variation in volatility exhibited in financial markets and is not representative of the "black swan" events that occur more than one would predict.

## GARCH Models for Asset Returns

GARCH processes differ from homoskedastic models, which assume constant volatility and are used in basic ordinary least squares (OLS) analysis. OLS aims to minimize the deviations between data points and a regression line to fit those points. With asset returns, volatility seems to vary during certain periods of time and depends on past variance, making a homoskedastic model not optimal or suitable.

GARCH processes, being autoregressive, depend on past squared observations and past variances to model for current variance. They are widely used in finance owing to their effectiveness in modeling asset returns and inflation. A GARCH process aims to minimize errors in forecasting by accounting for errors in prior forecasting, enhancing the accuracy of ongoing predictions.

More on the GARCH Process: http://www.investopedia.com/terms/generalizedautoregressiveconditionalheteroskedasticity.asp#ixzz4XwGOV3MI

And now consider a CRAN package based on GARCH:

## Computational Finance

| Description | Time series analysis and computational finance. |
| Depends | R (>= 2.10.0) |
| Imports | graphics, stats, utils, quadprog, zoo |
| License | GPL-2 |
| NeedsCompilation | yes |
| Author | Adrian Trapetti [aut],
Kurt Hornik [aut, cre],
Blake LeBaron [ctb] (BDS test code) |
| Maintainer | Kurt Hornik <Kurt.Hornik@R-project.org> |
| Repository | CRAN |
| Date/Publication | 2017-01-17 12:33:40 |
| Description | Download historical financial data from a given data provider over the WWW. |

## Usage

```
get.hist.quote{instrument = "*gdax*", start, end,
quote = c("Open", "High", "Low", "Close"),
provider = c("yahoo", "oanda"),
method = NULL,
origin = "1899-12-30",
compression = "d",
retclass = c("zoo", "ts"),
quiet = FALSE,
drop = FALSE}
```
