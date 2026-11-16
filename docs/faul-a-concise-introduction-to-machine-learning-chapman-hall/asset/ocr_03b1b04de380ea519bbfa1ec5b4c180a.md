Returning to our example, the inverse $\mathbf{g}^{-1}$ is given by Equation (2.20). The matrix of partial derivatives is

$$ \begin{pmatrix} \frac{1}{2} & \frac{1}{2} \\ \frac{1}{2} & -\frac{1}{2} \end{pmatrix} $$

and the modulus of its determinant is 1/2. Both $x_1$ and $x_2$ were assumed to be independent and follow the standard normal distribution. Hence,

$$ f_Y(y) = \frac{1}{\sqrt{2\pi}} \exp \left( - \left( \frac{y_1 + y_2}{2} \right)^2 / 2 \right) \frac{1}{\sqrt{2\pi}} \exp \left( - \left( \frac{y_1 - y_2}{2} \right)^2 / 2 \right) \frac{1}{2} = \frac{1}{4\pi} \exp \left( \frac{y_1^2 + y_2^2}{4} \right) = \frac{1}{\sqrt{2}\sqrt{2\pi}} \exp \left( \left( \frac{y_1}{\sqrt{2}} \right)^2 / 2 \right) \frac{1}{\sqrt{2}\sqrt{2\pi}} \exp \left( \left( \frac{y_2}{\sqrt{2}} \right)^2 / 2 \right). $$

Therefore, the random variables $y_1$ and $y_2$ are independent. Both are normally distributed with mean 0 and standard deviation $\sqrt{2}$. Or in other words the variance is 2, which is the sum of the variances of $x_1$ and $x_2$.

More generally, if $y$ is a linear combination of independent normally distributed variables, i.e. $y = c_1 x_1 + \cdots + c_K x_K$, with $x_k \sim \mathcal{N}(\mu_k, \sigma_k^2)$, then $y$ is normally distributed with mean

$$ \mu = c_1 \mu_1 + \cdots + c_K \mu_K. $$

and variance

$$ \sigma^2 = c_1^2 \sigma_1^2 + \cdots + c_K^2 \sigma_K^2. $$

So far we have looked at different probability distributions and how to derive the probability density function for functions of random variables. In the next section we look at how to link this to data.

# 2.6 Conjugate Probability Distributions

The previous sections were concerned with probabilities and how to describe them. However, we are interested in describing data with probabilities. To this end, let us return to the experiment of flipping a coin, or more generally an experiment with two possible outcomes following a Bernoulli distribution $\text{Bern}(x|\mu)$, where $\mu$ is unknown. Let $x_1, \dots, x_N$ be $N$ observations of the experiment. The probability to observe this data $\mathcal{D} = \{x_1, \dots, x_N\}$ is

$$ p(\mathcal{D}|\mu) = \prod_{n=1}^N \text{Bern}(x_n|\mu) = \prod_{n=1}^N \mu^{x_n} (1-\mu)^{1-x_n} = \mu^{\sum_{n=1}^N x_n} (1-\mu)^{\sum_{n=1}^N (1-x_n)}. $$

This is known as the *likelihood* of the data $\mathcal{D}$. Now, $x_n$ only takes the values 0 and 1. If $m$ is the number of times we have $x_n = 1$ in the $N$ trials, then

$$ p(\mathcal{D}|\mu) = \mu^m (1-\mu)^{N-m}. $$