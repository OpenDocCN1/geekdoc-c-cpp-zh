# 4.5 Quasistochastic Approximation

| $\mu = -0.47$ | Monte Carlo | $\mu = -0.48$ | QSA | $\mu = -0.48$ | QSA |
|---|---|---|---|---|--|
| $\sigma^2 = 2e-03$ | $g = 1$ | $\sigma^2 = 1e-03$ | $g = 1$ | $\sigma^2 = 1e-07$ | $g = 2$ |

**Figure 4.4** Histograms of Monte Carlo and quasi Monte Carlo estimates after $10^4$ independent runs. The optimal parameter is $	heta^* \approx -0.4841$.

```
$$\epsilon(k) = \epsilon(0) + \omega k \quad \text{(mod 1)}.$
```

Subject to the conditions on the parameter $\omega$ and function $y: \mathbb{R} \to \mathbb{R}$, we have the Law of Large Numbers Numbers:

```
$$\lim_{N \to \infty} \frac{1}{N} \sum_{k=1}^{N} y(k) = \int_{0}^{1} y(r) dr.$
```

This is known as the Equilibrium Theorem (see [33], and [149, p. 87] for more history). The quasi Monte Carlo literature contains more sophisticated techniques to define wellbehaved "probing sequences.\
Sinusoids and functions are used in this chapter for simplicity (and because of my ignorance of the substantial literature on pseudorandomness). An expert in quasi Monte Carlo methods might suggest a two-step process in translating a QSA ODE to discrete time:

+   (1) A discrete-time approximation of the QSA ODE in discrete time.
(2) Careful selection of the probing sequence in discrete time.

I hope that step 2 can be avoided, as long as we are careful with step 1. We are not bound to Euler here: Remember that Matlab's ode45 is based on more efficient numerical methods.

# 4.5.2 System Identification

The next example illustrating QSA techniques concerns system identification. Consider the nonlinear space model in continuous

```
$$\dot{x}_{t_i} = f(x_{t_i}, u_{t_i}) + d_{t_i}, \quad x_0 \ \text{given}$ \ny_{t_i} = g(x_{t_i}, u_{t_i}) + w_{t_i}$ $$
```

with state $x_t \in \mathbb{R}^n$ and input $u_t \in \mathbb{R}^m$, and the output taken scalar for simplicity: $y_t \in \mathbb{R}$. The noise $\{d_t\}$ and $\{w_t\}$ are known respectively as the disturbance and measurement

The functions $f$ and $g$ that define dynamics are not known. We are given observations of the input and output (and possibly the state), and we want to find a model that fits these measurements. One is to propose a parameterized family of models:

```
$$\dot{x}_t^\theta = f(x_t^\theta, u_t; \theta), \quad x_0^\theta = x_0$\nny_t^\theta = g(x_t^\theta, u_t; \theta).$$
```