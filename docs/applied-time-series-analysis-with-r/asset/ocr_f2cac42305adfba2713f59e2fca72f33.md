# Definition 10.6

Let $X_t$ be a causal, stationary multivariate process that satisfies

```
$X_t = \alpha + \Phi_1 X_{t-1} - \dots - \Phi_p X_{t-p} + a_t, \quad (10.15)$
```

where

+   1. $X_t = (X_{t1}, \dots, X_{tm})'$ is an $m \times 1$ vector
2. $\Phi_k$ is a real-valued $m \times m$ matrix for each $k = 1, \dots, p$
3. $a_t$, is multivariate white noise with covariance matrix $E[a_t, a_t'] = \Gamma_a$;n4. $\alpha = (\Phi_1 - \dots - \Phi_p)\mu$, where $\mu = E(X_t)$

Then $X_t$ is a VAR($p$) process, that is, a multivariate AR process of order $p$.

Note that Equation 10.1 can be written in multivariate operator notation $\Phi(B)(X_t - \mu) = a_t$,

```
$\Phi(B) = \mathbf{I} - \Phi_1 B - \dots - \Phi_p B^p, \quad (10.16)$
```

and $B^k X_t = X_{t-k}$. Theorem 10.1 gives stationarity conditions for VAR($p$) models that are analogous to those in Theorem 3.2 for univariate AR($p$) models.

# Theorem 10.1

A multivariate process $X_t$, satisfying the difference equation in Equation 10.15 is a stationary and causal VAR($p$) process if only if the roots of the determinantal equation,

```
$|\Phi(z)| = |\mathbf{I} - \Phi_1 z - \dots - \Phi_p z^p| = 0$,
```

outside the unit circle.

Proof: See Brockwell and Davis (1991) and Reinsel (1997).

Note that a VAR($p$) model $\Phi(B)(X_t - \mu) = a_t$, satisfying Theorem 10.1 can be written in the multivariate general linear process form

```
$X_t - \mu = \Psi(B)a_t;\n= \sum_{j=0}^infty \Psi_j a_{t-j}, \quad (10.17)$
```

where $\Psi(B) = \Phi^{-1}(B)$.\nThe multivariate Yule–Walker equations are given by

```
$\Gamma(k) = \Gamma(k-1)\Phi_k' + \dots + \Gamma(k-p)\Phi_p, \ k=1, \dots, p, \quad (10.18)$
```