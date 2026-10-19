# 8.9

# Extensions: Nonlinear Resonances, Beats, Friction

**Problem**  So far our oscillations have been rather simple. We have ignored friction and have assumed that there are no external forces (hands) influencing the system’s natural oscillations. Determine

+   1. How the oscillations change when friction is included?
+   2. How the resonances and beats of nonlinear oscillators differ from those of linear oscillators?
+   3. How introducing friction affects resonances?

# 8.9.1

# Friction (Model)

The world is full of friction, and not all of it is bad. For while friction makes it harder to pedal a bike through the wind, it also lets you walk on ice, and generally adds stability to dynamical systems. The simplest models for frictional force are called *static, kinetic,* and *viscous* friction:

$F_f^{(\mathrm{static})} \leq -\mu_s N, \qquad F_f^{(\mathrm{kinetic})}=-\mu_k N\frac{v}{|v|}, \qquad F_f^{(\mathrm{viscous})}=-bv. \tag{8.45}$

Here $N$ is the *normal force* on the object under consideration, $\mu$ and $b$ are parameters, and $v$ is the velocity. This model for static friction is appropriate for objects at rest, while the model for kinetic friction is appropriate for an object sliding on a dry surface. If the surface is lubricated, or if the object is moving through a viscous medium, then a frictional force dependent on velocity is a better model.

+   1. Extend your harmonic oscillator code to include the three types of friction in (8.45) and observe how the motion differs for each.
+   2. *Hint:* For the simulation with static plus kinetic friction, each time the oscillator has $v=0$ you need to check that the restoring force exceeds the static force of friction. If not, the oscillation must end at that instant. Check that your simulation terminates at nonzero $x$ values.
+   3. For your simulations with viscous friction, investigate the qualitative changes that occur for increasing $b$ values:

| Regime | Condition | Behavior |
|---|---|---|
| Underdamped | $b < 2m\omega_0$ | Oscillate within decaying envelope |
| Critically: | $b = 2m\omega_0$ | Nonoscillatory, finite decay time |
| Overdamped: | $b > 2m\omega_0$ | Nonoscillatory, infinite decay time |

5) The effect of air resistance on projectile motion is studied in Section 9.6.