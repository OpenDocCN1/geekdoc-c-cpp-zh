# Control Crush Course

![](bbox=[0.176, 0.078, 0.823, 0.237])

![](bbox=[0.176, 0.291, 0.823, 0.389])

toward the origin, and it is intuitively “stable.” The plot on the right is a simulation of the linear model subject to a “white noise” disturbance:

```
$X(k+1) = FX(k) + N(k+1), \quad k \geq 0.$
```

See the discussion that follows (7.46) for details of the disturbance process $N$,

**Example 2.4.2 (Frictionless Pendulum)** *The frictionless pendulum* illustrated on the left-hand side of Figure 2.8 is a favorite example in physics and undergraduate control courses. It is based on simplifying assumptions:

+   - There is no friction or air resistance.
- The rod on which the bob swings is rigid and without mass.
- The bob has mass, but only in two dimensions.
- The gravitational field is uniform.
- “F = MA” (apply classical mechanics, subject to the foregoing).

A nonlinear state model is obtained in which $x_1$ is the angular position $	heta$, and $x_2$ its derivative:

```
$$\frac{dx}{dt} = f(x) = \left[egin{matrix} x_2 \ -g\sin(x_1) \end{matrix}\right]. (2.49)$
```

Shown on the right-hand side of Figure 2.8 are trajectories of $x_1$, and two equilibria. An inspection of state trajectories shown on the right-hand side of Figure 2.8 reveals that the equilibrium $x^e = (\frac{\pi}{2})$ is not stable in any sense, which agrees with physical intuition (the pendulum is sitting upright in this case). Trajectories that begin near the equilibrium $x^e = 0$ will remain near this equilibrium thereafter.