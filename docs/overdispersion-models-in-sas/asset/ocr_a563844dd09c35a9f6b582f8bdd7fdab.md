# 54 Overdispersion Models in SAS

Note that variance (3.6) can be written as

```
$$Var(\hat{\beta}) \equiv \phi \left(\\sum_{j=1}^{n} d_j v_j^{-1} d_j^{\top}\right)^{-1} \quad (3.7)$
```

For canonical links, equation (3.6) becomes

```
$$Var(\hat{\beta}) \equiv \phi(X^{\top}X)^{-1} \quad (0.8)$
```

# 3.3 An Oral Care Example

In order to illustrate the quasi-likelihood estimation procedure, consider the data in Table 3.1 taken from a clinical trial (Schulte et al., 1998) where $n=17$ subjects brushed their teeth for six consecutive weeks with an experimental dental paste. The pH was measured at the end of the study at four sites of each subject's mouth ($m=4$). It is believed that if the pH $\le 6.5$, the subject is at higher risk of oral disease. Note that pH measurements are related to the brushing habits, toothpaste used, food consumption, and genetic characteristics of the subject. Therefore, it will be natural to assume positive correlation among sites in each subject and, overdispersion.

Let $T_j, j=1,2,...,n$ denote the number of PH-depleted sites observed in each of the n subjects. Let us consider the simple case where $T_j, j=1,2,...,n$ are uncorrelated and identically distributed random variables with overdispersion relative to the Binomial model. The mean and variance of $T_j$ are, respectively, $\mu_j=m\pi$ and $\phi(\mu_j)=m\pi(1-\pi)$ with $\phi=\{1+\rho(m-1)\}$, where $\pi=Prob(pH \le 6.5)$ and $\rho$ is the intra-cluster correlation, which is assumed positive. For the parameter of interest $\pi$, the link function is the identity function. If the reader is estimating the log-odds, then the log link would be appropriate.

# Table 3.1: pH data from an Oral Care Study

| Number of mouth sites with pH $\le$ 6.5 | 0 | 1 | 2 | 3 | 4 |
| Number of subjects | 4 | 4 | 6 | 2 | 1 |

Let $t_j$ represent a realization of $T_j$. In this simple example, the solution to the quasi-likelihood score function (3.5) reduces to

```
$$$\sum_{j=1}^{n} \frac{t_j - m\pi}{m\pi(1-\pi)} = 0.$
```

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS.© Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

**