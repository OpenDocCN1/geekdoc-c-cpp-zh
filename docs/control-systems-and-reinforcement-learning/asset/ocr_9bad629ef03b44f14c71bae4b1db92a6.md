# Temporal Difference Methods

Soon after stability was established, Szepvesvari investigated the rate of convergence. Using a coupling argument introduced in [227], the following upper bound is obtained in [346] for Watkins's algorithm with the state-dependent step size $\alpha_t^n:

```
|H^n(x,u) - Q^*(x,u)| \leq B \frac{1}{n^{(1-\gamma)r}}, \quad n \geq 1, x \in X, u \in U,
```

with $B$ and $r = \varrho/\varrho$ (the ratio of the minimum and maximum of $\Omega$). The bound is only valid for sufficient $large$ (it is not realistic to have $(1-\gamma)r > 1/2$). While only one upper bound, stability performs poorly when the discount factor is close to unity. See [18, 124] for extensions and refinements.

It was established in [112, 113] that the convergence of the rate of MSE $E[|\theta^t - \theta^0||^2]$ of Watkins's Q-learning can be slower than $O(1/n^{(1-\gamma)r})$, if the discount factor $\gamma > 1/2$. It has also shown that the optimal convergence rate (8.8) is achieved by using a step-size of the form $\alpha_t = q/n$ or $\alpha_t = q_t^*$, for $q > 0$ sufficiently large.

Stability theory is not well developed outside of very special cases, such as the use of Exercise 9.3. This exercise is introduced by Gordon [146], who describes this other successful function approximation architectures. A generalization of binning soft state aggregation was introduced in [324]. Stability theory for policy TD faces similar challenges as Q-learning [219, 249, 345]. Counterexamples show that the function class are required in general, even in a linear function approximation setting [21, 147, 341, 355].

# 9.11.3 GQ and Zap

The GQ-learning algorithm of Section 9.8.1 was introduced in [345] for linear approximation (see also [234]). Convergence theory was extended to nonlinear function approximation in [5].

The LSTD($\alpha$) algorithm 9.2 was introduced in [75] (also see [70, 2771]). It is an instance of stochastic Newton–Raphson, but the original motivation had nothing to do with minimizing the asymptotic convergence.

From Recall 4.11 that the Newton-Raphson flow was developed by Smale [325]. The Zap-Q learning algorithm was introduced in [112, 113] without knowledge of Smale's theory–the matrix gain was motivated by the asymptotic convergence, rather than creating a general tool for consistent algorithms.

The proof of convergence based on Figure 4 first appeared in [112], and soon after it was realized that the ODE approximation (9.97) was valid outside of the tabular setting [90, 107, 110].

The discontinuity of the vector field $f^0$ initially presented a challenge in analysis of Zap-learning: It wasn't obvious that the ODE approximation could be justified. In [90], this open question was resolved by appealing to special structure in Q-learning. The theory in [90] is completely general (applicable even nonlinear function approximation architecture, such as neural networks). A central idea can be explained within the context of the tabular setting. Matrix $A_{n+1}$ appearing in (9.96) is a subgradient of $f_{n+1}$ at the value $	heta_n$ in the following sense: