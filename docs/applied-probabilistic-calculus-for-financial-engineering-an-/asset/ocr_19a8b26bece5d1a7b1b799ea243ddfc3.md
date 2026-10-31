```
else{ ... }
return(r)
}
```

This simplistic strategy usually does not work all that well for gradient-based or Newton-type methods. It is likely to be acceptable when the solution is in the interior of the feasible region, but when the solution is on the boundary, optimization algorithm would have a difficult time converging.

Furthermore, when the solution is on the boundary, this strategy would make the algorithm converge to an inferior solution in the interior. However, for methods such as DE, which are not gradient based, this strategy might not be that bad.

Note that DEoptim stops if any NA or NaN value is obtained. Under these conditions: redefine the function to handle these values (for instance, set NA to Inf in ones objective function).

It is important to emphasize that the result of DEoptim is a random variable, that is, different results may be obtained when the algorithm is run repeatedly with the same settings. Hence, the user should set the random seed if they want to reproduce the results, for example, by setting set.seed(1234) before the call of DEoptim.

DEoptim depends on repeated evaluation of the objective function in order to move the population toward a global minimum. Users interested in making DEoptim run as fast as possible should consider using the package in parallel mode (so that all CPUs available are used), and also ensure that evaluation of the objective function is as efficient as possible (e.g., by using vectorization in pure R code, or writing parts of the objective function in a lower level language like C or Fortran).

Further details and examples of the R package DEoptim can be found in Mullen et al. (2011) and Ardia et al. (2011a, 2011b) or look at the package's vignette by typing vignette("DEoptim").

Also, an illustration of the package usage for a high-dimensional nonlinear portfolio optimization problem is available by typing vignette("DEoptim PortfolioOptimization").

# Remarks:

+   - A) Differential evolution is a search heuristic code introduced by Storn and Price (1997). Its remarkable performance as a global optimization algorithm on continuous numerical minimization problems has been extensively explored. DE belongs to the class of genetic algorithms that use biology-inspired operations of crossover, mutation, and selection on a population in order to minimize an objective function over the course of successive generations.
+   - B) As with other evolutionary algorithms, DE solves optimization problems by evolving a population of candidate solutions using alteration and selection operators. DE uses floating-point instead of bit string encoding of