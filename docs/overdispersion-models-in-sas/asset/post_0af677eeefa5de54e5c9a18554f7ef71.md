
## 22 Overdispersion Models in SAS

## Plot 2.1: Diagnostic Plots for Gains in Weight Example

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_34_0.png)

## 2.4 Generalized Linear Models (GLM)

Generalized Linear Models (GLM) is an extension of the linear regression model to accommodate non-normal response variables which are possibly even discrete. GLM formulation captures the essential commonality in the computation of MLE when responses are distributed according to a member of the exponential family of distributions, and the mean of the response variable is related to an unknown linear combination of the predictor variables via a known nonlinear function. Thus, GLM provides a unified approach to a large class of commonly used models such as linear regression, logistic and Poisson regression models, etc. In order to understand GLMs, three fundamental concepts are needed: the random component (response variable), the systematic component (predictor variables), and the link function.

$Y_j, j=1,2,...,n$, represent $n$ independent random variables belonging to a specific distribution in the exponential family. We have $E(Y_j)=\mu_j$ and since the $Y_j$ belong to the exponential family.

$Var(Y_j)=\phi v(\mu_j)$.

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS.. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

In the framework of GLM, the mean $\mu_j$, $j=1,2,...,n$, depends on $k$-dimensional row vector of known covariates $\mathbf{x}_j$ and a $k$-dimensional column vector of unknown parameters $\mathbf{\beta}$, through a twice differentiable smooth function $g(\cdot)$ so that

```
$g(\mu_j) = \mathbf{x}_j\mathbf{\beta} = \sum_{i=1}^k x_{ji}\beta_i. (2.10)$
```

The function $g(\cdot)$ is called a **link function**, and $\mathbf{x\beta}$ is called the **linear predictor**. Recall that the link function was previously defined in Section 1.6 of Chapter 6. The linear predictor is usually denoted as $\eta_j = \mathbf{x}_j\mathbf{\beta}$. In the case of classical regression models discussed in Section 2.2,
$\mu_j = \mathbf{x}_j\mathbf{\beta} = \sum_{i=1}^k x_{ji}\beta_i$, so the link function is the identity function. Note that $\mu_j = g^{-1}(\mathbf{x}_j\mathbf{\beta})$ whereas $g^{-1}(\cdot)$ is the mean function. In Table 1.2 of Chapter 1 we provided the mean and canonical link functions for the Bernoulli and Poisson distributions. From now on, $g(\cdot)$ will be used to denote any link function, including canonical link functions. Thus, the main characteristics of a GLM are:

- 1. **The random component**: the components of $Y_j$, $j=1,2,...,n$ are independent and distributed according to one of the distributions in the exponential family.

- 2. **The systematic component**: the linear predictors $\eta_j = \mathbf{x}_j\mathbf{\beta}$, $j=1,2,...,n$, are such that $\mathbf{x}_j$ is a vector of known covariates, and $\mathbf{\beta}$ is the unknown vector of parameters.

- 3. **The link function**: the link between the random and systematic parts that is $g(\mu_j) = \eta_j$, $j=1,2,...,n$.

Table 2.2 gives these three key components of GLM for various members of the family. In all these examples the random component is $Y_j$ and the linear predictor is $\eta_j = \mathbf{x}_j\mathbf{\beta}$. Note that distributions admit more than one link function, and the choice is not limited to canonical links only. This is not an exhaustive list. A complete list of available options of link functions may be found in the GENMOD GLIMMIX documentation.

## Table 2.2: Some Link and Mean Functions for Selected Distributions

| Distribution of $Y_j$ | Link Function | Mean Function |
|---|---|---|
| Normal($\mu_j, \sigma^2$) | Identity: $\mu_j = \mathbf{x}\beta$ | Identity: $\mu_j = \mathbf{x}\beta$ |
| Normal($\mu_j, \sigma^2$) | Logarithm: $\ln(\mu_j) = \mathbf{x}\beta$ | Exponential: $\mu_j = e^{\mathbf{x}\beta}$ |
| Bernoulli($\pi_j$) | Logit: $\ln\frac{\pi_j}{1-\pi_j} = \mathbf{x}\beta$ | Logistic: $\pi_j = \frac{e^{\mathbf{x}\beta}}{1+e^{\mathbf{x}\beta}}$ |
| Bernoulli($\pi_j$) | Probit: $\Phi^{-1}(\pi_j) = \mathbf{x}\beta$ | Normal: $\pi_j = \Phi(\mathbf{x}\beta)$ |
| Poisson($\lambda_j$) | Logarithm: $\ln(\lambda_j) = \mathbf{x}\beta$ | Exponential: $\lambda_j = e^{\mathbf{x}\beta}$ |
| Poisson($\lambda_j$) | Identity: $\lambda_j = \mathbf{x}\beta$ | Identity: $\lambda_j = \mathbf{x}\beta$ |

Here, $\Phi(\cdot)$, represents the cumulative probability function of a standard Normal distribution,

given by, $\Phi(x) = \frac{1}{\sqrt{2\pi}} \int \exp\left(-\frac{Z^2}{2}\right) dZ$.

## 2.5 The Deviance and the Pearson Chi-Square Statistic

In linear regression models, goodness-of-fit is usually measured by the sum of squared residuals. Nested models are obtained by taking a subset of the predictor variables from a larger (full) model. Reduced models can be compared to full models using the sum of squared residuals, and F-tests can be constructed using the sum of squared residuals from the full and reduced models. In GLM, the sum of squared residuals may not always be meaningful, especially when the response variables are discrete. Therefore, alternative ways of examining the goodness-of-fit are desired. By computing the statistic known as Deviance, which was originally proposed by Nelder and Woodburn (1971). They noted that for any set of two extreme models are conceivable: namely, the minimal model and the saturated model. The minimal model contains one single parameter (the mean), whereas the saturated model has a parameter for each observation. The minimal model is too simple. On the other hand, the saturated model is uninformative in the sense that it provides a perfect fit estimating the maximum allowable number of parameters. Although saturated models do not summarize the data, they are useful in practice. The most desirable model is likely to be between the minimal and saturated models. The deviance is in essence measure of the distance between the model and the saturated model, measured in terms of the log-likelihood function. McCullagh and Nelder (1989) point out that differences in deviances for nested models can be approximated by Chi-square distributions with degrees of freedom by the parameters in which two models are compared.

For a independent binomial random variables $T_j, j=1,2,...,n, T \sim \text{Binomial}(\pi_j, m_j)$, consider $t_j$ as a Binomial of $T_j$. Note the slight departure from earlier notation by denoting the response variable with the letter $T$ that is Binomial. We will denote Poisson and

Bernoulli outcomes with the letter Y. Then, for the Binomial distribution it can be shown the deviance is

```
$D = 2\sum_{j=1}^{n} t_j \log\left(\frac{t_j}{m_j\hat{\pi}_j}\right) + (m_j - t_j) \log\left(\frac{m_j - t_j}{m_j-\hat{\pi}_j}\right) \quad (2.11)$
```

where $\hat{\pi}_j = g^{-1}(x_j\hat{\beta}_j)$. When $Y_j \sim \text{Poisson}(\lambda_j), j=1,2,...,n$, it can be shown the deviance is

```
$D = 2\sum_{j=1}^{n} y_j \log\left(\frac{y_j}{\hat{\lambda}_j}\right) - (y-\hat{\lambda}_j) \quad (2.12)$
```

where $\hat{\lambda}_j = g^{-1}(x_j\hat{\beta}_j)$.

Nelder and Wedderburn went further and proposed a generalized analysis of variance for sequential fitting of models using differences of deviances analogous to the classical analysis of variance based on differences of squares. This analysis is possible because the additive property of the deviance for nested (sequential) models. The GENMOD procedure can provide generalized analysis of variance.

Another important measure of the goodness-of-fit of a GLM is the Pearson $X^2$ statistic. In the context of GLMs, it is defined as

```
$X^2 = \sum_{j=1}^{n} \frac{(y_j-\hat{\mu}_j)^2}{v(\hat{\mu}_j)}$
```

where $v(\hat{\mu}_j)$ is the estimated variance function for the distribution under consideration. For the Binomial distribution, the Pearson $X^2$ statistic is

```
$X^2 = \sum_{j=1}^{n} \frac{(t_j-m_j\hat{\pi}_j)^2}{m_j\hat{\pi}_j(1-\hat{\pi}_j)} \quad (2.13)$
```

and for the Poisson distribution

```
$X^2 = \sum_{j=1}^{n} \frac{(y_j-\hat{\lambda}_j)^2}{\hat{\lambda}_j} \quad (2.14)$
```
