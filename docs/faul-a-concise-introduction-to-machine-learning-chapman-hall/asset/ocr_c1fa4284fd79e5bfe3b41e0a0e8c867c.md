for some function $h$ of $x$ has to be calculated, arises often, but integrating analytically is too complex. Sampling methods are used to estimate the expectation described by the probability density function $f$. The expectation is approximated by

$\mathbb{E}[h] \approx \frac{1}{N} \sum_{n=1}^N h(x_n)$.

It needs to be ensured that all samples are independent. If some are dependent, the sample size $N$ needs to be increased to counter the effect that some samples might not give any new information.

The relative sizes of $h(x_n)$ to $f(x_n)$ can also skew the result. This happens, for example, if $h(x_n)$ is large in areas where $f(x_n)$ is small and vice versa. Then the expectation is dominated by the few large values of $h$, even though the probability density is small in this region. Again, it is necessary to have a sufficiently large sample size $N$ to counter act this.

In this chapter, we introduce some general sampling methods. For a more thorough treatment see [10].

# 3.1 Inverse Transform Sampling

We need to be able to generate samples of the probability density function $f(x)$. We assume that we have an algorithm available that generates uniformly distributed random numbers in the interval (0, 1). The cumulative probability density function is given by

$F(x) = \int_{-\infty}^x f(t) dt$.

We assume that it is continuous and strictly monotonically increasing on the interval $[a, b)$ and 0 for $x \le a$ and 1 for $x \ge b$. It takes values in the interval $[0, 1]$. Let $y$ be drawn from the uniform distribution over (0, 1). Then there exists a unique number in $(a, b)$ such that $F(x) = y$, or in other words $x = F^{-1}(y)$. Then $x$ is a continuous random variable with cumulative distribution function $F(x)$ and hence probability density function $f(x)$. This technique is known as inverse transform sampling. It is also known as inverse transformation, inverse sampling, inverse probability integral transform, and Smirnov transform.

We need to show that for $x = F^{-1}(y)$, we have indeed $p(x \le \hat{x}) = F(\hat{x})$ for a given value $\hat{x}$. Firstly,

$p(x \le \hat{x}) = p(F^{-1}(y) \le \hat{x})$

by the definition for $x$. Next, it follows from $F$ and subsequently $F^{-1}$ being strictly monotonically increasing that $F^{-1}(y) \le \hat{x}$ if and only if $y \le F(\hat{x})$. Lastly, since $y$ is from the uniform distribution on (0, 1), the probability of $y$ being less than or equal to $F(\hat{x})$ is in fact $F(\hat{x})$ itself and the assertion follows.