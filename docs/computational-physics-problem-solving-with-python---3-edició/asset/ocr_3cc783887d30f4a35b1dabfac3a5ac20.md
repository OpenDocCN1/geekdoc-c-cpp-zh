![](bbox=[0.15, 0.12, 0.68, 0.33])

Figure 15.1 (a) A pendulum of length l driven through resistive air (dotted arcs) by an external sinusoidal torque (semicircle). The strength of the external torque is given by f and that of air resistance by α. (b) A double pendulum with neither air resistance nor a driving force. In both cases there is a gravitational torque.

Equation 15.2 is a second-order time-dependent nonlinear differential equation. Its nonlinearity arises from the sin θ, as opposed to the θ, dependence of the gravitational torque. The parameter ω₀ is the natural frequency of the system arising from the restoring torque, α is a measure of the strength of friction, and f is a measure of the strength of the driving torque. In our standard ODE form, d y / d t = f (Chapter 8), we have two simultaneous first-order equations:

```
d y^(0) / d t = y^(1),  (15.4)
```

```
d y^(1) / d t = - ω₀² sin y^(0) - α y^(1) + f cos ω t ,
```

```
y^(0) = θ(t),    y^(1) = d θ(t) / d t .  (15.5)
```

# 15.1.1

# Free Pendulum Oscillations

If we ignore friction and external torques, Newton’s law (15.2) takes the simple, yet still nonlinear, form

```
d² θ / d t² = - ω₀² sin θ .  (15.6)
```

If the displacements are small, we can approximate sin θ by θ and obtain the linear equation of simple harmonic motion with frequency ω₀:

```
d² θ / d t² ≈ - ω₀² θ  ⇒  θ(t) = θ₀ sin(ω₀ t + φ) .  (15.7)
```