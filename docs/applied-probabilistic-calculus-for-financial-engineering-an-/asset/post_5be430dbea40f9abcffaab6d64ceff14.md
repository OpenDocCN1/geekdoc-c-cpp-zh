
Implements the differential evolution algorithm for global optimization of a real-valued function of a real-valued parameter vector.

| Field | Value |
|---|---|
| Version | 2.2-4 |
| Depends | parallel |
| Suggests | foreach, iterators, colorspace, lattice |
| Published | 2016-12-19 |
| Author | David Ardia [aut], Katharine Mullen [aut, cre], Brian Peterson [aut], Joshua Ulrich [aut], Kris Boudt [ctb] |
| Maintainer | `Katharine Mullen <mullenkate@gmail.com>` |
| License | GPL-2 \| GPL-3 [expanded from: GPL (≥ 2)] |
| NeedsCompilation | yes |
| Citation | DEoptim citation info |
| Materials | README NEWS |
| In views | Optimization |
| CRAN checks | DEoptim results |

## Downloads:

| Resource | Details |
|---|---|
| Reference manual | DEoptim.pdf |
| Vignettes | DEoptim: An R Package for Differential Evolution<br>Large scale portfolio optimization with DEoptim |
| Package source | DEoptim_2.2-4.tar.gz |
| Windows binaries | r-devel: DEoptim_2.2-4.zip, r-release: DEoptim_2.2-4.zip, r-oldrel: DEoptim_2.2-4.zip |
| OS X Mavericks binaries | r-release: DEoptim_2.2-4.tgz, r-oldrel: DEoptim_2.2-4.tgz |
| Old sources | DEoptim archive |

## Reverse Dependencies:

| Type | Packages |
|---|---|
| Reverse depends | EcoHydRology, galts, IBHM, likeLTD, micEconCES, quicksky, selectMeta |
| Reverse imports | BBEST, CEGO, covmat, DstarM, FuzzyStatProb, MSGARCH, SpaDES |
| Reverse suggests | BayesianTools, MSCMT, nanop, npsp, PortfolioAnalytics, RcppDE, SACOBRA, SPOT |

## Examples from CRAN:

Use the following two examples, in R, to illustrate the use of the aforementioned approach in portfolio optimization:

## DEoptim: Differential Evolution Optimization

### Description

Performs evolutionary global optimization via the differential evolution algorithm.

### Usage

```r
DEoptim(fn, lower, upper, control = DEoptim.control(), ..., fnMap=NULL)
```

### Arguments

- `fn` the function to be optimized (minimized). The function should have as its first argument the vector of real-valued parameters to optimize, and return a scalar real result. NA and NaN values are not allowed.
- `lower, upper` two vectors specifying scalar real lower and upper bounds on each parameter to be optimized, so that the i-th element of lower and upper applies to the ith parameter. The implementation searches between lower and upper for the global optimum (minimum) of fn.
- `control` a list of control parameters; see `DEoptim.control`.
- `fnMap` an optional function that will be run after each population is created, but before the population is passed to the objective function. This allows the user to impose integer/cardinality constraints.
- `...` further arguments to be passed to fn.

### Details

DEoptim performs optimization (minimization) of fn. The control argument is a list; see the help file for DEoptim.control for details.

The R implementation of DE, DEoptim, was first published on the Comprehensive R Archive Network (CRAN) in 2005 by David Ardia. Early versions were written in pure R. Since version 2.0-0 (published on CRAN in 2009), the package has relied on an interface to a C implementation of DE, which is significantly faster on most problems as compared to the implementation in pure R.

It is important to emphasize that the result of `DEoptim` is a random variable, that is, different results may be obtained when the algorithm is run repeatedly with the same settings. Hence, the user should set the random seed if they want to reproduce the results, for example, by setting `set.seed(1234)` before the call of `DEoptim`.

`DEoptim` relies on repeated evaluation of the objective function in order to move the population toward a global minimum. Users interested in making `DEoptim` run as fast as possible should consider using the package in parallel mode (so that all CPUs available are used), and also ensure that the evaluation of the objective function is as efficient as possible (e.g., by using vectorization in pure R code, or writing parts of the objective function in a lower level language like C or Fortran).

Further details and examples of the R package `DEoptim` can be found in Mullen et al. (2011) and Ardia et al. (2011a, 2011b) or look at the package's vignette by typing `vignette("DEoptim")`. Also, an illustration of the package usage for a high-dimensional nonlinear portfolio optimization problem is available by typing `vignette("DEoptimPortfolioOptimization")`.

Please cite the package in publications. Use `citation("DEoptim")`.

### Value

The output of the function `DEoptim` is a member of the S3 class `DEoptim`. More precisely, this is a list (of length 2) containing the following elements:

- `optim`, a list containing the following elements:
  - `bestmem`: the best set of parameters found.
  - `bestval`: the value of fn corresponding to bestmem.
  - `nfeval`: number of function evaluations.
  - `iter`: number of procedure iterations.
- `member`, a list containing the following elements:
  - `lower`: the lower boundary.
  - `upper`: the upper boundary.
  - `bestvalit`: the best value of fn at each iteration.
  - `bestmemit`: the best member at each iteration.
  - `pop`: the population generated at the last iteration.
  - `storepop`: a list containing the intermediate populations.

Members of the class `DEoptim` have a `plot` method that accepts the argument `plot.type`. `plot.type = "bestmemit"` results in a plot of the parameter values that represent the lowest value of the objective function in each generation. `plot.type = "bestvalit"` plots the best value of the objective function in each generation. Finally, `plot.type = "storepop"` results in a plot of stored populations (which are only available if these have been saved by setting the control argument of `DEoptim()` appropriately). Storing intermediate populations allows us to examine the progress of the optimization in detail. A summary method also exists and returns the best parameter vector, the best value of the objective function, the number of generations optimization ran, and the number of times the objective function was evaluated.

### Note

DE is a search heuristic introduced by Storn and Price (1997). Its remarkable performance as a global optimization algorithm on continuous numerical minimization problems has been extensively explored. DE belongs to the class of genetic algorithms that use biology-inspired operations of crossover, mutation, and selection on a population in order to minimize an objective function over the course of successive generations. As with other evolutionary algorithms, DE solves optimization problems by evolving a population of candidate solutions using alteration and selection operators. DE uses floating-point instead of bit string encoding of population members, and arithmetic operations instead of logical operations in mutation. DE is particularly well suited to find the global optimum of a real-valued function of real-valued parameters, and does not require that the function be either continuous or differentiable.

Let NP denote the number of parameter vectors (members) x ∈ R^k in the population. In order to create the initial generation, NP guesses for the optimal value of the parameter vector are made, either using random values between lower and upper bounds (defined by the user) or using values given by the user. Each generation involves creation of a new population from the current population members. This is accomplished using differential mutation of the population members. An initial mutant parameter vector v_i is created by choosing three members of the population, x_{r0}, x_{r1}, and x_{r2}, at random. Then v_i is generated as

v_i = x_{r0} + F(x_{r1} - x_{r2})

where F is the differential weighting factor, effective values for which are typically between 0 and 1. After the first mutation operation, mutation is continued until d mutations have been made, with a crossover probability CR ∈ [0, 1]. The crossover probability CR controls the fraction of the parameter values that are copied from the mutant. If an element of the trial parameter vector is found to violate the bounds after mutation and crossover, it is reset in such a way that the bounds are respected (with the specific protocol depending on the implementation). Then, the objective function values associated with the children are determined. If a trial vector has equal or lower objective function value than the previous vector, it replaces the previous vector in the population.
