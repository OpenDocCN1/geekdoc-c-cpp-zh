$(1+t)^\alpha = \sum_{k=0}^{\infty} \binom{\alpha}{k} t^k,$ (31.8)

where

$\displaystyle \binom{\alpha}{k} = \frac{\alpha \cdot (\alpha - 1) \cdots (\alpha - k + 1)}{k!}$ (31.9)

is defined for any real number $\alpha$ and for $k = 0, 1, \ldots$. We’ll be applying this to the case $\alpha = \frac{1}{2}$ and $t = -\frac{37}{50}$, so that $1 - t = \frac{13}{50}$, so that evaluating Equation 31.8 will give us the value of the solution in Equation 31.7.

To do so requires summing an infinite series, however. The great insight is the realization that the sum of an infinite series can be estimated by looking at individual elements of the series.

# 31.5.1  Summing a Series by Sampling and Estimation

We now lay the foundations for all the Monte Carlo approaches to rendering, starting with a few simple applications of probability theory.

# 31.5.1.1  Finite Series

Suppose that we have a finite series

$A = a_1 + a_2 + a_3 + \cdots + a_{20},$ (31.10)

and we want to estimate the sum, $A$. We can do the following: Pick a random integer $i$ between 1 and 20 (with probability $1/20$ of picking each possible number), and let $X = 20a_i$. Then $X$ is a random variable. Its expected value is the weighted average of its values, with weights being the probabilities, that is,

$E[X] = (1/20)(20a_1) + (1/20)(20a_2) + \cdots + (1/20)(20a_{20})$ (31.11)

$= a_1 + a_2 + \cdots + a_{20}$ (31.12)

$= A.$ (31.13)

We’ve got a random variable whose expected value is the sum we’re seeking! By actually taking samples of this random variable and averaging them, we can approximate the sum.

> **Inline Exercise 31.1:** Suppose that all 20 numbers $a_1, a_2, \ldots$ are equal. What’s the variance of the random variable $X$? How many samples of $X$ do you need to take to get a good estimate of $A$ in this case?

In general, the variance of $X$ is related to how much the terms in the sequence vary: If all the terms are identical, then $X$ has no variance, for instance. It’s also related to the way we chose the terms, which happens to have been uniform, but we’ll use nonuniform samples in other examples later. When we apply these ideas to rendering, we will end up sampling among various paths along which light can travel; the value being computed will be the light transport along the path. Since some paths carry a lot of light (e.g., a direct path from a light source to your eye) and some carry very little, a large variance is present; to make estimates accurate