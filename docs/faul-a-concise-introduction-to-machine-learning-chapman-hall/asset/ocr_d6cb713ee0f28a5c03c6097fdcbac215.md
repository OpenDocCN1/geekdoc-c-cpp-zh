mass is concentrated within the simplex. Therefore, in some literature, the parameters of the Dirichlet distribution are given as \(\alpha \mu\), where

\(\alpha = \alpha_0 = \sum_{k=1}^K \alpha_k,\)
\(\mu = \left( \frac{\alpha_1}{\alpha_0}, \dots, \frac{\alpha_K}{\alpha_0} \right)^T.\)
(2.17)

In this case, \(\alpha\) is known as the (single) *concentration parameter*, while \(\mu\) is the *base distribution*. It is also the expectation of the distribution and satisfies the constraint

\(\sum_{k=1}^K \mu_k = 1.\)

With this notation,

\(\text{var}[x_j] = \frac{1}{\alpha + 1} \mu_j (1 - \mu_j),\)
\(\text{cov}[x_j, x_k] = \frac{1}{\alpha + 1} \mu_j \mu_k.\)

We have already seen that, if \(\alpha = 1\), the Dirichlet distribution is the uniform distribution. This means all distributions \(\mathbf{x}\) are equally likely. If \(\alpha\) tends to infinity, then only distributions which are themselves nearly uniform distributions become likely. The Dirichlet probability density function becomes infinitely peaked around the uniform distribution given by \(\mathbf{x} = (1/K, \dots, 1/K)^T\). In Figure 2.23, \(\alpha_0 = \alpha\) is largest for \(\alpha = (5, 5, 5)^T\) and the probability mass is concentrated around \((1/3, 1/3, 1/3)\), which describes the uniform distribution for three possible outcomes.

If \(\alpha\) tends to zero, let \(\mu_k\) be the component which is largest, i.e. \(\mu_k > \mu_j\) for all \(j \neq k\). Then the Dirichlet distribution tends to be peaked at this corner of the simplex. If there are several components with the same largest value, it tends to peaks at these corners, while it is zero everywhere else.

Both the beta distribution and the Dirichlet distribution can be illustrated by the *Pólya urn model*. Imagine an urn which contains balls of \(K\) different colours. For the beta distribution, these are two colours. Initially the urn contains \(\alpha_1\) balls of colour 1, \(\alpha_2\) balls of colour 2, and so on. As given in Equation 2.17, the total number of balls is the concentration \(\alpha\) and the initial proportions are given by the base distribution \(\mu\).

Now, each time a ball is drawn from the urn and replaced, but also another ball of the same colour is added, until the urn contains \(N\) balls. Since the colour drawn is random, the final number of balls of each colour is a random variable. However, it is influenced by the initial proportion of balls. If initially there are only balls of one colour, then the outcome is determined, because then the urn will continue to contain only balls of one colour. If there are disproportionally more balls of that one colour, we would expect there also to be more balls of that