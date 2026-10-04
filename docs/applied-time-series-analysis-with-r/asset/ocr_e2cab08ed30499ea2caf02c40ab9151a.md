# ARMA Time Series Models

Since $\sum_{p=0}^{\infty} |\alpha_p^{(1)}| < \infty$ and $\sum_{p=0}^{\infty} |\alpha_p^{(2)}| < \infty$ if the roots of the characteristic equation are all outside the unit circle, then $\sum_{t=0}^{\infty} \psi_t(p)$ converges absolutely. It follows that the right side of Equation 3.26 converges in mean square, and X, is a causal stationary solution of Equation 3.25.
Sufficiency) See Theorem 3.1.1 Brockwell and Davis (1991).

**Schur's lemma:** A necessary and sufficient condition that the roots of the algebraic equation

```
$$\phi(z) = 1 - \phi_1 z - \phi_2 z^2 - \dots - \phi_p z^p = 0,$$
```

all lie outside the unit circle is the quadratic form

```
$$\left[ \sum_{k=0}^{p-1} \phi_k Y_{j+k} \right]^2 - \left[ \sum_{k=0}^{p-1} \phi_k Y_{j+1+k} \right]^2 = (3A.2)$
```

where $\phi_0 = -1$ is positive definite. By expanding Equation 3A.2, one can see that the symmetric matrix, C, associated with Equation 3A.2 is given by

```
$C = (c_{jk}),$$
```

where

```
$c_{jk} = \sum_{h=1}^{\min(j,k)} (\phi_{j-h}\phi_{k-h} - \phi_{p+h-j}\phi_{p+h-k}).$$
```

Proof: See Henrici (1974).

# **Proof of Theorem 3.3**

(Sufficiency) The fact that all roots of $	heta(z) = 0$ lie outside the unit circle implies that $	heta(z) \neq 0$ for $|z| \le 1$, and hence, there exists an $\varepsilon > 0$ such that $	heta^{-1}(z)$ has a convergent power series expansion for $|z| < 1 + \varepsilon$. So, from Equation 3.82,

```
$|\theta^{-1}(z)| = \sum_{j=0}^{\infty} \pi_j z^j < \infty, \quad (3A.3)$
```