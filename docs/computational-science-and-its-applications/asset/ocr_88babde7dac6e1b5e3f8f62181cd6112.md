We then obtain the optimal control problem on the time-discrete level:

min_{(p,q,u,s)} I(p,q,u,s) := \sum_{i\in\mathcal{I}} \sum_{n=1}^{N} \int_{0}^{\ell_i} I_i(p_{i,n},q_{i,n})dx + \frac{\nu}{2} \sum_{j\in\mathcal{J}^S} \sum_{n=1}^{N} |u_j(n)|^2 + \frac{\mu}{2} \sum_{j\in\mathcal{J}_v\setminus\mathcal{J}_c} \sum_{n=1}^{N} s_{j,n}^2

s.t.

(p,q,u,s) satisfies (2.8). (2.9)

In Equation (2.4), we consider edgewise given cost functions e.g.

I_i(p_{i,n},q_{i,n})(x) := \frac{\kappa_i}{2} \left\{ |p_{i,n}(x)-p_{i,n}^d(x)|^2 + |q_{i,n}(x)-q_{i,n}^d(x)|^2 \right\}, x\in(0,\ell_i), i\in\mathcal{I}.

It is clear that (2.4) involves all time-steps in the cost functional. We would like to reduce the complexity of the problem even further. To this aim we consider what has come to be known as “instantaneous control.” This amounts to reducing the sums in the cost function of Equation (2.9) to the time-level t_{n+1}. This strategy has is known as a “rolling horizon approach,” the simplest case of the “moving horizon” paradigm, see e.g. [8, 9]. Thus, for each n = 1, …, N − 1 and given p_{i,n}, q_{i,n}, we consider the problems

min_{(p,q,u,s)} I(p,q,u,s) := \sum_{i\in\mathcal{I}} \int_{0}^{\ell_i} I_i(p_i,q_i)dx + \frac{\nu}{2} \sum_{j\in\mathcal{J}^S} |u_j|^2 + \frac{\mu}{2} \sum_{j\in\mathcal{J}_v\setminus\mathcal{J}_c} s_j^2

s.t.

(p,q,u,s) satisfies (8) at time level n + 1. (2.10)

It is now convenient to discard the actual time level n + 1 and redefine the states at the former time as input data. To this end, we introduce \alpha_i := \frac{1}{\Delta t}, f_i^1 := \frac{1}{\Delta t} p_{i,n}(x), f_i^2 := \frac{1}{\Delta t} q_{i,n}(x), \gamma_i(x) := \frac{\lambda c_i^2}{2D_i a_i^2} \frac{1}{p_{i,n}(x)} and rewrite Equation (2.8) as

\alpha_i p_i(x) + \frac{c_i^2}{a_i} \partial_x q_i(x) = f_i^1, x\in(0,\ell_i), i\in\mathcal{I}
\alpha_i q_i(x) + \partial_x p_i(x) + \gamma_i(x) q_i(x) |q_i(x)| = f_i^2, x\in(0,\ell_i), i\in\mathcal{I}
g_j(p_i(n_j), q_i(n_j)) = u_j, i\in\mathcal{I}_j, j\in\mathcal{J}^S
p_i(n_j) = p_k(n_j), \forall i,k\in\mathcal{I}_j, j\in\mathcal{J}^M \setminus (\mathcal{J}_c \cup \mathcal{J}_v)
\sum_{i\in\mathcal{I}_j} d_{ij} q_i(n_j) = 0, j\in\mathcal{J}^M
s_j^v \left( p_i(n_j) - p_k(n_j) \right) + (1 - s_j^v) q_i(n_j) = 0, j\in\mathcal{J}_v, i\in\mathcal{I}_j^-, k\in\mathcal{I}_j^+
s_j^c \left( u_j - C \left( \left( \frac{p_k(n_j)}{p_i(n_j)} \right)^{\operatorname{sign}(q_k(n_j))\kappa} - 1 \right) \right) + (1 - s_j^c) \left( p_i(n_j) - p_k(n_j) \right) = 0 \quad j\in\mathcal{J}_c, i\in\mathcal{I}_j^-, k\in\mathcal{I}_j^+. (2.11)