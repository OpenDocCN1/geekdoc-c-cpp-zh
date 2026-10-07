# Unsteady, Non-linear, and Chaotic Systems

and leads (problem 91) to the equation of motion (4.84d) in the original time:

```
$$\ddot{x} + \omega_0^2[1+2h\cos(\omega, t)]x = 0. \quad (4.88)$
```

The latter corresponds to a Mathieu **equation (1873) (4.89):**

```
$$\frac{d^2w}{d\theta^2} + [a-2q\cos(2\theta)]w = 0, \quad (4.89)$
```

with: (i) independent variable (4.90a); (ii) dependent variable (4.90d); and (iii) parameters (4.90b, c):

```
$$\theta = \frac{\omega,t}{2}, \quad a = \left(\frac{2\omega_0}{\omega}\right)^2, \quad q = -h\left(\frac{2\omega_0}{\omega}\right)^3, \quad w(\theta) \equiv x(t). \quad (4.90a–d)$
```

The general properties of linear differential equations of second order with periodic coefficients (subsections 4.3.3–4.3.6) are used to solve (subsections 4.3.7–4.3.12) the Mathieu equation (4.89) exactly; these are illustrated by approximate solutions of the harmonic oscillator with vibrating support (4.88) without (with) damping [subsections 4.3.13–4.3.15 (4.3.16–4.3.18)]. An example is a pendulum with support oscillating vertically (subsections 4.3.19–4.3.20).

# 4.3.3 Linear Differential Equation with Periodic Coefficients (Floquet 1883)

The Mathieu equation (4.89) is a particular case of the unforced linear differential equation (1.34b; 1.36c) $\equiv$ (4.91b) with periodic coefficients

```
$$A_n(t+\tau) = A_n(t): \quad \sum_{n=0}^N A_n(t)\frac{d^nx}{dt^n} = 0, \quad (4.91a, b)$
```

considered next (in the section 9.3) for order two (order N). In the secondorder case:

```
$$N=2: \quad A_2(t)\ddot{x}(t) + A_1(t)\dot{x}(t) + A_0(t)x(t) = 0, \quad (4.92a, b)$
```

the general integral is a linear combination (1.36b) $\equiv$ (4.92d) of linearly independent particular integrals with the non-zero Wronskian (1.40c) $\equiv$ (4.92c):

```
$$0 \neq W(x_1x_2) = x_1\dot{x}_2 - \dot{x}_1x_2: \quad x(t) = C_1x_1(t) + C_2x_2(t), \quad (4.92c, d)$
```