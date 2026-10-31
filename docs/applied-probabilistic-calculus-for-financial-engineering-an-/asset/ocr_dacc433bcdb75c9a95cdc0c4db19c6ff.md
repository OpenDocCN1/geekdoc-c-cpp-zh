optimization method). Currently, supported optimization methods include the following:

+   - Random portfolios
+   - Differential evolution
+   - Particle swarm optimization
+   - Generalized simulated annealing
+   - Linear and quadratic programming routines

The solver can be specified with the optimize_method argument in optimize.portfolio and optimize.portfolio.rebalancing. The optimize_method argument must be one of random, DEoptim, pso, GenSA, ROI, quadprog, glpk, or symphony. Additional information on random portfolios is provided further. The differential evolution algorithm is implemented via the DEoptim package, the particle swarm optimization algorithm via the pso package, the generalized simulated annealing via the GenSA package, and linear and quadratic programming are implemented via the ROI package that acts as an interface to the Rglpk, Rsymphony.

# Worked Example No. 2

PortfolioAnalytics-package

Numeric methods for optimization of portfolios

indexes
Six Major Economic Indexes

# Description

Monthly data of five indexes beginning on 2000 January, 31 and ending 2009 December, 31.

The following are the five financial indexes, together with inflation factors:

+   1) U.S. bonds
+   2) U.S. equities
+   3) International equities
+   4) Commodities
+   5) U.S. T-Bills
+   6) Inflation factors

# Usage

```
data(indexes)
```

# Format

CSV converted into xts object with monthly observations.

# Examples

```
data(indexes)
#preview the data
```