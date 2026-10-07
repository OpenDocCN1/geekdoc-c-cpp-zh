
## 68 Overdispersion Models in SAS

```
run;
ods html close;
```

### Output 3.5: Results from the Vertebral Fracture Example Using GENMOD

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_80_0.png)

| Criteria For Assessing Goodness Of Fit |
| Criterion | DF | Value | Value/DF |
| Pearson Chi-Square | 51 | 88.2883 | 1.7311 |

| Analysis Of Maximum Likelihood Parameter Estimates |
| Parameter | DF | Estimate | Standard Error | Wald 95% Confidence Limits | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -0.0449 | 0.1632 | -0.3647 | 0.2750 | 0.08 | 0.7833 |
| treat | Active | 1 | -0.9000 | 0.2974 | -1.4829 | -0.3170 | 9.16 | 0.0025 |
| treat | Placebo | 0 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | |
| Scale | 0 | 0.3157 | 0.0000 | 0.3157 | 1.3157 | | |

> The scale parameter was estimated by the square root of Pearson's Chi-Square/DOF.

| Contrast Estimate Results |
| Label | Mean Estimate | Mean | L'Beta Estimate | Standard Error | Alpha | L'Beta | Chi-Square | Pr > ChiSq |
| | | Confidence Limits | | | | Confidence Limits | | |
| Placebo | 0.9561 | 0.6944 | 1.3165 | -0.0449 | 0.1632 | 0.05 | -0.3647 | 0.2750 | 0.08 | 0.7833 |
| Active | 0.3887 | 0.2388 | 0.6329 | -0.9488 | 0.2486 | 0.05 | -1.4322 | -0.4575 | 14.44 | 0.0001 |
| Rate Ratio | 0.4066 | 0.2278 | 0.7283 | -0.0900 | 0.2475 | 0.05 | -1.4829 | -0.3170 | 9.16 | 0.0025 |

More, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS*. Copyright © 2011, SAS Institute, Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

## Chapter 3 Quasi-likelihood Functions 69

The estimated fractures-per-year rates are $e^{-0.0449} = 0.9561$ for the placebo group and
$e^{-0.0449-0.9000} = 0.3887$ for the bisphosphonate group, indicating a highly significant

(P-value = 0.0025) reduction in the number of vertebral fractures in the bisphosphonate group as compared with the placebo. The estimated fractures per-year are of the form

```
$$\left(\sum_{j=1}^{n_i} y_{ij} / \sum_{j=1}^{n_i} z_{ij}\right), i = 1, 2.$
```

The Rate Ratio is

```
$RR = \left(\sum_{j=1}^{n_i} y_{ij} / \sum_{j=1}^{n_i} z_{ij}\right) \cdot \left(\sum_{j=1}^{n_i} y_{2j} / \sum_{j=1}^{n_i} z_{2j}\right)$
```

which in this example turns out to be 0.4066. This result indicates that there is approximately 41% reduction in the estimated fractures-per-year in the bisphosphonate group relative to the placebo group. An approximate 95% confidence interval for the Rate Ratio is (0.2270, 0.7283). This confidence interval was obtained by applying the inverse link function, which is the exponential function to the bounds of the model scale confidence interval ($-1.4829, -0.3170$). The square root of the inflation factor, as estimated by the Pearson’s Chi-square statistic over its degrees of freedom, was 1.3157. All standard errors obtained from the maximum likelihood estimation were inflated by this factor.

### Table 3.6: Estimates, Standard Errors, Chi-squares, and P-values for Poisson Extra Variation Model of Vertebral Fracture Data

| Parameter | Estimate | Standard Error | Chi-square | P-value |
|---| Intercept | -0.0449 | 0.1632 | 0.08 | 0.7833 |
| Bisphosphonate | -0.9000 | 0.2974 | 9.16 | 0.0025 |
| Scale ($\sqrt{\}$) | 1.3157 | | | |

### 3.7 Williams’ Quasi-likelihood Model

Consider the following logistic regression model with overdispersion

```
$E(T) = \mu_i, \text{Var}(T) = \mu_i\pi_i\{1+(1-\pi_i)\theta\},$ and $\log(\frac{\pi_i}{1-\pi_i}) = x_i\beta.$
```

Williams (1982) proposed an iterative weighted least-squares procedure similar to that in equation (2.23) of Chapter 2 in order to estimate $\beta$ and $\theta$ simultaneously. In Williams’ paper the intra-cluster correlation is denoted by $\phi$. To avoid confusion with the scale (dispersion) parameter

## Overdispersion Models in SAS

models for overdispersion. When appropriate, we will denote the intra-cluster correlation by $\rho^2$ to indicate overdispersion.

Williams modified the iterative least-squares procedure in equation (2.23) of Chapter 2 to allow the weights (inflation factors) $w_j^{-1} = [1 + (m_j - 1)\theta]$ to be used in conjunction with the variance function $v_j = m_j\pi_j(1 - \pi_j)$. Note that the variance of $T_j$ is $v_jw_j^{-1}$. For known $\theta$, the Quasi-likelihood estimator of $\beta$ can be solved iteratively

```
$\hat{\beta}_{(s+1)} = \hat{\beta}_{(s)} +(\mathbf{X}'\mathbf{W}\mathbf{X})^{-1}\mathbf{X}'\mathbf{W}(\mathbf{y}-\boldsymbol{\mu}),\quad$ (3.10)
```

where $\mathbf{V} = \text{Diag} [m_1\pi_1(1-\pi_1), m_2\pi_2(1-\pi_2), ..., m_n\pi_n(1-\pi_n)] = (v_1, v_2, ..., v_n)$ and

```
$\mathbf{W} = \text{Diag} [\frac{1}{1+(m_1-1)\theta}, \frac{1}{1+(m_2-1)\theta}, ..., \frac{1}{1+(m_n-1)\theta}] = \text{Diag}(w_1, w_2, ..., w_n).$ The case $\theta=0$ makes $\mathbf{W} = \mathbf{I}$, the identity matrix. Then, the above iterative procedure becomes the one for finding the MLE of $\beta$.
```

When a $w_j$ is associated with the $j$-th subject (cluster), the usual Pearson-square statistic

```
$\chi^2 = \sum_{j=1}^n \frac{w_j(t_j-m_j\hat{\pi}_j)^2}{m_j\hat{\pi}_j(1-\hat{\pi}_j)},\quad$ (3.11)
```

Williams performed Taylor's series expansion on $E(X^2)$ to derive the moment estimator

```
$\hat{\theta} = \frac{\sum_{j=1}^n w_j(1-w_jv_j)}{\sum_{j=1}^n w_j(m_j-1)(1-w_jv_j)},\quad$ (3.12)
```

where $h_j$ is the variance of the linear predictor $\hat{\eta}_j = \mathbf{x}'\boldsymbol{\beta}$.

The algorithm proposed by Williams to estimate $\beta$ and $\theta$ simultaneously is as follows.

- Step 1: Assume $\theta=0$ ($w_j=1$) and obtain $\hat{\beta}$, the MLE of $\beta$ using the algorithm in equation (2.23) of Chapter 2. Evaluate the Pearson's chi-square statistic $X^2$ using equation (3.11).

## Chapter 3 Quasi-likelihood Functions 71

Step 2: Compare the value of X$^2$ with that of a Chi-square distribution with (n–k) degrees of freedom. If the statistic X$^2$ is unacceptably large, conclude that the intra-cluster correlation is greater than zero, ($\theta > 0$) and obtain $\hat{\theta}$ as

```
$$\hat{\theta} = \frac{X^2 - (n-k)}{\sum(m_j-1)(1-v_j^2)}$$
```

Step 3: Using the new weights $w_j = [1+(m_j-1)\hat{\theta}^2]^{-1}$, estimate $\hat{\beta}$ using the iterative procedure in (3.10). Recalculate the Pearson’s Chi-square statistic X^2$ using equation (3.11).

Step 4: If the X$^2$ is close to (n – k), then conclude that $\hat{\theta}$ is satisfactory and stop the procedure, re-estimate $\hat{\theta}$ using equation (3.12), and go back to Step 3.

As in Williams (1982), we revisit Crowder’s (1978) example to illustrate this methodology. Crowder’s example consisted of a 2x2 factorial experiment with two types of seeds (O. aegyptiaca 75 and 73) and two types of root extracts (bean and cucumber). The outcome is “t”, the number of Seeds that germinated out of “m” seeds. The data are reported in Table 3.7.

### Table 3.7: Seed Germination for Two Types of Seeds (O. aegyptiaca 75 and 73) and Two Types of Root Extracts (Bean and Cucumber)

| Type of Seed | Root Extract | $t_j$ | $m_j$ |
|---|---|---|---|
| O. aegyptiaca 75 | Bean | 10 | 39 |
| | | 23 | 62 |
| | | 23 | 81 |
| | | 26 | 51 |
| | | 17 | 39 |
| | Cucumber | 5 | 6 |
| | | 53 | 74 |
| | | 55 | 72 |
| | | 32 | 51 |
| | | 46 | 79 |
| | | 10 | 13 |
| O. aegyptiaca 73 | Bean | 8 | 16 |
| | | 10 | 30 |
| | | 8 | 28 |
| | | 23 | 45 |
| | | 0 | 4 |

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

## Overdispersion Models in SAS

| Cucumber | 3 | 12 |
| | 22 | 41 |
| | 15 | 30 |
| | 32 | 51 |
| | 3 | 7 |

We will use the LOGISTIC procedure since it has the capability of handling Williams’ Quasi-likelihood model. We also fit a model with no overdispersion using the SCALE=NONE option. The programming statements are provided in Program 3.6.

### Program 3.6: Fitting Williams’ (1982) Quasi-likelihood Model to Seed Germination Data of Table 3.5

> Williams (1982) analysis using seed germination data in Crowder (1978)

type_seed = 0 corresponds to O. aegyptiaca 75
type_seed = 1 corresponds to O. aegyptiaca 73
root_extract = 0 corresponds to Beans
root_extract = 1 corresponds to Cucumbers

```
data seeds;
input type_seed root_extract t m;
datalines;
0 0 10 39
0 0 23 62
0 0 23 81
0 0 26 51
0 0 17 39
0 1 53 74
0 1 55 72
0 1 46 79
1 0 10 13
1 0 8 16
1 0 10 30
1 0 8 28
1 1 23 45
1 1 0 4
1 1 3 12
1 1 22 41
1 1 15 30
1 1 32 51
1 1 3 7;
```

```
ods html;
proc logistic data=seeds;
model/m = type_seed root_extract type_seed*root_extract / scale=none;
out output=out-out predicted=pi_hat;
title "Full Model With SCALE=NONE";
```

```
proc logistic data=seeds;
model/m = type_seed root_extract type_seed*root_extract / scale=williams;
out output=out-out predicted=pi_hat;
```

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.
