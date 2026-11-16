Then, the LME basis functions can be expressed at any point $x \in P$ as

$$
\phi_i(x) = \frac{1}{Z(x, \lambda^*(x))} \exp \left[ -\beta_i \|x - v_i\|^2 + \lambda^*(x) \cdot (x - v_i) \right]. \quad (13.9)
$$

This expression is not fully explicit because to compute $\lambda^*(x)$ an unconstrained optimization must be solved: the minimization of the strictly convex function $\log Z(x, \lambda)$. It can be observed that the functions can be viewed as the product of a Gaussian function around vertex $v_i$, a normalizing factor ($Z$) so that all functions add up to one, and an exponential factor that depends on the Lagrange multiplier $\lambda^*$ enforcing the linear reproduction condition. Examination of (13.9) shows that, strictly speaking, these basis functions have global support. However, due to the fast decay of the Gaussian function, for all practical purposes they can be considered as compactly supported. Furthermore, the sum in calculation of $Z$ in (13.8) effectively involves only a handful of terms corresponding to vertices in the neighborhood of $x$, which makes the evaluation of the basis functions efficient.

We emphasize the dependence of $\lambda^*$ on position to highlight the fact that at each evaluation point, an unconstrained nonlinear optimization problem must be solved. This problem, however, is only $d$-dimensional, has a unique solution, and can be efficiently solved numerically using Newton's method. See [15, 279, 335] for mathematical and computational details, as well as for the explicit expressions to compute first and second spatial derivatives of the basis functions, and see [177] for the calculation of the gradients of the basis functions on the boundary of $P$.

We end this section by presenting an alternative method to introduce locality into the maximum-entropy framework, which in addition provides a means to define finite strictly compactly supported basis functions. It is very easy to define a set of non-negative smooth basis functions $\psi_i(x)$ relative to $V$, localized around the corresponding vertex, and satisfying only the zeroth-order reproducing condition, $\sum_{i=1}^n \psi_i(x) = 1$. Indeed, consider for instance a scalar, non-negative, and smooth window function $w : [0, +\infty) \to \mathbb{R}$, which decays when the argument is large compared to 1 and satisfies that all odd derivatives up to $k$ at 0 vanish (to guarantee that the even extension of $w$ to $\mathbb{R}$ is $C^k$). Then, for a large enough $\rho$ the functions

```
$$
\psi_i(x) = \frac{w(\|x - v_i\|/\rho)}{\sum_{j=1}^n w(\|x - v_j\|/\rho)}
$$
```

are clearly non-negative, localized around their corresponding vertex $v_i$ with typical width $\rho$, smooth, and add up to one. Furthermore if $w$ is compactly supported, then the functions $\psi_i(x)$ are also compactly supported. Thus, at each point, the numbers $\psi_1(x), \psi_2(x), \dots, \psi_n(x)$ define a discrete probability distribution, which contains information about locality ($\psi_i(x)$ is larger if $x$ is closer to $v_i$) but does not satisfy the first-order reproducing constraint (13.2b). This constraint can be recovered using the concept of *relative entropy*, also called Kullback–Leibler distance, which measures the amount of information required to obtain a discrete probability distribution from a prior distribution. Viewing $\psi_i(x), i = 1, \dots, n$ as a prior