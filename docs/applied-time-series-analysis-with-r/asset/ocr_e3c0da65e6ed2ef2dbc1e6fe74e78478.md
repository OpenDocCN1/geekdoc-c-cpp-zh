# Long-Memory Processes

# 477

# TABLE 11.1

Approximating $\gamma_0$ by Truncating in Equation 11.24
When $u=1$ and $\sigma_u^*=1$

| $\lambda(d/2)$ | Exact | Sum to 200,000 | Sum to 10 Million |
|---|---|---|--|
| 0.05 | 1.0195 | 1.0195 | 1.0195 |
| 0.125 | 1.1803 | 1.1800 | 1.1803 |
| 0.24 | 8.4061 | 3.9004 | 4.5527 |

One technique for calculating the autocovariances is to truncate the series in Equation 11.24 after a sufficient number of terms. Table 11.1 (given by Ford, 1991) illustrates that, depending on the parameters, the terms in this series may not damp quickly enough to make truncation feasible.

The table considers the problem of using Equation 11.24 to calculate $\gamma_u$ for the case $u=1$. In this case Theorem 11.1(4) and the fact that $d=2\lambda$, the infinite series in Equation 11.24 is known in closed form to be $\gamma_0^*=\Gamma(-4\lambda+1)/\Gamma(-2\lambda+1)^2$. Table 11.1 compares values of the infinite sum in Equation 11.24 to the results of truncating the sum after 200 million terms and 10 million terms. In the table it sees that for $\lambda=0.05$ and $\lambda=0.125$ the two truncated approximate the infinite sum quite well, in the near-stationary case $\lambda=0.24$, the convergence is extremely slow and a sum to 10 million is a very poor approximation! Chung (1996a) expressed $\gamma_u$ for a (1-factor) Gegenbauer process as a recursion using Legendre functions. Using Equations 11.28 and 11.19, an expression for the autocovariance of a Gegenbauer process is given by the inverse Fourier transform of the spectrum,

> $$\gamma_k = \int_{-0.5}^{0.5} e^{2\pi ikf} P(f)df. \quad (11.25)$

In the Gegenbauer setting, Ford (1991) examined the use of Levin and Sidi’s (1981) $d$-transform for increasing the rate of convergence of the sum in Equation 11.24 and compared the resulting approximations with those obtained by numerically integrating Equation 11.25. As noted, $P_x(f)$ is unbounded for $f_c = (\cos^{-1}(u))/2\lambda$. Ford (1991) concluded that careful numerical integration using Equation 11.25 is the preferred method. Based on these findings, we approximate the autocovariances of $k$-factor Gegenbauer and $k$-factor GARMA models by numerically integrating the integral in Equation 11.25. It should be noted that both methods produce approximate autocorrelations, and for some parameter configurations these can be relatively poor.