is a $\mathcal{Y}^n, P^{V,x}$ martingale. Check also that

$$
\alpha^n u(y_n) + \sum_{j=1}^{n-1} \alpha^j (u(y_j) - \alpha \Phi^{v_j}(y_1, \cdots y_j) u(y_j)),
$$

is a $\mathcal{Y}^n, P^{V,x}$ martingale.

**Remark.** We can consider the deterministic case as a particular case of a Markov chain, in which

$$
\pi(x, v, d\eta) = \delta_{g(x,v)}
$$

the Dirac measure at the point $g(x, v)$. However the control must remain defined in a closed loop manner. We cannot recover the open loop control in this manner. This is why to go through this path to consider the deterministic problem is unnecessary complicated.

# 4.2.2. SETTING OF THE PROBLEM.

Consider

(4.2.1) $$l(x, v) \ge 0,$$

and $U$ is a subset of a metric space.

We consider a controlled Markov chain described by its transition probability $\pi(x, v, \Gamma)$. Consider a control policy $V$ and construct the corresponding probability $P^{V,x}$ for the canonical process $y_n$. The functions $v_n(x_1, \cdots, x_n)$ appearing in the control must take values in $U$.

We define the cost functional

(4.2.2) $$
J_x(V) = E^{V,x} \sum_{n=1}^{\infty} \alpha^{n-1} l(y_n, v_n).
$$

If we accept the value $+\infty$ this quantity is well defined. The value function is defined by

$$
u(x) = \inf_V J_x(V).
$$

An important question is whether the value function satisfies a functional equation, as in the deterministic case, following algebraic arguments. This becomes highly non trivial, but we are going to show that it is possible, in a case which is useful for applications and mimics to some extent the deterministic case. In the general situation described above, we will avoid the difficulty by using arguments from analysis and not from algebra.

# 4.2.3. DIRECT APPROACH.

We consider the situation when the evolution of the dynamic system is described as follows. Consider a probability space $(\Omega, \mathcal{A}, P)$, on which is defined a stochastic process $D_1 \cdots D_n \cdots$ made of independent, identically distributed random variables. The notation $D$ recalls the demand process, which will appear constantly in the application to inventory control. We denote by $h(\xi)$ the probability density of a generic $D$, which lies in $R^k$ to fix ideas. The process $y_n$ is defined by

$$
y_{n+1} = g(y_n, v_n, D_n) \quad y_1 = x.
$$

We shall assume that the demand is observable. At time $n+1$, we have observed the values of $D_1 \cdots D_n$. So

$$
v_n = v_n(D_1, \cdots, D_{n-1}) \quad n \ge 2,
$$