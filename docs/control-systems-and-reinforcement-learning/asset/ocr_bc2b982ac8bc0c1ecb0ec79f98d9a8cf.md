# 5.8 Exercises

$R^{\psi} = \lim_{N\to\infty} \frac{1}{N} \sum_{k=0}^{N-1} \psi_{(k)}^{\psi_{(k)}}.$

Investigate the consequences of rank deficiency, and see if you can construct an example for which this matrix is full rank $p=1$ or $2$.
It is essential to approximate the:

```
$x(k) = \sum_{i=1}^{p} a_i^x \sin(2\pi[phi_i^x + \omega_i^xk]) + \varepsilon(k),
```

$\varepsilon(k)$ converges to zero geometrically, and $\{a_i^x, \phi_i^x, \omega_i^x\}$ are obtained by your lecture notes on signals and systems! You can ignore the vanishing term $\varepsilon(k)$ in your computation of $R^x$.

+   5.3 Obtain an expression for $A(\theta) = -\nabla^{\theta}\Gamma_N(\theta)$ for the batch loss function (5.3b). Obtain conditions on $\{x(0), u'(0)\}$ so that $A$ is Hurwitz, then it will be helpful to represent $-A$ as the sum of $M$ positive semidefinite matrices.

+   5.4 The ODE approximation for $TD(\lambda)$ is $\frac{d\theta}{d\lambda}$, the function approximation architecture is linear (recall 5.48). With $Q^0 = \theta^0\psi$, we have

$A = E_{\}[[-\psi_{(k)}^{\psi_{(k)} + \psi(x(k+1)),\phi(x(k+1))]]].$.
The existence of a steady-state $\zeta$ can be justified by an implementation with restart. In this exercise, consider $\lambda=0$ or $\zeta = \psi(k) = \psi(x(k), u(k))$, and consider the on-policy setting for which we may have

$A = E_{\}[[-\psi_{(k)}^{\psi_{(k)}} + \psi_{(k)}^{\psi_{(k+1)}}]]$.

To simplify the calculations, follow that $E_{\}[ (\psi_{(k)}^{\psi_{(k)}})^2] = I$, and also assume the nondegeneracy condition: $\theta \neq 0$. Show that the matrix $A$ is Hurwitz under these assumptions.
Suggested approach: Let $(\lambda, v)$ denote an eigenvalue-eigenvector pair, with $||v||=1$ (and remember that $\lambda$ and $v$ may be complex). Then find the eigenvector by property,

"\lambda" introduce complex conjugate transport. Consider the next result of our discussion:

```
$A = -I + E_{\}[[\psi_{(k)}^{\psi_{(k+1)}}]]$.$

$\lambda v = A^T v = -v + E_{\}[[(\psi_{(k)}^{\psi_{(k+1)}})^T v^T\ \psi_{(k+1)}}]]$.
```

The right-hand side is $-1 + E_{\}[\psi_{(k)}^{\psi_{(k)}}v^T\psi_{(k)}]$ in the notation introduced in Section 5.4.1. Use the Cauchy-Schwarz inequality to show well the inner product, and that the real part of $A$ is strictly negative.

+   5.5 Formulate $TD(\lambda)$-learning for the discounted-criterion, with a fixed-policy Q-function defined by

```
$Q^{\phi}(x,u) = \sum_{k=0}^{\infty} \gamma^k v(x(k),u(k)), \quad x(0)=x, u(0)=u$ and $u(k)=\phi(x(k))$ for k \geq 1$.
```

The key step is to obtain a new definition for the temporal difference.
Repeat Exercise 5.4 for the on-policy version of your algorithm.