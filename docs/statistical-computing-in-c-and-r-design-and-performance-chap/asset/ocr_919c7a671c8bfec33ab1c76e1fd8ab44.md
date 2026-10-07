# 318

# NUMERICAL OPTIMIZATION

To illustrate the use of mle, consider the function

```
lfunc <- function(theta, xbar, n)-n*log(theta) + n*xbar*theta)
```

This evaluates the negative log-likelihood for an exponential distribution given the sample size n and the sample mean xbar. For optimization purposes, the values of n and xbar must be fixed and the fixed argument for mle can be used to handle this. The listing below demonstrates this with the same data that was used with our like class.

```
> set.seed(123)
> x0 <- rep(100, 1)
> library("stats")n> mle(lfunc, start = list(theta = .5), fixed = list(xbar = mean(x0),
+ n = length(x0)))
```

```
Call:
mle(lfunc, start = list(theta = 0.6), fixed = list(xbar = mean(x0),
  n = length(x0))
```

Coefficients:

| theta | xbar |
|---|---|
| 0.95628036 | 1.0451781100000000 |

# 8.6 Random search

Deterministic optimization methods such as the golden section and Newton's method provide practical alternatives to a global search strategy for finding the global minimizer of a function f. However, they are limited by their requirement of a good initial search location. The use of random number generators to find such locations can be quite effective. This raises the question of why use deterministic methods at all? Not simply search the entire optimization region with a sequence of random numbers? There are many methods that do precisely this. An overview of this area is provided by Spall (2003).

The simplest strategy is a blind search method where one simulates in the region of interest until, e.g., a suitable approximation to the minimizer has found. Spall (2003) shows that, under weak restrictions on f, the resulting sequence of approximate minimizers converge to the global minimizer with probability one. The approach is summarized formally in Algorithm 8.3 that requires a choice for the iteration counter parameters maxit.

# Algorithm 8.3 Blind random search

```
iter <- 0
Generate minTemp uniformly distributed on [a, b]
while iter < maxit do
  Generate U uniformly distributed on [a, b]
  if f(U) < f(minTemp) then
    minTemp = U
  end if
  iter <- iter + 1
end while
return minTemp
```

The ranSearch method below was added to Listing 8.8 directly implements Algorithm 8.3 using a ranGen object from Appendix E.