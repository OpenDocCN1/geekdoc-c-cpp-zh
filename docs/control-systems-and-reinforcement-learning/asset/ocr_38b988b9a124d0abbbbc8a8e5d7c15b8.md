# Value Function Approximations

As always, the output of the algorithm defines the final approximation $Q^{	heta^*}$. The ODE approximation is successful provided the second-step sequence size is relatively large:

```
$$\lim_{n\to\infty} \frac{eta_n}{\alpha_n} = \infty.$
```

There are several challenges and questions:

+   - We may have difficulty obtaining a global minimum of (5.54) the objective $\Gamma$ is not convex.
- Suppose that in fact $\hat{f}(\theta^*)=0$ does have a solution. Challenges remain with approximation of the ODE (5.55), beyond lack of convexity of the objective function. Nesterov discusses this root finding in his monograph [273, section 4.4.1]. He warns that it can lead to numerical instability: "... if our system of equations is linear, then such a transformation squares the condition number of the problem." He goes on to warn that it can lead to “aring the number of iterations” to obtain the desired error bound. To see this, consider the second-order approximation of the loss function at $\theta^*$:

```
$$\Gamma(\theta) \approx \Gamma(\theta^*) + (\theta-\theta^*)^T[A'MA^T](\theta-\theta^*),$
```

uses $\hat{f}(\theta)=0$. The appearance of $A'MA^T$ is the “squaring” that Nesterov warns about. If $A'$ has a large condition number, then we make things worse. The numerical challenge can be addressed with an alternative choice for $M$, provided this can be done without introducing additional complexity.

+   - But not least, it is not obvious that minimizing (5.54) is a worthwhile goal. Further research is needed to explain why $Q(\lambda)$ and DQN algorithms are often successful in practice, and to predict when these algorithms might fail.

# 5.4.5 Batch Methods and DQN

The Deep Q Network (DQN) algorithm was designed for neural network function approximation, the term “deep” refers to a large number of hidden layers. The basic algorithm is summarized here, without imposing any particular form for $Q^theta$.

One component of this approach is to abandon the purely recursive form of the predicting RL algorithms. In a batch RL, the time-horizon $T$ is broken into $B$ batches of more reasonable size, defined by the sequence of intermediate times $T_0 < T_1 < T_2 < ... < T_{B-1} < T_B$. The potential benefits are more obvious when we come to RL design using kernels for function approximation, or for stochastic control systems.

# DQN

With $\theta_0 \in \R^d$ given along with a sequence of positive scalars $\{\alpha_n\}$, define recursively,

```
$$\theta_{n+1} = \arg\min_{\theta}\{\Gamma_n(\theta) + \frac{1}{\alpha_{n+1}}||\theta-\theta_n||^2},\ \quad 0 \le n \le B-1, \quad (5.58a)$
```

> More on the source of condition number can be found in Section 8.6.1, with definitions.