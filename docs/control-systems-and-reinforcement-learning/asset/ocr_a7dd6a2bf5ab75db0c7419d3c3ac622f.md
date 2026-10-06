# 8.7 Some Theory

The scaled error is denoted

```
$Z_n \triangleq \frac{1}{\sqrt{\alpha_n}}\hat{	heta}_n, \quad \text{and,} \quad \Sigma_n^{Z_n} \triangleq \mathbb{E}[Z_n Z_n^\top] = \frac{1}{\alpha_n}\mathbb{E}[\hat{	heta}_n\hat{	heta}_n^\top]. \quad (8.68)$
```

**Proposition 8.10** Suppose that $\{\Delta_n\}$ satisfies (SA2), and that the covariance is independent of $n$. Then the following approximations hold:

+   (i) With $\alpha_n = 1/(n+n_0)$,

```
$\Sigma_{n+1}^Z = \Sigma_n^Z + \frac{1}{n+n_0}\{(A + I + \mathcal{E}_n)\Sigma_n^Z + \Sigma_n^Z(A + I + \mathcal{E}_n)^\top + \Sigma_{\Delta}\}, \quad (8.69a)$
```

with $|\E_n|| = O(1/n)$. If in addition the matrix $A+\frac{1}{2}I$ is Hurwitz, then $\Sigma_n^Z$ converges to $\Sigma_0$, and this limit is the solution to the Lyapunov equation (8.28a).

+   (ii) With $\alpha_n = 1/(n+n_0)^\rho$, using $\frac{1}{2}<rho < 1$,

```
$\Sigma_{n+1}^Z = \Sigma_n^Z + \frac{1}{n+n_0}\{(A + I)\Sigma_n^Z + \Sigma_n^Z(A + I)^\top + \Sigma_{\Delta}\}, \quad (8.69b)$
```

with $|\Delta_n|| = O(1/n)$. If in addition the matrix $A$ is Hurwitz, then $\Sigma_n^Z$ converges to $\Sigma_0$, and this limit is the solution to the Lyapunov equation (8.28b).

Proof. In both parts, we simplify the calculations by setting $n_0 = 0$. This is justified if $\rho \in (\frac{1}{2},1]$ and $n_0 > 0$, we have the following for any $n \geq 1$:

```
$\frac{1}{(n+n_0)^\rho} = \frac{1}{n^\rho}} + O(\frac{1}{n^{1+\rho}}).
```

+   (i) The approximation (8.69a) begins with the Taylor series approximation

```
$\sqrt{n+1} = \sqrt{n} + \frac{1}{2\sqrt{n}} + O(\frac{1}{n^{3/2}}).
```

Multiplying both sides of the recursion (8.67) results in a result for $\mathbf{Z}$:

```
$Z_{n+1} = Z_n + \frac{1}{n+1}\{(A + I + \mathcal{\varepsilon}_n)Z_n + \sqrt{n}\Delta_{n+1}\}, \quad (8.70)$
```

with $\varepsilon_n = O(n^{-1})$. Taking products on both sides of the recursion, and then taking expectations, we obtain the recursion of (8.69a) after simplifications. It is in this step that we use the fact that $\mathbf{\Delta}$ is a martingale difference sequence, in particular,

```
$\mathbb{E}[Z_n\Delta_{n+1}^\top] = \mathbb{E}[\Delta_{n+1}Z_n^top] = 0$.
```

The recursion (8.69a) can be viewed as a linear stochastic approximation algorithm of the form (8.53b), subject to multiplicative noise that is $O(1/n)$. Convergence follows under the Hurwitz assumption on $A+\frac{1}{2}I$.

The proof of (ii) is identical, following the Taylor series approximation

```
$(n+1)^\rho = n^\rho + O(n^{-1})n^\rho$.
```