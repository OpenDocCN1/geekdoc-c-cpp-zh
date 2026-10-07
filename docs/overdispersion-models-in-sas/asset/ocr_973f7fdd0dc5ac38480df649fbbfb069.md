Note that the output corresponding to the G-side model contains only a single covariance
parameter. The value is close to 1, which is the variance of the within-subject random effect used
in the simulation data. The estimated probability of success is 0.7723. The true value set in
the simulation is 0.8. Similarly for the R-side output, the estimated probability of success is
0.7480. Note that both estimates are biased low. This output consists of two covariance
parameters. The labeled CS corresponds to the between-subject covariance, and the
estimated Residual corresponds to the within-subject variance.

# 9.3 GEE Methodology for Binary and Count Data

For each subject $j$, $j=1,2,...,n$, let $Y_j = (Y_{j,1}, Y_{j,2},...,Y_{j,m_j})$ represent an $m_j$-dimensional
column vector of responses, and let $x_j=(x_{j,1}, x_{j,2},...,x_{j,m_j})$ denote an associated $m_j \times k$ matrix
of observed covariates, where $x_{j,i}=1,2,...,m_j$ represent a $k$-dimensional row vector. Let $\mu_j$
and $v(\mu_j)$ represent, respectively, the mean and the "natural variance" of $Y_{j,i}$, the latter being
variance of $Y_{j,i}$ when they are independent and belong to the exponential family. If
$Y_{j,i}$'s were either Bernoulli or Poisson-distributed, their corresponding natural variances would
be $\pi_{j,i}(1-\pi_{j,i})$ or $\lambda_{j,i}$, respectively. It is further assumed that $\mu_{j,i}$'s are related to the $x_{j,i}$'s
through a link function $g()$ such that $g(\mu_j)=x_j\beta$, where $eta$ is a $k$-dimensional column vector
of unknown parameters. The canonical links for the Bernoulli and Poisson distributions as set
in earlier chapters, are, the logit and logarithmic functions. Other links for the
Bernoulli distribution are the "identity," \|probit" and the "complementary log-log" functions.
The identity function may also be used as a link function for the Poisson case.

Let $A_j$ represent the $m_j \times m_j$ diagonal matrix of natural variances of the vector $Y_j$,
$A_j = \text{diag}(v(\mu_{j,1}), v(\mu_{j,2}),...,v(\mu_{j,m_j}))$. In order to apply the GEE methodology, one needs
first to define the correlation structure of $Y_j = (Y_{j,1}, Y_{j,2},...,Y_{j,m_j})$ through an $m_j \times m_j$
"working" correlation matrix $R_j(\alpha)$ such that

```
$A_j = A_j^{1/2}R_j(\alpha)A_j^{1/2}\phi,$
```

$\alpha$ is a vector of unknown parameters, and $\phi$ is the usual dispersion parameter of
distributions in the exponential family. Note that in the case of the Bernoulli, Poisson
and Multinomial distributions, $\phi=1$. The variance-covariance matrix $V_j$ (above) would equal