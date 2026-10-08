for the Taubin fit, see (5.48); here we again use our standard “sample mean” notation $\bar{z} = \frac{1}{n} \sum z_i$, etc.

**Reduction to a generalized eigenvalue problem.** To solve the constrained minimization problem (5.62)–(5.63) one uses a Lagrange multiplier $\boldsymbol{\eta}$ and reduces it to an unconstrained minimization of the function

```
$$\mathscr{G}(\mathbf{A}, \boldsymbol{\eta}) = \mathbf{A}^T \mathbf{M} \mathbf{A} - \boldsymbol{\eta}(\boldsymbol{\eta}^T \mathbf{N} \mathbf{A} - 1).$$
```

Differentiating with respect to $\mathbf{A}$ and $\boldsymbol{\eta}$ gives

```
$$\mathbf{M}\mathbf{A} = \boldsymbol{\eta}\mathbf{N}\mathbf{A} \qquad \qquad \qquad (5.68)$$
```

and

```
$$\mathbf{A}^T \mathbf{N} \mathbf{A} = 1, \qquad \qquad \qquad \qquad (5.69)$$
```

thus $\mathbf{A}$ must be a generalized eigenvector for the matrix pair $(\mathbf{M}, \mathbf{N})$, which also satisfies $\mathbf{A}^T \mathbf{N} \mathbf{A} = 1$. The problem (5.68)–(5.69) may have several solutions. To choose the right one we note that for each solution $(\boldsymbol{\eta}, \mathbf{A})$ we have

```
$$\mathbf{A}^T \mathbf{M} \mathbf{A} = \boldsymbol{\eta}\mathbf{A}^T \mathbf{N} \mathbf{A} = \boldsymbol{\eta}, \qquad \qquad (5.70)$$
```

thus for the purpose of minimizing $\mathbf{A}^T \mathbf{M} \mathbf{A}$ we should choose the solution of (5.68)–(5.69) with the smallest $\boldsymbol{\eta}$. Note that $\boldsymbol{\eta}$ is automatically nonnegative, since $\mathbf{M} = \frac{1}{n}\mathbf{X}^T\mathbf{X}$ is a positive semi-definite matrix.

Since multiplying $\mathbf{A}$ by a scalar does not change the circle it represents, it is common in practical applications to require that $\|\mathbf{A}\|=1$, instead of $\mathbf{A}^T \mathbf{N} \mathbf{A}=1$. Accordingly one needs to replace the rigid constraint (5.69) with a softer one $\mathbf{A}^T \mathbf{N} \mathbf{A}>0$. The latter can be further relaxed as follows.

For generic data sets, $\mathbf{M}$ is positive definite. Thus if $(\boldsymbol{\eta},\mathbf{A})$ is any solution of the generalized eigenvalue problem (5.68), then $\mathbf{A}^T \mathbf{M} \mathbf{A} > 0$. In that case, due to (5.70), we have $\mathbf{A}^T \mathbf{N} \mathbf{A} > 0$ if and only if $\boldsymbol{\eta} > 0$. Thus it is enough to solve the problem (5.68) and choose the smallest positive $\boldsymbol{\eta}$ and the corresponding unit vector $\mathbf{A}$. This rule is almost universally used in practice. However, it needs to be adapted to one special case, which turns out to be quite precarious.

**The singular case.** The matrix $\mathbf{M}$ is singular if and only if the observed points lie on a circle (or a line); in this case the eigenvector $\mathbf{A}_0$ corresponding to $\boldsymbol{\eta} = 0$ satisfies $\mathbf{X}\mathbf{A}_0 = \mathbf{0}$, i.e., it gives the interpolating circle (line), which is obviously the best possible fit. However, it may happen that for some (poorly chosen) matrices $\mathbf{N}$ we have $\mathbf{A}_0^T\mathbf{N}\mathbf{A}_0 < 0$, so that the geometrically perfect solution fails to satisfy the “soft” constraint $\mathbf{A}^T\mathbf{N}\mathbf{A} > 0$, and thus has to be rejected. Such algebraic fits are poorly designed and not worth considering.

For all the constraint matrices $\mathbf{N}$ mentioned so far we have $\mathbf{A}^T \mathbf{N} \mathbf{A} \ge 0$ whenever $\mathbf{A}^T \mathbf{M} \mathbf{A} = 0$. For example, the Kása matrix $\mathbf{K}$, the Taubin matrix $\mathbf{T}$, and the constraint matrices corresponding to the Gander-Golub-Strebel fit and