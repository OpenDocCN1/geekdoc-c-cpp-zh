# 5.1 Function Approximation Architectures

With y, $\alpha^* \in \mathbb{R}^N$ column vectors, this gives

> $\alpha^* = (K^	op K + \delta K)^{-1} K^	op y.$

The transpose in (5.18) is not necessarily, since $K = K^	op$ by assumption.

# Mean-Square Bellman Error

We no longer have an explicit solution to (5.16), we $G$ quadratic, but that $h^*$ is of the form (5.17) for some vector $\alpha^*$. Hence $h^*$ is a finite-dimensional optimization problem. Exercises 5.10 and 5.11 provide a roadmap to approximations of this complex nonlinear optimization by a sequence of quadratic optimization problems.

A more successful approach may proceed using a convex loss function $\Gamma: \mathbb{R}^N \to \mathbb{R}_+$, constructed by applying the representations in Section 3.5; more on this approach may be found in Section 5.5.

# 5.1.5 Are We Done Yet?

Let's think about how to answer the question of minimizing the mean-square Bellman error using linear function approximation, which results in the root-finding problem (5.9). That is, $f_N(\theta_N) = 0$, with

> $f_N(\theta_N) = \frac{1}{N} \sum_{k=1}^N D_k(h^0(z_k), h^0(z_{k+1}))\zeta^0(k).$

It may take you time to compute $\theta_N$, you are far from done.

Some experiments you can perform to obtain more confidence that you have a useful solution:

# Is Your Parameterization Redundant?

Consider $Q^0 = \theta^top\psi$, an approximate Q-function. With estimates of the best value of $\theta$, obtain the sample correlation matrix:

> $\hat{R}^v = \frac{1}{N} \sum_{i=1}^N \psi(z_i)\psi(z_i)^\top.$

Look at the eigenvalues of this positive semidefinite matrix – if there is a nontrivial null space, then there may be a problem with your basis or your choice of data.

If $\hat{R}^v = 0$ for some nonzero vector $v$, then $v^top \hat{R}^v = 0$, meaning that

> $0 = v^top \frac{1}{N} \sum_{i=1}^N (v^	op \psi(z_i))^2.$

It follows that $Q^0$, with $\theta = v$, is identically zero over the observed samples. And that your basis is redundant, in the sense that some $\psi_k$ is a linear combination of the others: If $v_k \neq 0$, then

> $\psi_k(z_i) = -\frac{1}{v_k} \sum_{j \neq k} v_j \psi_j(z_i), \quad 1 \le i \le N.$