# 15

# Continuous Nonlinear Dynamics

In Chapter 14, we developed the logistic map and predator–prey models as a means to understand how biological populations achieve dynamic equilibrium. In this chapter, we explore the driven realistic pendulum, a continuous system chaos that can support chaotic behavior. In Chapter 8, we have already seen how useful our tools are at solving nonlinear equations. Our emphasis now is on exploring chaos and on the usefulness of phase space in displaying the simplicity underlying complex behavior.

# 15.1

# Chaotic Pendulum

Problem The plane pendulum is a classic subject for physics. However, it has most often been studied assuming small angle displacements, which is a good approximation only for very large grandfather clocks. However, when the pendulum is driven and the displacements get large, the motion becomes too complicated for analytic solution. Your problem is to compute the motion of a driven pendulum with large displacements, to ensure that your calculation is reliable and sensitive, and then to search for the simplicity that may underly complexity.

What we call a chaotic pendulum is just a pendulum with friction and a driving torque (Figure 15.1a), but without the assumption of small deflection angle. Newton’s laws of rotational motion tell us that the sum of the gravitational torque −mgl sin θ, the frictional torque −β θ̇, and the external torque τ₀ cos ωt equals the moment of inertia of the pendulum times its angular acceleration (Rasband, 1990):

```
I d²θ/dt² = −mgl sin θ − β dθ/dt + τ₀ cos ωt   (15.1)
```

```
⇒ d²θ/dt² = −ω₀² sin θ − α dθ/dt + f cos ωt ,   (15.2)
```

```
ω₀ = mgl/I ,   α = β/I ,   f = τ₀/I .   (15.3)
```