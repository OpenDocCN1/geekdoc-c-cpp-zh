Using R: This realization is found in tswge data set fig6.1nf. Note that in this chapter, the “nf” indicates “no forecasts” to make it clear that the data set, in this case, only includes the 80 data values in Figure 6.1 and not the forecasts that are shown there.

![](bbox=[0.25, 0.24, 0.7, 0.44])

# FIGURE 6.1

Forecasts using the AR(1) model.

# EXAMPLE 6.2: FORECASTS FROM AN ARMA(2,1) MODEL

Consider the ARMA(2,1) model given by

$(1 - 1.2B + 0.6B^2)(X_t - 50) = (1 - 0.5B)a_t.\quad (6.26)$

Table 6.1 displays a realization $X_t$, $t = 1, 2, ..., 25$ generated from this model with $\sigma_a^2 = 1$. This data set is also available in tswge as fig6.2nf. According to Equation 6.24, forecasts from $t_0 = 25$ are given by

$\hat X_{25}(\ell) = \phi_1 \hat X_{25}(\ell -1) + \phi_2 \hat X_{25}(\ell -2) - \sum_{j=1}^q \theta_j \hat a_{25+\ell -j} + (1 - \phi_1 - \phi_2)\bar X,\quad (6.27)$
$= 1.2 \hat X_{25}(\ell -1) - 0.6 \hat X_{25}(\ell -2) - 0.5 \hat a_{25} + 0.4 \bar X,\ \text{for }\ell =1$
$= 1.2 \hat X_{25}(\ell -1) - 0.6 \hat X_{25}(\ell -2) + 0.4 \bar X,\ \text{for }\ell >1.$

Thus, it is seen that only $\hat a_{25}$ is needed in order to obtain the forecasts. The $\hat a_t$'s are obtained recursively using Equation 6.23, and in order to calculate $\hat a_{25}$, we must first compute $\hat a_t$, $t = 1, ..., 24$. These estimates are also shown in Table 6.1. Notice that $\hat a_1$ and $\hat a_2$ are both zero since, by Equation 6.23 $\hat a_t = 0$ for $t \le p$. Using the fact that