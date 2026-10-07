# Unsteady, Non-Linear, and Chaotic Systems

The combined convergence test (1.29c) $\equiv$ (4.412a):

```
$$\frac{a_{n+1}}{a_n} = 1 - \frac{\delta}{n} + O(\left(\frac{1}{n^2}\right); \quad g=1, \quad (4.412a, b)$
```

implies (4.412b) has radius of convergence unity; (ii/iii) they converge absolutely (uniformly) for variable $|z| < 1-\epsilon$ with $\\delta < 1-\epsilon < 1$; (iv) they diverge (1.295b) at $z=1$. The variable is $z=q^2$ in (4.403b) and $z=1/q^2$ in (4.404b).

Thus the period of the circulatory (oscillatory) motion [problem 131] of the circular pendulum is exceeded exactly by the series (4.403b)[4.404b]: (i) converges absolutely (sections 1.21.3-1.21.4), that is, the series of converges if $q^2 > 1$ ($q^2 < 1$) corresponding to (4.403a)[4.404a], and (ii) diverges (sections 1.21.5-1.21.6), that is, independent of the value of $q$, if $q^2 > 1+\delta$ with $\delta > 0$ ($q^2 < 1+\delta$). The two series coincide on boundary of convergence (4.413a) where $0 < \epsilon < 1$. This coincide (4.413b) which corresponds to the stopage at the top (4.390a) that takes an infinite time (4.390b).

```
$q=1; \quad \theta_0=2\omega_0, \quad D=A(1)=1+\sum_{n=m}^{\infty}(a_n)^2=\infty. \quad (4.413a-c)$
```

In the stopage (4.413a-c) the period of the oscillation (4.414a) is twice (4.414c) the period of the circulatory (4.414b):

```
$$\frac{2D}{\omega_0} \frac{4D}{\theta_0} = \frac{\tau_1}{\theta_0} \frac{2D}{\omega_0}: \quad \tau_2=2\tau_1, \quad (4.414a-c)$
```

because a complete oscillation (circulatory) goes twice (once) around the circle. The period of the circulatory (4.403a,b;4.405)[4.404a,b;4.406] circular pendulum motion increases for lower (higher) angular velocity at the top, and they coincide (4.414a-c) in the case of stopage at the top, when both are infinite (4.414a,b) in the ratio (4.414). The non-linear motion of the circular pendulum has been considered in the absence of damping (subsections 4.79-4.7.14) and is extended next (subsections 4.715-4.717) to quadratic damping.

# 4.716 Harmonic Oscillator with Non-Linear Damping

In the case of the homogeneous dynamo (subsection 4.7.2), there is no oscillation because the differential equation (4.343a) is of first order with real coefficients. An oscillator will for a second-order system with a linear restoring force and non-linear damping (4.315a):

```
$$\ddot{x}+h(\dot{x})+\\omega_0^2x=0; \quad v=\dot{x}, \quad \dot{v}=-h(v)-\omegaomega_0\dot{x}, \quad (4.415a-c)$
```