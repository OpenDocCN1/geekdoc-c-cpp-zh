# 9.6 Watkins’s Q-Learning

In the tabular setting, it is common to write $H^n$ rather than $H^{	heta_n}$ (identifying the function approximation with the parameter). This is justified by the following representation: For $i$ and $	heta$,

```
$H^0(x^i, u^i) = \sum_{j=1}^d \theta(j)\psi_j(x^i, u^i) = \theta(i), \quad (9.73)$
```

where the final equality holds because of the tabular basis. Two versions of tabular Q-learning are distinguished by the way in which samples of $\Phi=(X,U)$ are obtained.

Either of the following algorithms is commonly known as Watkins’ Q-learning.

+   (i) Asynchronous: access to a single sample path of $\Phi$.
$H^{n+1}(x,u) = H^n(x,u)$ if $\Phi(n) \neq (x,u)$, and otherwise
$H^{n+1}(x,u) = H^n(x,u) + a_{n+1}[-H^n(x,u) + \gamma H^n(X(n+1))]$.
Asynchronous Q-learning can be implemented with a simulator to $Q^*$ is approximated based on observations of the system.

+   (ii) Synchronous: access to a simulator to generate the generic distribution $P_u(x,\cdot)$ via i.i.d. sample $\Xi$ on $X^n$, with $\Xi_n \sim P_u(x^n)$.
At iteration $n+1$ each entry of $H^{n+1}$ is updated for $i=1, \dots, d$,
$H^{n+1}(x^i,u^i) = H^n(x^i,u^i) + a_{n+1}[-H^n(x^i,u^i) + \gamma H^n(\Xi_{n+1}^i)]$.
In either case, given the estimate of the Q-function at iteration $n$, we obtain the $H^n$-greedy policy as any solution to

```
$\phi_n(x) = \text{arg} \max_{u} H^n(x,u), \quad x \in \mathrm{X}. \quad (9.74)$
```

This section restricts itself to the asynchronous case (to avoid repetition of equations and concepts in the theoretical development). Given the definition of the basis, asynchronous Q-learning is expressed as Q(0)-learning:

```
$\theta_{n+1} = \theta_n + a_{n+1}\mathcal{D}_n\zeta_n,\n$\mathcal{D}_{n+1} = -H^n(\Phi(n)) + c_n + \gamma H^n(X(n+1)),\n\zeta_n = \nabla_{\theta}H^n(\Phi(n))|_{\theta_n} = \psi(n). \quad (9.75)$
```

The recursion (9.75) for the Q-learning algorithm can be written in a form similar to the linear recursion (8.53b). By denoting $\zeta_{n+1} = \psi(X(n+1),\phi_n(X(n+1)))$, with $\phi_n$ $H^n$-greedy policy,

```
$\theta_{n+1} = \theta_n + \alpha_{n+1}[A_{n+1}\theta_n - b_{n+1}]\n\text{with} \quad A_{n+1} = \psi(n)\{\psi(n_{n+1})\top - \psi(n},\\nb_{n+1} = -c_n\psi(n). \quad (9.76)$
```

This is not a linear SA algorithm since the policy $\phi_n$ depends on $\theta_n$.