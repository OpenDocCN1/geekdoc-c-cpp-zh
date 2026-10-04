
Generally, it's important to remember the following for any probability mass function based on a discrete random variable X:

- There are $k$ distinct outcomes $x_1, \dots, x_k$.
- For each $x_i$, where $i=\{1, \dots, k\}$, $0 \le \text{Pr}(X = x_i) \le 1$.
- $\sum_{i=1}^k \text{Pr}(X = x_i) = 1$.

## Mean and Variance of a Discrete Random Variable

It's useful to be able to describe or summarize properties of a random variable of interest as you would for raw data. The most useful two properties are the mean and variance, both of which depend upon the relevant distribution of probabilities associated with that random variable.

For some discrete random variable $X$, the mean $\mu_X$ (also referred to as the *expectation* or *expected value* $\mathbb{E}[X]$) is the “average outcome” that you expect over many realizations. Say X has $k$ possible outcomes, labeled $x_1, x_2, \dots, x_k$. Then you have to Pr:

```
\mu_X = \mathbb{E}[X] = x_1 \times \text{Pr}(X = x_1) + \dots + x_k \times \text{Pr}(X = x_k)
```

```
\sum_{i=1}^k x_i \text{Pr}(X = x_i) \quad (15.3)
```

Then to mean, simply multiply the numeric value of each outcome by its corresponding probability and sum the results. 

For a discrete random variable $X$, the variance $\sigma_X^2$, of Var$[X]$, quantifies the variability in the possible variances of $X$. Theoretically, in terms of expectations, it can be shown that $\sigma_X^2 = \text{Var}[X] = \mathbb{E}[X^2] - \mathbb{E}[X]^2$. As you can see, the calculation of the discrete random variable depends upon its mean $\mu_X$ and is as follows:

```
\sigma_X^2 = \text{Var}[X] = (x_1 - \mu_X)^2 \times \text{Pr}(X = x_1)
```

```
+ \dots + (x_k - \mu_X)^2 \times \text{Pr}(X = x_k)
```

```
\sum_{i=1}^k (x_i - \mu_X)^2 \text{Pr}(X = x_i) \quad (15.4)
```

Again, the procedure is straightforward—the variance is computed by squaring the differences between each realization and mean then multiplying by the corresponding probability of the occurrence before summing these products.

In practice, the probabilities associated with each outcome are unknown and estimated from observed data. Following that step, you apply the formulas in (15.3) and (15.4) to obtain estimates of the respective properties. Also, note that the general descriptions of mean and variance are the same as in Section 13.2—only they are now quantifying centrality and spread with respect to a random phenomenon.

Let's consider the gambling game with the possible realizations of the amount earned, X, and the associated probabilities specified in Table 15-1. With vector-oriented behavior (refer to Section 2.3.4), using R to calculate the mean and variance of X is easy. With the objects X.outcomes and X.prob from earlier, you can get the mean of X from the element-wise multiplication in the following:

```
R> mu <- sum(X.outcomes*X.prob)
R> mu.X
[1] -0.73
```

So, $\mu = -0.73$. By the same token, the following provides the variance of X:

```
R> var.X <- sum((X.outcomes-mu.X)^2*X.prob)
R> var.X
[1] 7.9371
```

You can also compute the standard deviation by taking the square root of the variance (recall the definitions in Section 13.2.4). This is done with the built-in sqrt command.

```
R> sd.X <- sqrt(var.X)
R> sd.X
[1] 2.817286
```

Based on these results, you can make several comments on the gambling game and its outcomes. The expected outcome of -0.73 suggests that, on average, you'll lose $0.73 per turn, with a standard deviation of about $2.82. These quantities are not, and not be one, of the specifically defined outcomes. They describe the behavior of the random mechanism over the long run.

## 15.2.3 Continuous Random Variables

Again following the definitions of variables from Chapter 13, a continuous random variable has no limit to the number of realizations. For a discrete random variable, it is natural to think of a specific outcome as an event and assign it a corresponding probability. Things are a little different when you're dealing with a continuous random variable, however. If you take the picnic example in Section 15.2.1, you can see that if you restrict the range of possible values of temperature measurement that you assume W could say, to between 40 and 90 degrees Fahrenheit (or, expressed more formally, 40 $\le W \le$ 90), there are still an infinite number of distinct values on that continuum. Measuring 59.1 degrees makes as sense as 

As such, it's not possible to assign probabilities to single temperatures; instead, you assign them to intervals. This is easier if you think about it. For example, the continuous function defined by Equation (15.5) yields a triangular shape, with an apex at 65. $f(w) = \begin{cases} \frac{w-40}{625} & \text{if } 40 \le w \le 65 \\ \frac{90-w}{625} & \text{if } 65 \le w \le 90 \\ 0 & \text{otherwise} \end{cases}$

The next lines make use of lower.w and upper.w to evaluate the correct result of $f(w)$ for the entries in w.
