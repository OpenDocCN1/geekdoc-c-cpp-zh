# Stationary Time Series

and the result follows. Note that in the case of a discrete time series defined on $t=0, \pm1, \pm2, \dots$, then Equation 1.1 is equivalent to the matrix

```
$$\Gamma_k = \begin{pmatrix} \rho_0 & \rho_1 & & & \rho_k \ \rho_1 & \rho_0 & & & \rho_{k-1} \ & & \vdots & & \vdots \ & & & \vdots & \ \rho_k & & \rho_{k-1} & & \rho_k \end{pmatrix}$$ $(1.2)$
```

being semidefinite for each $k$.
The autocorrelation function satisfies the following analogous properties:

+   a. $ho(0)=1$
b. $|\rho(h)|\le 1$ for all $h$
c. $ho(h)=\rho(-h)$
d. The function $\rho(h)$ is positive semidefinite, and for discrete time series defined on $t=0, \pm1, \pm2, \dots$, the matrix

```
$$\rho_k = \begin{pmatrix} & \rho_1 & & & \rho_k \ & 1 & & & \rho_{k-1} \ & & \vdots & & \ & & & & \vdots \ & & \rho_{k-1} & & 1 \end{pmatrix}$ $(1.3)$
```

is semidefinite for each $k$.

Theorem 1.1 gives conditions that guarantee the stronger conclusion that $\Gamma_k$ and equivalently $\rho_k$ are positive definite for each $k$. The proof of this result can be found in Blackwell and Davis (1991), Proposition 5.1.1.

# Theorem 1.1

If $\gamma_0 > 0$ and $\gamma_j=0$, then $\Gamma_k$ and $\rho_k$ are positive definite for each integer $k>0$.

It is important to understand the extent to which a plot of the autocorrelations for a given model describes the behavior in time series realizations from that model. While Figure 1.3, we show realizations from four stationary time series while Figure 1.4 shows the corresponding true autocorrelations for lags 0–45. Realization 1 in Figure 1.3a displays a wandering or piecewise trending behavior. That is typical for $x_t$ and $x_{t+1}$ to be relatively close to each other; that is, the value of $x_{t+1}$ is usually not very far from the value of $X_t$