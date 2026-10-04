

# 预测

237

和

$E_{t_0}[a_{t_0+k}] = 0, \quad k > 0$
$= a_{t_0+k}, \quad k \leq 0. \quad (6.20)$

If $E[X_t] = \mu \neq 0$, then Equation 6.19 holds for $X_t - \mu$, and we have the following for $\ell \geq 1$.

## 6.5.1 最佳预测方程的差分方程形式

$\hat{X}_{t_0}(\ell) = \sum_{j=1}^P \phi_j \hat{X}_{t_0}(\ell - j) - \sum_{j=1}^q \theta_j E_{t_0}[a_{t_0+\ell-j}] + \left(1 - \sum_{j=1}^P \phi_j\right) \mu. \quad (6.21)$

Before proceeding with the implementation of this result, we first note that

$X_{t_0+\ell} = \sum_{j=1}^P \phi_j X_{t_0+\ell} + a_{t_0+\ell} - \sum_{j=1}^q \theta_j a_{t_0+\ell-j} + \left(1 - \sum_{j=1}^P \phi_j\right) \mu. \quad (6.22)$

Thus, if data are available up to time $t_0$, we obtain $\hat{X}_{t_0}(\ell)$ in Equation 6.21 by the heurically sensible procedure of replacing each term in Equation 6.22 by either

- 1. Its known value as time $t_0$
- 2. Its forecast, or expected value, given data to time $t_0$

Although Equation 6.21 has an appeal over Equation 6.9 from a practical standpoint, there are still difficulties with its implementation. Specifically, in a practical situation

- 1. $X_1, X_2, \dots, X_{t_0}$ have been observed
- 2. Model parameters have been estimated
- 3. The $a_i$ are unknown

Consequently, Equation 6.21 cannot be immediately applied, and in practice, we use Equation 6.21 with the following modifications:

- 1. The estimated model is assumed to be the true model and $\mu$ is estimated by $\hat{X}$.
- 2. The $a_i$ are estimated from the data.

The comment in (a) relates to the fact mentioned at the beginning of this chapter, that our forecasting formulas are based on a known model. The estimation of $a_t$, proceeding by noting that for an ARMA(p,q) model,

$X_t = \sum_{j=1}^{p} \phi_j X_{t-j} + a_t - \sum_{j=1}^{q} \theta_j a_{t-j} + \left(1 - \sum_{j=1}^{p} \phi_j\right) \mu,$

which can be rewritten as

$a_t = X_t - \sum_{j=1}^{p} \phi_j X_{t-j} + \sum_{j=1}^{q} \theta_j a_{t-j} - \left(1 - \sum_{j=1}^{p} \phi_j\right) \mu.$

So, for $t \le t_0, E_0[a_t] = (a_t)$ is estimated by

$$\hat{a}_t = \begin{cases} 0, t \le p \ X_t - \sum_{j=1}^{p} \phi_j X_{t-j} + \sum_{j=1}^{q} \theta_j a_{t-j} - \left(1 - \sum_{j=1}^{q} \phi_j\right) \hat{X}_t, t = \max(p+1,q+1), \dots, t_0. \end{cases}$$
(6.23)

Moreover, from Equation 6.20, since $E_0[a_t] = 0$ for $t > t_0$, we define

$$\hat{a}_t = 0, t > t_0.$$

This leads to the following.

## 6.5.2 从 ARMA(p,q) 模型计算预测的基本差分方程形式

$$\hat{X}_{t_0}(\ell) = \sum_{j=1}^{p} \phi_j \hat{X}_{t_0}(\ell-j) - \sum_{j=1}^{q} \theta_j \hat{a}_{t_0+\ell-j} + \left(1 - \sum_{j=1}^{p} \phi_j\right) \hat{X}.$$
(6.24)

Notice that the $\hat{a}_i$'s enter the calculation of the forecasts only when there are moving average terms in the model. The use of Equation 6.24 for calculating forecasts is illustrated in the two examples. It should be noted that an improved method of calculating the $\hat{a}_i$'s, based on backcasting, is discussed in Section 74.

# 预测

## 示例 6.1：来自 AR(1) 模型的预测

Consider the AR(1) model

$$(1 - 0.8B)(X_t - \mu) = a_t \quad (6.25)$$

We observe $X_1, X_2, \dots, X_{t_0}$, and our goal is to estimate or forecast $X_{t_0+\ell}$. From Equation 6.24, we obtain

$$\hat{X}_{t_0}(\ell) = 0.8\hat{X}_{t_0}(\ell - 1) + 0.2\bar{X}$$

Thus, the forecasts are obtained by the following simple recursion:

$$\hat{X}_{t_0}(1) = 0.8\hat{X}_{t_0}(0) + 0.2\bar{X}$$
$= 0.8X_{t_0} + 0.2\bar{X}$
$\hat{X}_{t_0}(2) = 0.8\hat{X}_{t_0}(1) + 0.2\bar{X}$
:$
$\hat{X}_{t_0}(\ell) = 0.8\hat{X}_{t_0}(\ell - 1) + 0.2\bar{X}$

Figure 6.1 shows the forecasts $\hat{X}_{80}(\ell)$ for $\ell=1, \dots, 20$, based on a realization of length 80 from model in Equation 6.25 with $\mu=25$. For this realization, $\bar{X}=24.17$. The general form of the forecasts for large $\ell$ is discussed in Section 6.6.

**Using R:** This realization is found in *tswge* data set *fig6.inf*. Note that in this chapter, the "nf" indicates "no forecasts" to make clear that the data set, in this case, only includes the 80 data values in Figure 6.1 and not the forecasts that are shown there.

![](img/41dcbfb9af56fa48895afde322197b0b_255_0.png)

**FIGURE 6.1**
Forecasts using the AR(1) model.

# 应用时间序列分析与 R

## 示例 6.2：来自 ARMA(2,1) 模型的预测

Consider the ARMA(2,1) model given by

$$(1 - 1.2B + 0.6B^2)(X_t - 50) = (1 - 0.5B)\alpha_t.$$

Table 6.1 displays $X_t$, $t=1, 2, \dots, 25$, generated from this model with $\sigma_\alpha^2 = 1$. This data set is also available in *tsweg* at **fig6.2.nnf**. According to Equation 6.24, forecasts from $t_0$ are given by

$$\hat{X}_{25}(\ell) = \phi_1\hat{X}_{25}(\ell-1) + \phi_2\hat{X}_{25}(\ell-2) - \sum_{j=\ell}^{25} \hat{a}_{25,\ell-j} + (1-\phi_1-\phi_2)\hat{X}_j$$

$$=1.2\hat{X}_{25}(\ell-1) - 0.6\hat{X}_{25}(\ell-2) - 0.5\hat{a}_{25} + 0.4\hat{X}_ell, \ \text{for } \ell=1$$
$=1.2\hat{X}_{25}(\ell-1) - 0.6\hat{X}_{25}(\ell-2) + 0.4\hat{X}_ell, \ \text{for } \ell > 1.$

Thus, it is that only $\hat{a}_t$ are needed in order to obtain the forecasts. The $\hat{a}_t$'s are obtained recursively using Equation 6.23, and to calculate $\hat{a}_{25}$, we must compute $\hat{a}_t=1, \dots, 24$. These estimates are also shown in Table 6.1. Note that $\hat{a}_1$ and $\hat{a}_2$ are both zero, by Equation 6.23 $\hat{a}_t=0$ for $t \le p$. Using the fact that $X_{50}=50.04$ for the realization in Table 6.1, it follows that

$$\hat{a}_3 = X_3 - 1.2X_2 + 0.6X_1 + 0.5\hat{a}_2 - 50.04(0.4)$$
$=- -1.72,$

and the calculation of remaining $\hat{a}_t$ proceeds in a similar manner. The effect of setting $\hat{a}_1$ and $\hat{a}_2$ equal to zero is minimal, especially in cases where $t_0$ is larger than $p$. This can be seen by examining the expression for $X_t(\ell)$ in Equation 6.9 in terms of the $\psi$-weights

# TABLE 6.1

Realization of Length 25 and Accumulated Estimates of $a_t$ from $(1-1.2B+0.6B^2)(X_t-50) = (1-0.5B)a_t$,

| T | X_t | $\hat{a}_t$ | T | X_t | $\hat{a}_t$ |
|---|---|---|---|---|---|
| 1 | 49.99 | 0.00 | 14 | 50.00 | -0.42 |
| 2 | 51.14 | 0.00 | 15 | 49.70 | -0.61 |
| 3 | 49.97 | -1.72 | 16 | 51.73 | 1.77 |
| 4 | 49.74 | -0.42 | 17 | 51.88 | 0.49 |
| 5 | 50.35 | 0.42 | 18 | 50.88 | -0.11 |
| 6 | 49.57 | -0.81 | 19 | 48.78 | -1.22 |
| 7 | 50.39 | 0.70 | 20 | 49.14 | 0.51 |
| 8 | 51.04 | 0.65 | 21 | 48.10 | -1.36 |
| 9 | 49.93 | -0.78 | 22 | 49.52 | 0.59 |
| 10 | 49.78 | -0.08 | 23 | 50.06 | -0.23 |
| 11 | 48.37 | -1.38 | 24 | 50.66 | 0.17 |
| 12 | 48.85 | -0.03 | 25 | 52.05 | 1.36 |
| 13 | 49.85 | 0.22 | | | |

# 预测

and recalling that $\psi_j \to 0$ as $j \to \infty$ for a stationary model. We will return to the topic of calculating residuals in Section 7.4.
Finally, using Equation 6.27, forecasts are calculated as

$\tilde{X}_{25}(1) = 1.2\tilde{X}_{25}(0) - 0.6\tilde{X}_{25}(-1) - 0.5\tilde{a}_{25} + 0.4\bar{X}$
$= 1.2\tilde{X}_{25} - 0.6\tilde{X}_{24} - 0.5\tilde{a}_{25} + 0.4\bar{X}$
$= 1.2(52.05) - 0.6(50.66) - 0.5(1.36) + 0.4(50.04)$
$= 51.40$,
$\tilde{X}_{25}(2) = 1.2\tilde{X}_{25}(1) - 0.6\tilde{X}_{25}(0) + 0.4\bar{X}$
$= 1.2(51.40) - 0.6(52.05) - 0.4(50.04)$
$= 50.46$,
:

The forecasts $\hat{X}_{25}(\ell)$, $\ell = 1, \dots, 4$ are given in Table 6.2 and $\hat{X}_{25}(\ell)$, $\ell = 1, \dots, 20$ are shown in Figure 6.2.

**Using R:** Forecasts for a given stationary ARMA models can be found using the twge function `fore.arma.wge` and specifying the series, the ARMA model parameters, the number of steps ahead to forecast, and other plotting options. See Appendix 6B.

# TABLE 6.2
Forecasts from $l_0 = 25$ for the Realization in Table 6.1

| $\ell$ | $\hat{X}_{25}(\ell)$ |
|---|---|
| 1 | 51.40 |
| 2 | 50.46 |
| 3 | 49.73 |
| 4 | 49.42 |

![](img/41dcbfb9af56fa48895afde322197b0b_257_0.png)

**FIGURE 6.2**
Forecasts using the ARMA(2,1) model $(1 - 1.2B + 0.6B^2)(X - 50) = (1 - 0.5B)a_t$.

