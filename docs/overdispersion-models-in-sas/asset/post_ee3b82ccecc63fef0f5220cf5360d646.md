
# 224 Overdispersion Models in SAS

$$V(T) = m\{\text{Diag}(\pi) - \pi\pi^T\mathbf{1}+\rho^2(m-1)}, \quad (7.29)$$

where $\pi = (\pi_1, \pi_2, ..., \pi_d)$ is the vector of probabilities, $0 < \pi_i < 1$, $\sum_{i=1}^d \pi_i < 1$, and $\rho$ is the overdispersion parameter. Note that the probability associated with the gamma is

$$\pi_{d+1} = 1 - \sum_{i=1}^d \pi_i.$$ The moment structure given by equations (7.28) and (7.29) can be realized by a number of distributions with support in the usual multinomial space. We will refer to such distributions as overdispersed multinomial distributions (or models). We consider the Maximum Likelihood Estimation for two overdispersed Multinomial models, namely the Dirichlet-multinomial distribution, and the Random-clumped Multinomial distribution proposed by the authors of this paper.

If $t$ is a realization of $T$, $t = (t_1, t_2, ..., t_d)$ with $t_{d+1} = m - \sum_{i=1}^d t_i$, the probability function of the Dirichlet-multinomial (DM) distribution, due to Mosimann (1962), is by

$$P_{DM}(t; \pi, \rho) = \frac{m!}{t_1!t_2!...t_d!} \frac{\Gamma(c)}{\Gamma(m+c)} \frac{\prod_{i=1}^{d+1}\Gamma(t_i+c_i)}{\prod_{i=1}^{d+1}\Gamma(c_i)}, \quad (7.30)$$

where $c = \rho^2(1-\rho)$, $0 < \rho < 1$, and $\Gamma(\cdot)$ denotes the gamma function. Mean and variance of the Dirichlet-multinomial distribution are the same as those given by equations (7.28) and (7.29). The Dirichlet-multinomial distribution is a multivariate extension of the Beta-binomial distribution discussed in Section 4.2. If the conditional probability of $T|P$ is Multinomial($P;m$) and if $P$ is a Dirichlet distribution with probability density

$$f_D(P; \pi, \rho) = \frac{\Gamma(c)}{\prod_{i=1}^{d+1}\Gamma(c_i)} \prod_{i=1}^{d+1}P_i^{c_i-1}}, \quad (7.31)$$

then the unconditional distribution of $T$ is Dirichlet-multinomial. Mosimann (1962) refers to this distribution as the Compound Multinomial Distribution. This generalizes the Beta-binomial distribution to the multivariate case. The DM distribution possesses a number of interesting properties. For example, their margins are again DM, and in particular, the one-dimensional marginal is the Beta-binomial distribution. This observation turns out to be important in the computation of maximum likelihood estimates, as we shall see later.

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

## 7.8 The Random-clumped Multinomial Distribution

The second over-dispersed Multinomial model we will consider here was proposed by Morel and Nagaraj (1993) and Neerchal and Morel (1998). It is a multivariate generalization of the Random-clumped Multinomial distribution covered in Section 4.3. This model can be derived as follows.

Let $Y, Y_1^0, \dots, Y_m^0$ be independent and identically distributed Multinomial random variables with parameters $(\boldsymbol{\pi}; 1)$. The $(d+1)$ category has already been removed from all these Multinomial random vectors. Let $U_1, U_2, \dots, U_m$ be independent and identically distributed Uniform(0,1) random variables, and $\rho$ be any random variable, $0 < \rho < 1$. As in Section 4.3, define

$$Y_i = Y_i^0(U_i \le \rho) + Y_i^0(U_i > \rho), \quad i=1,2,\dots,m$$

where $I(\cdot)$ denotes an indicator function.

Now consider the random variable

$$\mathbf{T} = \sum_{i=1}^m Y_i$$

The mean and covariance matrix of $\mathbf{T}$ are as in equations (7.28) and (7.29). As the univariate version of the Random-clumped Binomial distribution in Chapter 4, the random vector $\mathbf{T}$ can be represented as

$$\mathbf{T} = (\mathbf{YN}) + (\mathbf{X|N}), \quad \quad (7.32)$$

where $N \sim \text{Binomial}(\rho; m)$ and $(\mathbf{X|N}) \sim \text{Multinomial}((1-\rho)\boldsymbol{\pi}; m)$ if $N < m$. The interpretation of the clustering mechanism of the Random-clumped Multinomial $T$ has been discussed in Section 4.3. Sutrachdar (2001) provides graphical representation of several scenarios depicting the cluster mechanism.

It can be shown that the probability function of the Random-clumped Multinomial (7.32) is given by

$$P_{\text{RCM}}(\mathbf{T}=\mathbf{t}) = \sum_{i=1}^{d+1} \dots P(\mathbf{X}_i=t_i), \quad (7.33)$$

where $\mathbf{X}_i$ is distributed as Multinomial($(1-\rho)\boldsymbol{\pi}; m)$ for $i=1,2,\dots,d$. The interpretation of the clustering mechanism of the Random-clumped Multinomial $T$ has been discussed in Section 4.3. Sutrachdar (2001) provides graphical representation of several scenarios depicting the cluster mechanism.
