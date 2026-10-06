
## 10.3 Regeneration

The proposition tells us that the choice of basis $\psi$ remains valid for approximating the advantage function, provided $w$ does not depend upon $u$. The Law of Large Numbers motivates an algorithm as seen in Proposition 10.6. Recall Section 9.5.4 for explanation of the bases $\psi^\circ$.

### LSTD(1) for Advantage with Weighting (On-Policy)

With weighting function $w: X \rightarrow (0, \infty)$, initialization $\zeta_0 \in \mathbb{R}^m, \Sigma_0 \in \mathbb{R}^{m \times m}$, and time horizon $N$,
$$\omega = \Sigma_N^{-1}\psi_N$$
$$\zeta_n = \gamma \zeta_{n-1} + w_n \psi_n, \quad w_n = w(\Phi(n)), \quad \psi_n = \psi^\circ(\Phi(n)), \quad 1 \leq n \leq N.$$
$$\Sigma_N = \frac{1}{N} \sum_{n=1}^N \zeta_n \psi_n^T$$
$$\psi_N = \frac{1}{N} \sum_{n=1}^N w_n \zeta_n^T$$

### 10.3 Regeneration

The representation (6.26) for Poisson's equation admits a generalization to the discounted-cost criterion. Let $z^* = (x', u) \in X \times U$ denote any state with positive steady-state probability $w(z^*) > 0$. Consider the function introduced before (9.5):
$$\hat{Q}_\gamma(z) = \mathbb{E}\left[\sum_{k=0}^{\tau_*-1} \gamma^k \delta(\Phi(k)) \mid \Phi(0) = z\right] + \mathbb{E}\left[\gamma^{\tau_*} \sum_{k=0}^{\infty} \gamma^k \delta(\Phi(k)) \mid \Phi(0) = z\right]$$
Apply the Markov property (see Section A.2.3) to obtain
$$\mathbb{E}\left[\sum_{k=0}^{\infty} \gamma^k \delta(\Phi(k)) \mid \Phi(0) = z\right] = \mathbb{E}\left[\gamma^{\tau_*} \hat{Q}_\gamma(\Phi(\tau_*)) \mid \Phi(0) = z\right]$$
$$\hat{Q}_\gamma(z^*) = \mathbb{E}[\gamma^{\tau_*} \mid \Phi(0) = z].$$

A similar decomposition holds for $Q_\gamma$:

**Lemma 10.10** The following hold for $\gamma \in [0, 1]$:
$$\tilde{Q}_\gamma(z) = \mathbb{E}\left[\sum_{k=0}^{\tau_*-1} \gamma^k \delta(\Phi(k)) \mid \Phi(0) = z\right] + \hat{Q}_\gamma(z^*) \mathbb{E}[\gamma^{\tau_*} \mid \Phi(0) = z].$$
$$Q_\gamma(z) = \mathbb{E}\left[\sum_{k=0}^{\tau_*-1} \gamma^k \delta(\Phi(k)) \mid \Phi(0) = z\right] + Q_\gamma(z^*) \mathbb{E}[\gamma^{\tau_*} \mid \Phi(0) = z].$$

### 3.7 Setting the Stage, Return of the Actors

Consequently, $\lim_{\gamma\to1} \tilde{Q}_{\gamma}(z) = H_3(z) + \tilde{Q}_1(z^*)$, where $H_3$ is the solution to Poisson's equation:
$$H_3(z) = \mathbb{E}\left[\sum_{k=0}^{\tau_*-1} \tilde{c}(\Phi(k)) \mid \Phi(0) = z\right].$$

For $\gamma \sim 1$ we might opt to estimate the finite horizon objective to obtain an algorithm with reduced variance. Consider for fixed-point $\phi$:
$$J_{\gamma}(z) = \mathbb{E}\left[\sum_{k=0}^{\tau_*-1} \gamma^k c(\Phi(k)) \mid \Phi(0) = z\right].$$

Writing $J_{\gamma}(z) = c(z) + \mathbb{E}[\gamma \mathbb{1}\{\tau_{\gamma} \ge 2\}]$, the following DP equation is established:
$$J_{\gamma}(z) = c(z) + \gamma \sum_{z^* \neq z} P(z,z')J_{\gamma}(z') = \mathbb{E}[c_n + \gamma\mathbb{1}\{\Phi(n+1) \neq z^*\} J_{\gamma}(\Phi(n+1)) \mid \Phi(n) = z].$$

The finite horizon objective introduces new eligibility vector: For $n \ge 0$,
$$\zeta_n = \sum_{\tilde{n}^n \le k \le n} (\lambda\gamma)^{n-k}\psi_{(k)}$
where $\tilde{n}^n = \max\{k \le n : \Phi(k) = z^*\}$.

In the special case $\Phi(k) \neq z^*$ for $k=0,...,n$ (i.e., the maximum in (10.19b) is over an empty set), we define $\tilde{n}^n=0$. The sequence of eligibility vectors has a recursive form, which with (10.118) motivates the recursive TD($\lambda$) algorithm:

### Regenerative TD($\lambda$) Algorithm (On-Policy)

For initialization $\theta_0, \zeta_0 \in \mathbb{R}^d$, the sequence of estimates are defined recursively:
$$\mathcal{D}_{n+1} = (-H^{\theta_n}(\Phi(n)) + c_n + \gamma\mathbb{1}\{\Phi(n+1) \neq z^*\} H^{\theta_n}(\Phi(n+1)))\big|_{\theta=\theta_n}$$
$$\zeta_{n+1} = \lambda\gamma\mathbb{1}\{\Phi(n+1) \neq z^*\}\zeta_n + \psi(n+1)$$

With the introduction of regularization, the algorithm remains practical even when $\gamma=1$. For linear function approximation, this is SA recursion:
$$\theta_{n+1} = \theta_n + \alpha_{n+1}[A_{n+1}+b_{n+1}]$$
$$A_{n+1} = \zeta_n [-\psi_{(n)} + \gamma\mathbb{1}\{\Phi(n+1) \neq z^*\}\psi_{(n+1)}]^T,$$
$$b_{n+1} = \zeta_n c_n.$$

### 3.4 Average Cost and Every Other Criterion

The value of $\lambda = 1$ is explained in Theorem 10.11, whose proof can be found in 10.9.

**Theorem 10.11 ($L_2$ Optimality of TD(1))** Consider the algorithm (10.20) with linear function approximation $H^\theta = \theta \psi$. Assume that $\Phi$ is unich and $\omega(z^*) > 0$. In the special case $\lambda = 1$:
(i) $E_\omega[A_n] = -R(0)$ and $E_\omega[b_n] = -E_\omega[J_\gamma(\Phi(n))\psi(\Phi(n))]$.
(ii) Any solution to $0 = E_\omega[D_{n+1}]$ solves the minimum norm problem:
$$\theta^* = \arg\min_{\theta} ||H^\theta - J_\gamma||^2 = \arg\min_{\theta} \mathbb{E}[(H^\theta(\Phi(n)) - J_\gamma(\Phi(n)))^2]. \quad (10.22)$$

As in TD(1) algorithms with linear function approximation, the characterization of $A$ strongly motivates the use of LSTD(1). One formulation is given by:
$$\theta_{N}^* = \tilde{A}^{-1}\tilde{b}, \quad (10.23)$$
where $N$ denotes the time horizon, and for $\tilde{R}_0 > 0$,
$$\tilde{A} = -\frac{1}{N}\sum_{k=1}^N (\tilde{R}_0 + \psi_{(k)})\psi_{(k)}^T, \quad \tilde{b} = -\frac{1}{N}\sum_{k=1}^N \zeta_n c_n.$$

#### 4.4.1 Other Criterion

When we optimize over a family of policies, as described at the start of this chapter, we expect to find a single policy in the family that minimizes the discounted-or total-cost criterion from any initial condition. It is customary to choose a pmf $\mu$ on $Z = X \times U$, and define the objective for optimization as follows:
$$\Gamma(\phi) = \sum_z h_\phi(z)\mu(z),$$
where $h_\phi$ is the value function associated with the policy $\phi$ for the chosen optimality. In Section 10.5, the family is defined through a finite-dimensional parameterization $\{\phi : \theta \in \mathbb{R}^d\}$, and we write $\Gamma(\theta)$ rather than $\Gamma(\phi)$.

In the following, we show how to translate one optimality criterion to another. Translation is accompanied by the creation of a Markov chain $\Psi$, a strictly increasing sequence of times $\{N_n : n \geq 1\}$, and a modified cost $\tilde{c}$, all designed so that the partial sums
$$S_n = \sum_{k=N_n}^{N_{n+1}-1} \tilde{c}(\Psi(k)), \quad n \geq 1, \quad (10.24)$$
are i.i.d., with common mean $\Gamma(\phi)$. It will follow by construction that $\Gamma(\phi)$ is proportional to average cost for the newly constructed stochastic process.

### 3.2 Setting the Stage, Return of the Actors

There is no need to identify which policy is under consideration in the constructions that follow so we write $\Gamma$ instead of $\Gamma(\Phi)$, and let $T$ denote the transition matrix for the Markov chain $\Phi$.

### Discounted Cost

Take $h$ equal to the discounted-cost value function obtained by a policy $\Phi$, and denote
$$\Gamma = \sum_{z}^{\infty} h(z)u(z) = \mathbb{E}\left[\sum_{k=0}^{\infty} \gamma^k c(\Phi(k))\right], \Phi(0)\sim \gamma.$$
The construction is defined through regeneration: $\Psi(k) = (\Phi(k), B(k))$, in which $B(k) \in \{0,1\}$ for each $k$, with $B(k)=1$ indicating that a regeneration occurred at time $k$, along the transition matrix $T$.

We begin with the construction of the first regeneration time. Let $B$ be a Bernoulli process with parameter $1-\gamma$, and $T_* = \min\{k \ge 1 : B(k)=1\}$, we have
$$P(T_* > k | \Phi(0)) = \gamma^k \quad k \ge 0,$$
and by independence the decomposition from (10.25):
$$h(z) = \mathbb{E}\left[\sum_{k=0}^{T_*-1} \gamma^k c(\Phi(k)) \mid \Phi(0) = z\right].$$
To define $\Psi$, we let $N_1 = T_*$, define the first regeneration time, and $\widehat{\Phi}(k) = \Phi(k)$ for $0 \le k \le T_*-1$. This construction, with $\{N_n\}$, a renewal process, defined inductively by
$$N_{n+1} = \min\{k \ge N_n+1 : B(k)=1\}, \quad n \ge 1$$
with $\Phi(k)$ defined as before on the interval $[N_n \le k < N_{n+1}]$ for each $n$. The random variable $\widehat{\Phi}(T_*)$ is independently sampled from the process, with distribution $\mu$.

In the following, we show how to translate one optimality criterion to another. Translation is accompanied by the creation of a Markov chain $\Psi$, a strictly increasing sequence of times $\{N_n : n \geq 1\}$, and a modified cost $\tilde{c}$, all designed so that the partial sums
$$S_n = \sum_{k=N_n}^{N_{n+1}-1} \tilde{c}(\Psi(k)), \quad n \geq 1, \quad (10.24)$$
are i.i.d., with common mean $\Gamma(\phi)$. It will follow by construction that $\Gamma(\phi)$ is proportional to average cost for the newly constructed stochastic process.
