# Chapter 5 Goodness-of-fit Tests for Overdispersed Binomial Models 119

Dean (1992) provides a methodology for obtaining tests for overdispersion with respect to a natural exponential. Several tests for extra-Binomial and extra-Poisson variance, similar to Tarone's test, can be obtained as special cases of Dean's methodology. We illustrate Dean's methodology using the log model discussed in Section 4.8 of Chapter 4. As before, let the probability of success $\pi_j, j=1,2,...,n$ depend on a k-dimensional row vector of covariates $x_j$ and a k-dimensional column vector of unknown parameters $eta$, via the logit link

```
$$\ln\left(\frac{\pi_j}{1-\pi_j}\right)=x_j\beta=\sum_{i=1}^k x_{ji}\beta_i$
```

Dean (1992) derived a score statistic for testing “$	au=0$” when the first two moments of the form

```
$E(T_j) = m_j\pi_j, \text{ and } Var(T_j) = m_j\pi_j(1-\pi_j)\{1+\tau(m_j-1)\}$
```

Dean's score statistic turned out be

```
$Z = \frac{\sum_{j=1}^n (t_j-m_j\hat{\pi}_j)^2 + \hat{\pi}_j^2(t_j-m_j\hat{\pi}_j)-t_j(1-\hat{\pi}_j)}{\hat{\pi}_j(1-\hat{\pi}_j)}}{\sqrt{2\sum_{j=1}^n m_j(m_j-1)}} (5.3)
```

Note that this score statistic (5.3) becomes when $\hat{\pi}_i=\hat{\pi}_n=\hat{\pi}$. Dean (1992) points out that the use of score statistic (5.3) is appropriate for arbitrary alternatives with the first two moments as indicated above. As noted earlier, the Beta-binomial and Random-clamped Binomial distributions are based on positively correlated Bernoullis with the above moment structure.

To illustrate the use of the score statistic (5.3) we revisit the Efron (1986) example from n=34 cities in El Salvador. The data are reported in Table 3.2. Recall that the outcome “number of cases testing for Toxoplasmosis ($t_j$)” out of the number of subjects sampled ($m_j$)” was analyzed as a function of the linear, quadratic, and cubic terms of standardized annual rainfall (inches) are shown in Program 5.2. We will skip the data statements since they are the same as those in Program 3.2.

Morel, Jorge, and Nagaraj Neeraraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.