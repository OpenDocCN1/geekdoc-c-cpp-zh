# 10.4 Average Cost and Every Other Criterion

The value of $\lambda = 1$ is explained in Theorem 10.11, whose proof can be found in 10.9.

**Theorem 10.11 ($L_2$ Optimality of TD(1))** Consider the algorithm (10,20) with linear function approximation $H^	heta = 	heta^	op \psi$. Assume that $\Phi$ is uni-chain and $\omega(z^*) > 0$. In the special case $\lambda = 1$,

+   (i) $A 	riangleq E_\omega[A_n] = -R(0)$ and $b 	riangleq E_\omega[b_n] = -E_\omega[J_\gamma(\Phi(n))\psi(\Phi(n))]$.
(ii) Any solution to $0 = 	ilde{f}(	heta) = E_\omega[\zeta_n D_{n+1}]$ solves the minimum norm problem:

```
$$\theta^* = \arg\min_{\theta} ||H^	heta - J_\gamma||^2_	heta = \arg\min_{\theta} [(H^	heta(\Phi(n)) - J_\gamma(\Phi(n)))^2]. \quad (10.22)$
```

As in TD(1) algorithms with linear function approximation, the characterization of A strongly motivates the use of LSTD(1). One formulation is given by

```
$$\theta_{N}^* = \tilde{A}^{-1}\tilde{b}, \quad (10.23)$
```

where $N$ denotes the time horizon, and for $	ilde{R}_0 > 0$,

```
$$\tilde{A} = -\frac{1}{N}\sum_{k=1}^N \tilde{R}_0 + \psi_{(k)}\psi_{(k)}^	op, \quad \tilde{b} = -\frac{1}{N}\sum_{k=1}^N \zeta_n c_n.$
```

# 10.4 Average Cost and Every Other Criterion

# 10.4.1 Every Other Criterion

When we optimize over a family of policies, as described at the start of this chapter, we expect to find a single policy in the family that minimizes the discounted-or total-cost criterion from any initial condition. It is customary to choose a pmf $\mu$ on $Z = X \times U$, and define the objective for optimization as follows:

```
$$\Gamma(\phi) = \sum_z h_\phi(z)\mu(z),$
```

where $h_\phi$ is the value function associated with the policy $\phi$ for the chosen optimality. In Section 10.5, the family is defined through a finite-dimensional parameterization $\{\phi : \theta \in \mathbb{R}^d\}$, and we write $\Gamma(\theta)$ rather than $\Gamma(\phi^	heta)$.

In the following, we show how to translate one optimality criterion to another. Translation is accompanied by the creation of a Markov chain $\Psi$, a strictly increasing sequence of times $\{\mathcal{N}_n : n \geq 1\}$, and a modified cost $	ilde{c}$, all designed so that the partial sums

```
$$\S_n = \sum_{k=N_n}^{N_{n+1}-1} \tilde{c}(\Psi(k)), \quad n \geq 1, \quad (10.24)$
```

are i.i.d., with common mean $\Gamma(\phi)$. It will follow by construction that $\Gamma(\phi)$ is proportional to average cost for the newly constructed stochastic process.