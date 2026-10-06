
# ODE Methods for Algorithm Design

Consider the unstructured problem in which $u_t = -\theta^\top x_t$, in the goal is to minimize the objective function

$$\Gamma(\theta) = \sum \nu(x_0^i)J_{\theta}(x_0^i)$$

where $u$ is a pmf on the state space, and $J_{\theta}$ is the infinite cost with the feedback law determined by $\theta$:

$$J_{\theta}(x_0) = \int c(x_t, u_t)dt, \quad x_0 \in \mathbb{R}^n.$$

To apply qSGD, it would be necessary to approximate by the horizon objective

$$J_{\theta}(x_0) = \int c(x_t, u_t)dt + x_T^\top S_T x_T$$

with $S_0 \ge 0$ included to ensure a stable control solution.

Before considering qSGD, we should first see if the gradient flow will be successful:

$$\frac{d}{dt}\theta = -\nabla\Gamma(\theta).$$

It is simplest to return to the infinite horizon setting, so that $T = \infty$ and $S_0=0$. Analysis is based on the correlation matrix

$$\Sigma_0 = \sum \nu(x_0^i)x_0^i{x_0^i}^\top$$

and the solution $X_{\theta}$ to the Lyapunov equation

$$(A - B_0\theta^\top)X_{\theta} + X_{\theta}(A - B_0\theta)^\top + S_0 = 0$$

We begin with bad news: it is known that $\Gamma$ is nonconvex in $\theta$. An in [77] shows that the domain of $\Gamma(\theta)$ is finite and not convex, but this also brings good news. It has been known since the 1980s that $\nabla\Gamma(\theta)$ vanishes only at $\theta = \theta^*$, and that $V(\theta) = \Gamma(\theta) - \Gamma(\theta^*)$ is coercive (even though it is not everywhere finite). Hence it serves as a Lyapunov function.

$$\frac{d}{dt}V(\theta_t) = -|\nabla\Gamma(\theta_t)\|^2 < 0, \quad \text{whenever} \theta_t \neq \theta^*.$$

## 4.7.3 What about High Dimensions?

The qSGD algorithms are easy to code, and quickly converge to an approximately optimal parameter for the example considered in this section. In high dimensions, we can't expect to blindly apply any of these algorithms. For example, the choice of probing signal (4.47), where $i$ ranges from 1 to $d = 1,000$. If the frequencies $\{\omega_i\}$ are chosen in a narrow range, the limit (4.48b) will converge very slowly. The rate will be faster if the frequencies are widely separated, but then we would need a higher resolution ODE approximation to implement an algorithm.

## 4.8 Stability of ODEs

This challenge is well understood in the optimization literature. One approach to create a reliable algorithm is to employ block coordinate descent. This requires two ingredients:

- (i) A sequence of time points $T_0 = 0 < T_1 < T_2 < \dots$.
- (ii) A sequence of "parameter blocks" $B_k \in \{1, \dots, d\}$ for each $k \ge 0$, where the number of elements $d_B$ in $B_i$ is far smaller than $d$.

The qSGD ODE (4.94) is modified so that $\Theta_t(i)$ is held constant on the interval $[T_k, T_{k+1})$ for $i \notin B_k$, and

$$\frac{d}{dt}\Theta_t(i) = -a_t|v_t(i)|, \quad i \in B_k, t \in [T_k, T_{k+1}).$$

See [19, 72] for this more sophisticated approaches. At this end of the section title indicates that it contains advanced material. The stability theory needed here is if you want to fully understand why ODE methods surveyed in this chapter are "well behaved," and the concepts will be extended in the following section. We begin with proof of a central result and a simple corollary.

### 4.8.1 Grönwall’s Inequality

Proof of Grönwall’s Inequality, Consider the simpler inequality (4.7):

$$z_t = \gamma_t + \int_0^t \beta_s z_s ds.$$

Observe that $\gamma$ is continuous, under the assumption that $z$ and $\beta$ are continuous. We can "solve" this equation through the construction of a state model with $x_t = z_t - \gamma_t$, and obtain $z_t$. From the integral equation with initial condition $x_0 = 0$, the time-varying state model

$$\frac{d}{dt}x_t = \beta_t x_t + \gamma_t, \quad z_t = x_t + \gamma_t$$

has an explicit solution:

$$x_t = \int_0^t u_s \exp(\int_s^s \beta_r dr).$$

We next turn to the inequality (4.6), which we can derive

$$z_t = \alpha_t + \int_0^t \beta_s ds - \delta_t,$$

where $\delta_t \ge 0$ for each $t$. Define $\gamma_t = \alpha_t - \delta_t$ and obtain, with $u_t = \beta_t\gamma_t$ as before,

$$x_t = \int_0^t u_s \exp(\int_s^t \beta_r dr) ds \le \int_0^t \beta_s \alpha_s ds.$$

Using $z_t \le \alpha_t$ then gives (i). We establish (ii): If the function is nondecreasing, then from part (i) and the assumption that $\beta$ is nondecreasing,

$$z_t = \alpha_t + \int_0^t \beta_s ds, \quad 0 \le t \le T.$$

This bound implies (ii) by substituting $\int_0^t \beta_r dr) ds = \exp(\int_0^t \beta_r dr) - 1$. Grönwall's Inequality provides a crude bound that is needed in approximations:

**Proposition 4.19** Consider the ODE (4.2), subject to the Lipschitz condition (4.5). Then,

- (i) There is a constant $B_f$ depending only on $t$ such that
$$|\partial_t| \le (B_f + \|\theta_0\|)e^{Lt} - B_f, \quad (4.18a)$$
$$|\partial_t - \theta_0\| \le (B_f + \|\theta_0\|)e^{Lt}, \quad t \ge 0. \quad (4.18b)$$
- (ii) If there is an equilibrium $\theta^*$, then for each condition,
$$|\partial_t - \theta^*\| \le \|\theta_0 - \theta^*\|e^{Lt}, \quad t \ge 0.$$

*Proof* We present a complete proof of (ii) and 4.18a (the proof of 4.18b is similar).

If there is an equilibrium $\theta^*$, this means that $f(\theta^*) = 0$. The proof of 4.18b begins with (4.3), in the form

$$\partial_t - \theta^* = \theta_0 - \theta^* + \int_0^t f(\partial_\tau) d\tau, \quad 0 \le t \le T.$$

Under the equilibrium condition and the Lipschitz assumption,

$$|f(\partial_t)\| \le \|f(\partial_t) - f(\theta^*)\| \le L|\partial_t - \theta^*\|.$$

Writing $z_t = \|\partial_t - \theta^*\|$, combined with (4.3) gives

$$z_t \le z_0 + L \int_0^t z_\tau d\tau, \quad 0 \le t \le T.$$

Grönwall's Inequality gives us (ii): Apply Proposition 4.2 (ii) using $\beta_t = L$ and $z_0 = \|\theta_0 - \theta^*\|$. To establish, take $\theta^* \in \mathbb{R}^d$ and use

$$z_t \le z_0 + L \int_0^t z_\tau d\tau, \quad 0 \le t \le T.$$

Wait, let's re-examine the logic. The OCR text was quite garbled. Let's clean up the flow based on standard ODE theory context.

## 4.8.2 Lyapunov Functions

The survey in Section 4.5 tells us much of what we need to know about Lyapunov functions. The goals of algorithm design is to ensure global asymptotic stability, so that the ODE does not “blow up”. The ODE is ultimately bounded if there is a bounded set $S \subset \mathbb{R}^d$ such that for each initial condition $\theta_0$, there is a time $T(\theta_0)$ such that $\theta_t \in S$. There is naturally a Lyapunov condition to:

$$\nabla V(\theta) \le -\delta_0, \quad \theta \neq \theta^*.$$

On the bound on first time $T_S$ is a function of Exercise 2.12! It follows easily from the sample path interpretation of (4.19):

$$\frac{d}{dt}V(\theta_t) \le -1, \quad 0 \le t \le T_S(\theta), \quad \theta_0 \in \mathbb{R}^d. \quad (4.11)$$

**Proposition 4.20** Assume that there is a continuously differentiable function $V: \mathbb{R}^d \to \mathbb{R}_+$ satisfying (4.19) for $\delta_0 > 0$ and set $S \subset \mathbb{R}^d$. Then $T(\theta_0) = \min\{t \ge 0: \theta_t \in S\}$ satisfies $T(\theta_0) \le \delta_0^{-1}V(\theta_0)$.

*Proof* We take $\delta_0 = 1$ without loss of generality (obtained by scaling the function $V$ if necessary). Integrating each side from time $t=0$ to $t=T_N = \min(N, T_S(\theta))$ gives the fundamental theorem of calculus

$$V(\theta_{T_N}) - V(\theta_0) \le -T_N,$$

giving $\min(N, T_S(\theta)) \le V(\theta_0)$, and the desired bound on choosing $N > V(\theta_0).
