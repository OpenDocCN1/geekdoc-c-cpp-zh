variable $X$ that can be modeled using the Bernoulli distribution, with the probability of success $p = \frac{1}{6}$. For example, $X \sim \text{BERN}(p)$. You can easily determine, (16.1), that

$Pr(\text{rolling a } 4) = Pr(X=1) = f(1) = \left(\frac{1}{6}\right)\left(\frac{5}{6}\right)^{5} = \frac{1}{6}$

and, in much the same way, that $f(0) = \frac{5}{6}$. Furthermore, you'd have $\mu_{X} = \frac{1}{6}$ and $\sigma_{X}^{2} = \frac{1}{6} \times \frac{5}{6}$.

# 16.1.2 Binomial Distribution

The *binomial distribution* is the distribution of successes in $n$ trials involving binary discrete random variables. The role of the Bernoulli distribution is typically of a "building block" for more complicated distributions, like the binomial, which gives you more interesting results.

For example, suppose you define a random variable $X = \sum_{i=1}^{n} Y_{i}$, where $Y_{1}, Y_{2}, \dots, Y_{n}$ are each Bernoulli random variables corresponding to the same event, in order, the die roll with success defined as a 4. The new random variable $X$, a sum of Bernoulli random variables, now describes the number of successes in $n$ trials of the defined action. Providing that reasonable assumptions are satisfied, the probability distribution describes this success counts is binomial.

In mathematical terms, for a discrete random variable and a realization $X=x$, the binomial mass function $f$

> $f(x) = \binom{n}{x}p^{x}(1-p)^{n-x}; \quad x = (0,1,\dots,n)$

where

> $\binom{n}{x} = \frac{n!}{x!(n-x)!}$

is known as the *binomial coefficient*. (Recall the use of integer factorial operator $!$, as first discussed in Exercise 10.4 on page 203.) This coefficient, also referred to as a *combination*, accounts for all different orders in which you might observe $x$ successes throughout $n$ trials.

The parameters of the binomial distribution are $n$ and $p$, and the notation

$X \sim \text{BIN}(n,p)$

is used to indicate that $X$ follows a binomial distribution for $n$ trials with parameter $p$.

The following are the key points to remember:

+   - X can take only the values 0, 1, \dots, $n$ and represents the total number of successes.

+   - $p$ should be interpreted as "the probability of success at each trial." Therefore, $0 \le p \le 1$, and $n > 0$ is an integer interpreted as "the number of trials."