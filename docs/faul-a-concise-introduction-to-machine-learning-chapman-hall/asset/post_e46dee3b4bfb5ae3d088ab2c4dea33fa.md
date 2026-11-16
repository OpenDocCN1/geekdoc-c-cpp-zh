
![](img/d3c00252180686426c9e63ab889b535b_45_0.png)

Figure 2.9: The Poisson probability mass function and its cumulative distribution function for \(\lambda = 1\) (top row), \(\lambda = 5\) (middle row), and \(\lambda = 10\) (bottom row).

The Poisson distribution \(m \sim \text{Po}(\lambda)\) gives the probability of \(m\) events occurring in the given time interval. The probability mass function is

\(\text{Po}(m|\lambda) = \frac{\lambda^m \exp(-\lambda)}{m!}.\) (2.8)

Both its expectation and variance are equal to \(\lambda\),

\(\text{E}[m] = \text{var}[m] = \lambda.\)

Of course, we are not just interested in experiments where the outcome is binary, but where the outcome can be any of \(K\) possible, mutually distinct outcomes. For example, the roll of a die would be one such experiment. The outcomes could be denoted \(\langle 1, 2, 3, 4, 5, 6 \rangle\) or \(\langle \blacksquare, \blacksquare, \blacksquare, \blacksquare, \blacksquare, \blacksquare \rangle\). However, it is convention to standardize the representation by using a 1-of-\(K\) representation. That is the random variable \(\mathbf{x}\) describing the outcome as a \(K\)-dimensional vector, where exactly one element \(x_k\) equals one and all the others are zero. For example, if in the die experiment \(x_4 = 1\), then \(\mathbf{x} = (0, 0, 0, 1, 0, 0)^T\) and it means that a four was rolled. The transpose \(^T\) is used, since all vector variables are column vectors throughout, but it is easier to write row vectors. Any experiments of a categorical nature can be described in this way.

The probability to get the \(k^{\text{th}}\) possible result, which means \(x_k = 1\), is denoted by \(\mu_k\). All probabilities are summarized in the vector \(\boldsymbol{\mu} = (\mu_1, \dots, \mu_K)^T\).

![](img/d3c00252180686426c9e63ab889b535b_46_0.png)

Figure 2.10: The categorical probability mass function and its cumulative distribution function for \(\boldsymbol{\mu} = (1/3, 1/2, 1/6)^T\).

The probabilities of all outcomes must sum to one,

\(\sum_{k=1}^K \mu_k = 1.\)

This defines the *categorical distribution* denoted \(\mathbf{x} \sim \text{Cat}(\boldsymbol{\mu})\) with probability density function

\(\text{Cat}(\mathbf{x}|\boldsymbol{\mu}) = p(x_k = 1|\boldsymbol{\mu}) = \prod_{k=1}^K \mu_k^{x_k}.\) (2.9)

Note that in the product all factors are 1 apart from one, since in \(\mathbf{x}\) all entries are 0 apart from one, which is 1. The categorical distribution can be viewed as a generalization of the Bernoulli distribution. The uniform distribution is a special case of it, as \(\mu_1 = \cdots = \mu_K = 1/K\).

Figure 2.10 illustrates the probability mass function of a categorical distribution where \(\boldsymbol{\mu} = (1/3, 1/2, 1/6)^T\). The cumulative distribution function is an irregular stair function. Both are drawn with regards to the indices in \(\mathbf{x}\). If the possible outcomes are ordered differently in \(\mathbf{x}\), the graphs will be different.

The expectation of the categorical distribution is calculated as

\(\mathbb{E}[\mathbf{x}] = \sum_{\mathbf{x}} \text{Cat}(\mathbf{x}|\boldsymbol{\mu})\mathbf{x} = \boldsymbol{\mu},\)

where the sum is over all possible values \(\mathbf{x}\) can take. Note that here we have made the step into a *multivariate distribution*, since \(\mathbf{x}\) is a vector, though one where all elements are zero apart from one, which is one.

Recall that the variance of a *univariate distribution* of the random variable \(x\) is given by \(\text{var}[x] = \mathbb{E}[(x - \mathbb{E}[x])^2] = \mathbb{E}[x^2] - \mathbb{E}[x]^2\). The multivariate equivalent is

\(\text{var}[\mathbf{x}] = \mathbb{E}[(\mathbf{x} - \mathbb{E}[\mathbf{x}])(\mathbf{x} - \mathbb{E}[\mathbf{x}])^T] = \mathbb{E}[\mathbf{x}\mathbf{x}^T] - \mathbb{E}[\mathbf{x}]\mathbb{E}[\mathbf{x}]^T.\) (2.10)

The result is a matrix, where the \(k^{\text{th}}\) diagonal entry gives how much \(x_k\) varies around the mean \(\mu_k\). The off-diagonal entries measure how much different components of \(\mathbf{x}\) influence each other.

Now, \(\mathbf{x}\) is a 1-of-K representation. If \(x_k = 1\) in \(\mathbf{x}\), then \(\mathbf{x}\mathbf{x}^T\) is a matrix with zero entries everywhere apart from the \(k^{\text{th}}\) diagonal element which has the entry 1. From this

\(\text{var}[\mathbf{x}] = \sum_{\mathbf{x}} \text{Cat}(\mathbf{x}|\boldsymbol{\mu})\mathbf{x}\mathbf{x}^T - \boldsymbol{\mu}\boldsymbol{\mu}^T = \text{diag}(\boldsymbol{\mu}) - \boldsymbol{\mu}\boldsymbol{\mu}^T\)

follows, where \(\text{diag}(\boldsymbol{\mu})\) denotes the matrix, where the off-diagonal elements are zero and the diagonal is given by the entries of \(\boldsymbol{\mu}\).

Note that the \(k^{\text{th}}\) diagonal entry of \(\text{var}[\mathbf{x}]\) is \(\mu_k - \mu_k^2 = \mu_k(1 - \mu_k)\). This is the variance of a Bernoulli distribution, where success is defined as the outcome being \(x_k = 1\) and failure as \(x_k = 0\). The \((k, l)\) off-diagonal entry is known as the \(\text{covariance } \text{cov}[x_k, x_l]\) between \(k^{\text{th}}\) and \(l^{\text{th}}\) element and is \(-\mu_k\mu_l\). This shows that the \(k^{\text{th}}\) and \(l^{\text{th}}\) component influence each other in a negative way, since if one is 1, the other has to be 0.

As with binary variables, we can also ask for the distribution of different combinations of outcomes, when the experiment is repeated \(N\) times. Each experiment gives a result vector \(\mathbf{x}_n, n = 1, \dots, N\). Let \(m_k\) be the number of times the outcome of the experiment is \(x_{nk} = 1\). Since \(x_{nk}\) is zero otherwise, we have

\(m_k = \sum_{n=1}^N x_{nk}\)

We are interested in the distribution of the tuple \(\mathbf{m} = (m_1, \dots, m_K)^T\) of length \(K\). It is actually of length \(K - 1\), since the numbers \(m_k\) are constrained by

\(\sum_{k=1}^K m_k = N,\) (2.11)

and hence \(m_K\) is given by \(m_K = N - m_1 - \dots - m_{K-1}\). The number of possibilities to generate a particular tuple is given by the *multinomial coefficient*,

\(\binom{N}{m_1 \dots m_K} = \frac{N!}{m_1! \dots m_K!}\)

Combinatorially, it is the number of ways one can put \(N\) balls into \(K\) bins where bin 1 contains \(m_1\) balls, bin 2 contains \(m_2\) objects and so on. Here \(0!\) is defined to be one. The binomial coefficient is the multinomial coefficient with \(m_1 = m\) and \(m_2 = N - m\).

The probability density function of the *multinomial distribution* \(\mathbf{m} \sim \text{Mult}(N, \boldsymbol{\mu})\) is then

\(\text{Mult}(\mathbf{m}|N, \boldsymbol{\mu}) = \binom{N}{m_1 \dots m_K} \prod_{k=1}^K \mu_k^{m_k}.\) (2.12)

![](img/d3c00252180686426c9e63ab889b535b_48_0.png)

Figure 2.11: The multinomial probability mass function for \(N=5\) and \(\boldsymbol{\mu} = (1/3, 1/2, 1/6)^T\).

Figure 2.11 shows the mass function of the multinomial distribution for \(N=5\) and \(\boldsymbol{\mu} = (1/3, 1/2, 1/6)^T\) as a bar graph. The graph only plots against \(m_1\) and \(m_2\), since \(m_3 = N - m_1 - m_2\) is given implicitly. On the right hand side we see that the probability mass is zero, whenever \(m_1 + m_2 > 5\) as required by the constraint given in 2.11. After zero, the smallest probability is for the tuple \((0, 0, 5)^T\) and is \(1/6^5\). The largest probability occurs three times for the tuples \((2, 2, 1)^T\), \((2, 3, 0)^T\) and \((1, 3, 1)^T\), since

\(\frac{5!}{2!2!1!} \left(\frac{1}{3}\right)^2 \left(\frac{1}{2}\right)^2 \left(\frac{1}{6}\right)^1 = \frac{5!}{2!3!0!} \left(\frac{1}{3}\right)^2 \left(\frac{1}{2}\right)^3 \left(\frac{1}{6}\right)^0\)

\(= \frac{5!}{1!3!1!} \left(\frac{1}{3}\right)^1 \left(\frac{1}{2}\right)^3 \left(\frac{1}{6}\right)^1 = \frac{5}{6^2}.\)

The expectation of the multinomial distribution is

\(\mathbb{E}[\mathbf{m}] = N\boldsymbol{\mu},\)

since we expect the \(\mu_k N\) experiments to result in the outcome \(x_k = 1\). The variance on the other hand is

\(\text{var}[\mathbf{m}] = N \text{diag}(\boldsymbol{\mu}) - \boldsymbol{\mu} \boldsymbol{\mu}^T.\)

It is \(N\) times the variance of a single experiment, which is described by the categorical distribution.
