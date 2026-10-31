```
> 
> #1 stockPortfolio-package
> # Build and manage stock models and portfolios
> 
> #===> two examples of downloading data <===#
> ## Not run: grEx1 <- getReturns(c('C', 'BAC'), start='2004-01-
01', end='2008-12-31')
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