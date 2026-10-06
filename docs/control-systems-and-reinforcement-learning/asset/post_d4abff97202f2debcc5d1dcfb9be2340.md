
# Markov Chains

- (a) If $\pi$ is an invariant pmf, so that $\pi P = \pi$, it then follows:

$$\pi[I - P + s \otimes \nu] = \delta\nu$$

where $\delta \geq 0$. Provide a formula for $G$ in terms of $\pi, s$ and $\nu$. Arg $\mu = \nu G$ is a left eigenvector of $P$, the inverse $G = [I - (P-s \otimes \nu)]^{-1}$ exists, and $\delta > 0$.

- (b) Postulate a representation for a solution to Poisson's equation $Ph = h - \hat{c}$, based on the matrix $G$.

## 6.21 PF Theory and Sensitivity. We now revisit the sensitivity function in Theorem 6.8. You will obtain an expression for the gradient of $h_{\theta}$ at $\theta^0 \in \mathbb{R}^d$, subject to these local assumptions: For some $\varepsilon > 0$:

- $P_{\theta}(x,x')$ and $c_{\theta}(x)$ are continuously differentiable for $\theta$ in the region $B_{\varepsilon} ={\theta:|||\theta-\theta^0|| \leq \varepsilon\}$. The Markov chain with transition matrix $P_{\theta}$ is uni-chain for each $\theta \in B_{\varepsilon}$ and satisfies the uniform minimization condition for $\theta$ in this:

$P_{\theta}(x,x') \geq s(x)\nu(x'), \quad x,x' \in X$,

where $\nu$ is a pmf, and $\pi_{\theta}(s) > 0$. Obtain a formula for $\nabla_{\theta}h_{\theta}$, using $h_{\theta} = G_{\theta}\hat{c}$,

$G_{\theta} = [I - P_{\theta} + s \otimes \nu]^{-1}$.

$$\frac{\partial}{\partial\theta}G_{\theta} = G_{\theta}\frac{\partial}{\partial\theta}P_{\theta}G_{\theta}.$$

## 6.22 Risk-Sensitive Control [374]. Another application of $P_{\theta}$ theory is infinite-horizon control with the risk-sensitive criterion.

- (a) The log generating function associated with a real-valued random variable $\Xi$ is $\Lambda(r) = \log E[exp(r\Xi)]$, with $r \in \mathbb{R}$ variable. As $\Lambda$ is finite in a neighborhood of the origin. Obtain the first and second derivatives of $\Lambda$ at the origin, to justify the ``small $r$ approximation":

$$\Lambda(r) = mz + \frac{1}{2}\sigma_z^2r^2 + O(r^3),$$

where the coefficients are the mean and variance of $\Xi$.

- (b) One formulation of risk-sensitive control is motivated by this Taylor series approximation, with $r > 0$

$$\sum_{k=0}^{\mathcal{N}-1} c(X(k)) + V_0(X(\mathcal{N}))$$

where $\mathcal{N} \geq 1$, $c$ is a cost function, and $V_0$ is the terminal cost. Consider the finite space Markov chain with $X=\{1, \dots, n\}$, induce an $n \times n$ matrix with entries

$R(i,j) = \exp(rc(i))P(i,j)$,

and let $(v, \lambda)$ denote a solution to the eigenvector equation $Rv = \lambda v$. For each $i \in X$,

$$\lambda^n v_i = \sum_{j} R^n(i,j)v_j = E[\sum_{k=0}^{\mathcal{N}-1} c(X(k)) + \mathcal{V}(X(\mathcal{N})) \mid X(0) = i],$$

where $\mathcal{V}(i) = \log(v_i)$ for each $i$. Conclude that $\Lambda = \log(\lambda)$ is the infinite-horizon risk-sensitive cost, defined by the following (using the notation (6.9)):

$$H_{\infty}(x)=\lim_{N\to\infty} \frac{1}{N} \log\left\{E_r\left[ \exp\left(r \sum_{k=0}^{N-1} c(X(k))\right)\right]\right\}, \quad X(0)=x\in X.$$

- (c) Solve the equation $R_0 = \Lambda v$ for the four-state Markov chain with transition matrix (6.21), with $c(i)=i$, and verify the following identities:

$$\Lambda(r)|_{r=0}=\eta=\pi(c), \quad \log(v_j(r)/v_i(r))|_{r=0}=h_j, \quad 1\le j\le 4,$$$$

where $h$ is the unique solution to Poisson's equation satisfying $h_1=0$.

## 6.11 Notes

As in [257], this word "chain" indicates that time is discrete, and the term *Markov process* is reserved for models in continuous time. The terminology is in honor of the Russian mathematician Andrey Markov. Good introductory texts include [138, 275], and for advanced material, some of the material in this chapter and Appendix B is adapted from [254, chapters 8 to 9] and its appendix. Standard texts on Perron-Frobenius theory are [277, 315], and the appendix of [254] contains a survey aimed at readers with interest in control. The reference [257] remains up-to-date source for Lyapunov and Poisson's equation for Markov chains on a general state. This book also contains potential theory in the general state setting, but this remains rapidly evolving [117, 196, 378].

It was first demonstrated in [253] that the finite-$n$ bound (6.43) cannot be obtained for M/M/1 queue and "skip-free" Markov chains on a countable state space. More on this topic can be found in [254, with details on Figure 6.6], and [119, 120] for a complete explanation of $I_{\theta}$ appearing in Section 8.3.

Techniques to obtain finite-$n$ bounds through introduction of control variates can be found in [194, 253] for applications of control in RL. Schweitzer introduced his sensitivity formula in his doctoral thesis, which was subsequently published in 1968 [251, 313]. See Konda's thesis for early history of optimization in RL [188, 191], and Section 10.10 of this book for more history.

## 7 Stochastic Control

By *stochastic control*, we mean that random disturbances and measurement noise are helpful to be accounted for explicitly in our control system. Markov decision processes (MDP) are a very special case. While the theory in this part of the book will focus exclusively on MDPs, the title of the chapter is meant to emphasize our goals rather than a particular set of techniques to explain the similarity between deterministic and stochastic control. The object of study in MDP theory is a state process $X = \{X(k) : k \ge 0\}$ that takes values in state space $X$. The evolution of $X$ is influenced by disturbances, as in nonlinear state model (6.3), and also control sequence $U = \{U(k) : k \ge 0\}$ taking values in input (or action) space $U$. In deterministic control, our objective is to choose $U(k)$ for every $k \ge 0$, based on observations, so that the system behaves as desired – the meaning depends on the application, as we will see in the examples that follow.

### 7.1 MDPs: A Quick Introduction

In this short introduction, we assume that the state and input spaces are finite, or countably infinite. This greatly simplifies statements of the definitions, in the uncontrolled setting. The first ingredient in an MDP is the controlled transition matrix: Subject to “admissibility” assumption defined later, the pair $(X(k), U(k))$ is a sufficient statistic in the following:

$$P\{X(k+1) = x' \mid X(0), \dots, X(k), U(0), \dots, U(k); X(k) = x, U(k) = u\} = P_u(x',x').$$

where the right-hand side is the controlled transition matrix, evaluated at the triplet $(u, x, x')$. More generally, for any $m, k \ge 0$ and function $g: X^{m+1} \to \mathbb{R}$,

$$E[g(X(k), X(k+1), \dots, X(k+m)) \mid X(0), \dots, X(k), U(0), \dots, U(k)] = E[g(X(k), X(k+1), \dots, X(k+m)) \mid X(k), U(k)].$$

The definition is far less abstract when we have a realization of the controlled Markov model:

$$X(k+1) = F(X(k), U(k), N(k+1)), \quad (7.1)$$

where $\mathcal{N}$ is an i.i.d. sequence. The controlled transition matrix has the explicit form

$$P_u(x, x') = P\{F(x, u, N(1)) = x'\}, \quad u \in U, x' \in X.$$

**Markov Decision Processes (MDP).** The definition requires three ingredients:

- (i) The controlled transition matrix, denoted $P_u(x, x')$ for $x, x' \in X, u \in U$.
- (ii) A cost function $c: X \times U \to \mathbb{R}$, and input constraints restricted by a set $U \subseteq C$ for $x \in X$.
- (iii) An objective, such as total cost: $h(x) = \sum_{k=0}^{\infty} E_x[c(X(k), U(k)]]$,
or average cost:

$$\lim_{n \to \infty} \frac{1}{n} \sum_{k=0}^{n-1} E_x[c(X(k), U(k))].\quad (7.2)$$

As in the deterministic setting, stationary policies play an important role. For any policy $\phi: X \to U$, if $U = \phi(X)$ for each $k$, then the controlled process $X$ is a Markov chain with transition matrix denoted by $\Phi_{\phi}$:

$$\Phi_{\phi}(x, x') = P_u(x, x')|_{u=\phi(x)}, \quad x, x' \in X.\quad (7.3)$$

For the total-cost-criterion, we have the following for each $x$:

$$h^*(x) = \min_{u \in U}c(x, u) + \sum_{x'} P_u(x, x')h^*(x')\}.$$ (7.4)$$

and the optimal policy is state feedback $\phi^*$, in which $\phi^*(x)$ is any minimizer of (7.4).

Also similar to deterministic control is the role of DP equations. Under mild assumptions, the minimal average cost $\eta^*$ does not depend on the initial condition, and there is a solution to the average-cost optimality equation (ACOE):

$$h^*(x) + \eta^* = \min_{u \in U}c(x, u) + \sum_{x'} P_u(x, x')h^*(x')\$.quad (7.5)$$

The function $h^*$ is known as the relative value function, and the optimal policy is again minimizer:

$$\phi^*(x) = \arg min_{u \in U}c(x, u) + \sum_{x'} P_u(x, x')h^*(x')\, \quad x \in X.$$ (7.6)$$

The "Q-function" of Q-learning is the function within the brackets:

$$Q^*(x, u) \overset{\text{def}}{=} c(x, u) + \sum_{x'} P_u(x, x')h^*(x'),\quadquad x \in X, u \in U$. (7.7)$$
