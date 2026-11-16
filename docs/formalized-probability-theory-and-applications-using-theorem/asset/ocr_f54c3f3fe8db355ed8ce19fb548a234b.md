where $\sum_i$ denotes the summation carried over all possible values of the random variable X. Another closely associated statistical characteristic is the nth moment of a random variable X, which is basically the expected value of the random variable X^n. Thus, the expectation and the first moment of a random variable represent the same statistical characteristic of a random variable. Another useful statistical characteristic of random variables is the measure of their dispersion from the average or the typical values.

The most widely used measures of dispersion are the standard deviation and the variance. The variance of a random variable X describes the difference between X and its expected value.

```
Var[X] = \sigma_x^2 = \begin{cases} \sum_i (x_i - E_x[X])^2 p_x(x_i), & \text{if } X \text{ is discrete}; \\ \int_{-\infty}^{\infty} (x - E_x[X])^2 f_X(x) dx, & \text{if } X \text{ is continuous.} \end{cases} \quad (1.5)
```

The square root of the variance, which is always a positive number, is known as the standard deviation; which is a useful in the sense that it has the same units as X and thus can be compared directly with the expected value. Based on the expectation and variance characteristics of a random variable, we can find bounds for the tail distribution, i.e., the probability that a random variable assumes values that are far from its expectation. These bounds are usually calculated using the Markov's or the Chebyshev's inequalities. The Markov's inequality gives an upper bound for the probability that a non-negative random variable X is greater than or equal to some positive constant.

```
\text{Pr}(X \ge a) \le \frac{E_X[X]}{a} \quad (1.6)
```

Markov's inequality gives the best tail bound possible, for a nonnegative random variable, using the expectation for the random variable only. Chebyshev's inequality provides a significantly stronger tail bound than the Markov's inequality by using the variance of the random variable:

```
\text{Pr}(|X - E_X[X]| \ge a) \le \frac{Var[X]}{a^2} \quad (1.7)
```