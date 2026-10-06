
## 126 ODE Methods for Algorithm Design

The crucial part of the proposition requires that we modify the set $S'$. Since it is compact, and $V$ is inf-compact, there exists $N < \infty$ such that $S \subset S_V(N) = \{\theta : V(\theta) \leq N\}$, with $S_V(N)$ also compact. Hence,

$$\nabla V(t, \theta(t)) \leq -1, \quad \theta \in \mathbb{R}^d, \ V(\theta) \geq N.$$

In fact, we write $V(\theta_t) > N$, since $\theta \notin S_V(N)$, but the left-hand side is continuous. Because $V(\theta_t)$ is decreasing when $\theta_t \in S_V(N)$, it follows that the set $S_V(N)$ is absorbing, which means that $\theta_t \in S_V(N)$ for all $t \geq T_S(0)$.

### 4.8.3 Gradient Flows

The proofs of Propositions 4.11 and 4.13 rely on Lyapunov techniques and the following:

**Lemma 4.21 (Arzelà-Ascoli Theorem)** *Consider a sequence of vector-valued functions $\{\gamma^n : n \geq 0\}$ that satisfy these two conditions on a bounded time interval $[a,b]$*

- (i) Uniformly bounded: There is a constant $B$ such that $|\gamma_t^n| \leq B$ for all $n$ and $a \leq t \leq b$.
- (ii) Equicontinuity: For each $\epsilon > 0$, there exists $\delta > 0$ such that $|\gamma_t^n - \gamma_s^n| \leq \epsilon$ for every $n$, and every $t, s \in [a,b]$ satisfying $|t - s| \leq \delta$.

Then there exists a sequence $\{\gamma^n\}$ and a continuous function $\gamma^\infty$ such that

$$\lim_{n \to \infty} ||\gamma_t^n - \gamma_t^\infty|| = 0.$$

Equicontinuity holds under a uniform Lipschitz bound: $|\gamma_t^n - \gamma_s^n| \leq L|t - s|$ for fixed $L$, and all $t, s, n$.

**Proof of Proposition 4.11** We first note that the existence of an optimizer follows from the assumptions: The optimizer $\theta^*$ for the primal exists because of the assumptions on $\Gamma$. It remains core and convex when its domain is restricted to the set $\{\theta : g(\theta) = 0\}$. The dual optimizer $\lambda^*$ is then obtained via the first-order conditions for optimality:

$$0 = \nabla_{\theta}\mathcal{L}(\theta^*, \lambda^*) = \nabla \Gamma(\theta^*) + D^T\lambda^*.$$

Multiplying each side by $D$ and inverting gives $\lambda^* = -[DD^T]^{-1}\nabla \Gamma(\theta^*)$, and then by construction

$$\varphi(\lambda^*) = \min_{\theta} \mathcal{L}(\theta, \lambda^*) = \Gamma(\theta^*) + \lambda^{*T}g(\theta^*) = \gamma^*.$$

The proof of convergence is similar to Proposition 4.7. The Lyapunov function

$$V(\theta, \lambda) = \frac{1}{2}||\theta - \theta^*||^2 + \frac{1}{2}||\lambda - \lambda^*||^2.$$

Applying the chain rule,

$$\frac{d}{dt}\mathcal{L}(\theta_t, \lambda_t) = ((\theta_t - \theta^*, \nabla_{\theta}\mathcal{L}(\theta_t, \lambda_t)) + (\lambda_t - \lambda^*, \nabla_{\lambda}\mathcal{L}(\theta_t, \lambda_t)) = -(\theta_t - \theta^*, \nabla_{\theta}\mathcal{L}(\theta_t, \lambda_t)) + (\lambda_t - \lambda^*, \nabla_{\lambda}\mathcal{L}(\theta_t, \lambda_t)).$$

Convexity of $\mathcal{L}$ in $\theta$ and linearity in $\lambda$ gives us,

$$\mathcal{L}(\theta_t, \lambda_t) \geq \mathcal{L}(\theta^*, \lambda^*) + (\theta_t - \theta^*, \nabla_{\theta}\mathcal{L}(\theta_t, \lambda_t))$$
$$\mathcal{L}(\theta_t, \lambda_t) \geq \mathcal{L}(\theta^*, \lambda^*) + (\lambda_t - \lambda^*, \nabla_{\lambda}\mathcal{L}(\theta_t, \lambda_t)).$$

### 4.8 Stability of ODEs

This implies the derivative bound

$$\frac{d}{dt}V(\theta_t, \lambda_t) \le [\mathcal{L}(\theta^*, \lambda_t) - \mathcal{L}(\theta_t, \lambda^*)] + [\mathcal{L}(\theta_t, \lambda^*) - \mathcal{L}(\theta^*, \lambda^*)] = [\mathcal{L}(\theta^*, \lambda_t) - \mathcal{L}(\theta_t, \lambda^*)] + [\mathcal{L}(\theta_t, \lambda^*) - \mathcal{L}(\theta^*, \lambda^*)]$$

The first term on the right-hand side can be simplified:

$$\mathcal{L}(\theta^*, \lambda_t) - \mathcal{L}(\theta_t, \lambda^*) = (\lambda_t - \lambda^*)^T g(\theta^*).$$

This is zero since $\theta^*$ is feasible. The second term is nonpositive due to saddle point property (4.4), giving

$$\frac{d}{dt}V(\theta_t, \lambda_t) \le \mathcal{L}(\theta^*, \lambda^*) - \mathcal{L}(\theta_t, \lambda^*) \le 0.$$

The inequality is strict when $\theta_t = \theta^*$ near $\Gamma$, and $\mathcal{L}(\cdot, \lambda^*)$ is strictly convex. From this, we obtain the following:

- (i) $V(\theta_t, \lambda_t)$ is nonincreasing, which implies that $\{\theta_t, \lambda_t\}$ evolve in a compact set.
- (ii) The bound $0 \le \int_{-\infty}^T \{\mathcal{L}(\theta^*, \lambda_t) - \mathcal{L}(\theta^*, \lambda^*)\} dt \le V(\theta_0, \lambda_0)$ is obtained for all $T>0$ by integration. And this implies $\lim_{t\to\infty}\mathcal{L}(\theta^*, \lambda_t) = \mathcal{L}(\theta^*, \lambda^*) = \Gamma(\theta^*)$.
- (iii) $\lim_{t\to\infty}\theta_t = \theta^*$ as $t\to\infty$ since $\mathcal{L}(\cdot, \lambda^*)$ is strictly convex.

To establish convergence of the dual, we revisit (4.3). Applying Lemma 4.21 $\gamma^n = (\theta_n, \lambda_{n+1})$, we can establish convergence for any $a < b$, and any subsequent limit $\gamma = (\theta^*, 0)$ is identically constant; Hence from (4.3), $$0 = \lim_{t\to\infty}\dot{\theta}_t = \lim_{t\to\infty}\{-\Gamma(\theta_t) - D^T\lambda_t\}.$$

It follows that the limit point $\lim_{t\to\infty}\{\lambda_t\}$ satisfies $0 = \Gamma(\theta^*) + D^T\lambda_\infty$, and, by multiplying side by $D$, $$0 = D\Gamma(\theta^*) + DD^T\lambda_\infty = 0.$$

Under full rank assumption, $\lambda_\infty = [-DD^T]^{-1}\Gamma(\theta^*)$.

**Proof of Proposition 4.13** We present a shorter proof, highlighting the differences with the first-order proof of 4.13. We first obtain a representation for Lagrange multiplier: from the first-order condition for optimality, we have $\nabla_{\theta}\mathcal{L}(\theta, \lambda) = 0$ at $(\theta, \lambda) = (\theta^*, \lambda^*)$. That is,

$$\Gamma(\theta^*) + D^T\lambda^* = 0 \quad \text{with } D = \partial g(\theta^*),$$

and thus by full rank assumption, $\lambda^* = [-DD^T]^{-1}\Gamma(\theta^*)$. Based on this representation, the proposition is established once we show that $\{\theta_t, \lambda_t\}$ is bounded and $\lim_{t\to\infty}\theta_t = \theta^*$. As in the previous proposition this then implies that, with $D_t \equiv \frac{\partial g}{\partial \theta_t}$,

$$0 = \lim_{t\to\infty}\frac{d\theta_t}{dt} = \lim_{t\to\infty}\{-\Gamma(\theta_t) - D^T\lambda_t\}.$$

## ODE Methods for Algorithm Design

Under convergence of $\{\theta_t\}$ and the full rank condition, this implies that $\{\lambda_t\}$ is also.

$$\lim_{t\to\infty}\lambda_t = -\lim_{t\to\infty}\{D_t D_t^T\}^{-1} D_t \Gamma(\theta_t) = \lambda^*.$$

To complete the proof, we use the quadratic Lyapunov function (4.11) to establish of $\{\theta_t\}$. Apply the chain rule to obtain

$$V(\theta_T, \lambda_T) = V(\theta_0, \lambda_0) + \int_0^T \langle\theta_t - \theta^*, \nabla_{\theta}\mathcal{L}(\theta_t,\lambda_t)\rangle + \langle\lambda_t - \lambda^*, \nabla_{\lambda}\mathcal{L}(\theta_t,\lambda_t)\rangle dt + \int_0^T (\lambda_t - \lambda^*)^T d\gamma_t.$$

The final integral can be bounded as follows:

$$\int_0^T (\lambda_t - \lambda^*)^T d\gamma_t = -\lambda^* \int_0^T d\gamma_t \le 0.$$

The equality follows from (4.39), and the inequality follows from the assumption that the $\lambda$ and $\lambda^*$ are $n$-dimensional vectors with nonnegative entries. Following as in the case of equality constraints,

$$V(\theta_T, \lambda_T) - V(\theta_0, \lambda_0) \le \int_0^T [L(\theta_t,\lambda_t) - L(\theta^*,\lambda^*)] + [L(\theta^*,\lambda^*) - L(\theta_t,\lambda_t)] dt = \int_0^T \{\lambda_t^T g'(\theta_t) + [L(\theta^*,\lambda^*) - L(\theta_t,\lambda_t)]\} dt.$$

This implies that $V(\theta_T,\lambda_T)$ is nonincreasing, since each term in the integrand is nonpositive:

$$\lambda_t^T g'(\theta_t) \le 0 \quad \text{and} \quad L(\theta^*,\lambda^*) - L(\theta_t,\lambda_t) \le 0.$$

### 4.8.4 The ODE at $\infty$

We consider here another way to verify that the ODE (4.2) is ultimately bounded. idea is pretty simple: to see if the ODE is ultimately bounded, we only need to consider values of $\vartheta$ that are "very big". Rather than using a telescope to examine these big states, we scale and use the resulting dynamics. To make this explicit we require to make dependency on the initial condition explicit,

$$\vartheta_t^r \stackrel{\text{def}}{=} r^{-1}\vartheta(t;r\theta_0).$$

We have $\vartheta_0^r = \theta_0$ for any $r \ge 1$, and we obtain from (4.2),

$$\frac{d}{dt}\vartheta_t^r = r^{-1}\frac{d}{dt}(t;r\theta_0) = r^{-1}f(\vartheta(t;r\theta_0)).$$
