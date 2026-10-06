# 380 Setting the Stage, Return of the Actors

$\mathcal{R}: \mathbb{R}^d 	o \mathbb{R}_+$, and modify the actor-critic algorithm to approximate regularized gradient descent:

```
$\frac{d	heta}{dt} = -
abla\Gamma(\theta) - \mathcal{R}(	heta) \quad (10.46)$
```

so that (10.44a) is replaced with

```
$\theta_{n+1} = \theta_n - \alpha_n + \alpha_n{\widehat{V}}_f(n) + \mathcal{R}_n(\theta_n))$
```

where $\mathcal{R}_n: \mathbb{R}^d 	o \mathbb{R}_+$ is potentially random, with $E[\mathcal{R}_n(\theta)] \approx \mathcal{R}(	heta)$ for each $	heta$ and all large $n$.

# 10.6 SGD without Bias

The ODE approximation in Proposition 10.17 can be obtained under assumptions weaker than (10.45).

A function class $\{\mathcal{H}^\theta: \theta \in \mathbb{R}^d\}$ of candidate approximations to the Q-functions is said to satisfy the compatible features property (CFP) if

```
$\Lambda_i^\theta = \mathcal{H}^\theta \quad$ for each $\theta \in \mathbb{R}^d$ and $1 \le i \le d. \quad (10.47)$
```

**Proposition 10.18** Suppose that $\{\mathcal{H}^\theta: \theta \in \mathbb{R}^d\}$ satisfies the CFP (10.47). Given $\theta \in \mathbb{R}^d$, let $Q$ denote a solution to the minimum norm problem:

```
$\tilde{Q} = \arg \min{||H - Q_0||_{\theta}^2} : H \in \mathcal{H}^\theta$.
```

Then,

```
$\nabla\Gamma(\theta) = E_{\theta}[\Lambda^\theta(\Phi(k))Q(\Phi(k))] = E_{\theta}[\Lambda^\theta(\Phi(k))\Phi(\Phi(k))]. \quad (10.48)$
```

Proof $L_2$ locality is equivalent to the orthogonality property:

```
$0 = E_{\theta}[[Q(\Phi(k)) - \tilde{Q}(\Phi(k))]H(\Phi(k))], \quad$ for all $H \in \mathcal{H}^\theta$.
```

The identity (10.48) is obtained by setting $\theta = \Lambda^\theta$ for each $i$.

The practical importance of the proposition is seen in reuniting Theorem 10.14: For $\theta$ and $U(k) = \phi^theta(X(k))$ for all $k$, the identity (10.48) will hold for the approximation obtained using TD(1), whenever the linear class classifies the CFP.

This assumption is not restrictive. In practice, we might start with a function class $\mathcal{H}^theta$, and for each $\theta$ define

```
$\mathcal{H}^\theta = {h = h^0 + \sum_{i=1}^d \omega_i\Lambda_i^\theta : h^0 \in \mathcal{H}^\theta, \omega \in \mathbb{R}^d}. \quad (10.49)$
```

While Theorem 10.14 is only when $\theta$ is independent of $n$, the theory of two time-scale SA gives us the following extension of Proposition 10.17:

**Proposition 10.19** Suppose that the assumptions of Proposition 10.17 hold, but with replaced the compatible features assumption (10.47).

Then, the ODE approximation of (10.44) is unchanged:

```
$\frac{d\theta}{dt} = -
abla\Gamma(\theta)$.
```