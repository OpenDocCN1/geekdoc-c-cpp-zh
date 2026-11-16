
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

## 2.6 Conjugate Probability Distributions

The previous sections were concerned with probabilities and how to describe them. However, we are interested in describing data with probabilities. To this end, let us return to the experiment of flipping a coin, or more generally an experiment with two possible outcomes following a Bernoulli distribution $\text{Bern}(x|\mu)$, where $\mu$ is unknown. Let $x_1, \dots, x_N$ be $N$ observations of the experiment. The probability to observe this data $\mathcal{D} = \{x_1, \dots, x_N\}$ is

$$ p(\mathcal{D}|\mu) = \prod_{n=1}^N \text{Bern}(x_n|\mu) = \prod_{n=1}^N \mu^{x_n} (1-\mu)^{1-x_n} = \mu^{\sum_{n=1}^N x_n} (1-\mu)^{\sum_{n=1}^N (1-x_n)}. $$

This is known as the *likelihood* of the data $\mathcal{D}$. Now, $x_n$ only takes the values 0 and 1. If $m$ is the number of times we have $x_n = 1$ in the $N$ trials, then

$$ p(\mathcal{D}|\mu) = \mu^m (1-\mu)^{N-m}. $$

The value of \(\mu\) can be estimated by maximizing the likelihood with respect to \(\mu\), since we want to choose the \(\mu\) which explains the data best.

The maximization is equivalent to maximizing the logarithm, which is valid, since the logarithm is a monotonically increasing function. This is the log likelihood:

\(\log p(\mathcal{D}|\mu) = m \log \mu + (N - m) \log(1 - \mu).\)

The location of the maximum is where the derivative with respect to \(\mu\) vanishes. The derivative is

\(\frac{d}{d\mu}p(\mathcal{D}|\mu) = \frac{m}{\mu} - \frac{N - m}{1 - \mu}.\)

Setting to zero, multiplying through by \(\mu(1 - \mu)\) and solving for \(\mu\) gives the maximum likelihood estimator

\(\mu_{\text{ML}} = \frac{m}{N}.\)

Returning to flipping the coin, if we happen to get tails (\(x_n = 0\)) three times in a row in three flips, then the maximum likelihood estimator is \(\mu_{\text{ML}} = 0\). The interpretation is that in all future flips we would continue to see tails. Equally, if we happen to flip heads (\(x_n = 1\)) three times in a row, the maximum likelihood estimator is \(\mu_{\text{ML}} = 1\). Both cases are realistic, but the conclusion is not and caused by the small number of trials. In general, to get a good maximum likelihood estimator for any parameter, many observations are necessary.

However, in real world applications such abundance of data might be a luxury. If we describe what we “believe” about \(\mu\), mathematically and then use Bayes’ rule to modify our “belief”, less data is necessary to estimate the parameter \(\mu\). It is the probability of success, and therefore \(\mu \in [0, 1]\). Thus, the beta distribution \(\text{Beta}(\mu|\alpha, \beta)\) lends itself to describe \(\mu\), where \(\alpha\) and \(\beta\) are known as *hyperparameters* and set to some reasonable initial values. This is the *prior distribution*. In the following, we will see how these parameters get updated with data becoming available.

The joint probability density function of \(\mu\) and \(m\) is the product of the likelihood and the prior

$$ f(\mu, m|N, \alpha, \beta) = p(\mathcal{D}|\mu)\text{Beta}(\mu|\alpha, \beta) = \mu^m(1-\mu)^{N-m} \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \mu^{\alpha-1}(1-\mu)^{\beta-1}. \tag{2.21} $$

The posterior density function of \(\mu\), \(f(\mu|m, N, \alpha, \beta)\), is proportional to the joint distribution following Bayes. The constant factors can be dropped when using the proportionality \(\propto\), and hence

$$ f(\mu|m, N, \alpha, \beta) \propto \mu^{m+\alpha-1}(1-\mu)^{N-m+\beta-1}. $$

It has the functional form of another, different beta distribution. Inserting the appropriate factor to ensure the integral over the distribution is one gives

$$ f(\mu|m, N, \alpha, \beta) = \frac{\Gamma(N + \alpha + \beta)}{\Gamma(m + \alpha)\Gamma(N - m + \beta)} \mu^{m+\alpha-1} (1 - \mu)^{N-m+\beta-1}. $$

Observing \( m \) successes and \( N - m \) failures changes the shape of the prior distribution to arrive at the posterior distribution. The order of successes and failures is irrelevant.

What is the probability of success after taking the data \( \mathcal{D} \) into account, \( p(x=1|\mathcal{D}) \)? The data is sufficiently specified by \( N \) and \( m \). There is no longer a single value for \( \mu \), but a posterior distribution over \( \mu \). All possible values are considered by taking the integral

$$ \begin{aligned} p(x=1|\mathcal{D}) &= \int_0^1 p(x=1|\mu) f(\mu|m, N, \alpha, \beta) d\mu \\ &= \int_0^1 \mu f(\mu|m, N, \alpha, \beta) d\mu = \mathbb{E}(\mu|m, N, \alpha, \beta) \\ &= \frac{m + \alpha}{N + \alpha + \beta}. \end{aligned} \tag{2.22} $$

Because of the inclusion of \( \alpha \) and \( \beta \), the probability can never become 0, even if \( m=0 \), or 1, even if \( m=N \), contrary to the maximum likelihood estimator. It incorporates the uncertainty caused by seeing only a finite set of data.

The above result no longer depends on \( \mu \). It is an example of a latent or hidden variable.

Figure 2.31 shows how the beta distribution changes from a prior distribution with \( \alpha = \beta = 2 \) as more data is observed. If 0 stands for tails when flipping a coin, the second to seventh plot illustrated a sequence of three times tails followed by three times heads. As more tails are observed, the mean of the distribution moves to the left, but with more observations of heads, it moves back right towards the centre. The last plot is after 100 coin flips, where an equal number of heads and tails are observed. The posterior distribution becomes more peaked around 1/2. As \( N \) increases, \( \alpha \) and \( \beta \) become relatively small compared to it, and \( p(x=1|\mathcal{D}) \) approaches the maximum likelihood estimator \( p_{ML} \) for this \( \mathcal{D} \).

As can be seen in Figure 2.31, this approach can be used in real-time learning, where data arrives sequentially, and predictions are updated when more knowledge is gained. It can also be used for large data sets, where it is not possible to load all data into memory at the same time.

The beta distribution is known as the *conjugate* distribution to the Bernoulli and binomial distribution. It was motivated by choosing a suitable prior distribution describing an unknown parameter (\( \mu \)). There is also a mathematical motivation, since the posterior distribution arising from Bayes' rule in this case has the same functional form as the prior and therefore can be determined in closed form. This is not always the case. When choosing appropriate distributions to describe the data, mathematical convenience should play a subordinate role to the data and expert knowledge.
