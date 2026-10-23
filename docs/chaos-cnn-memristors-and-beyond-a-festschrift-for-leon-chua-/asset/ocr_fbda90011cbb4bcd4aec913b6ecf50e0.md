![](bbox=[0.09, 0.08, 0.49, 0.44])

Fig. 21. Experimental time series plot (Eq. (34)) of the drive x(t) (blue) and the response y(t) (yellow), (a) anticipatory synchronization for τ₂ ≈ 3.1007, (b) complete synchronization for τ₂ ≈ 2.8022 and (c) lag synchronization for τ₂ = 2.5; vertical scale 5V/div., horizontal scale 1 ms.

![](bbox=[0.09, 0.58, 0.49, 0.81])

Fig. 22. Experimental time series plots of the drive x(t) (blue) and the response y(t) (yellow) (a) inverse anticipatory synchronization, (b) inverse complete synchronization and (c) inverse lag synchronization, see Eq. (34).

where a and b are positive parameters and τ is the time delay [36]. The function F(x) is taken to be the symmetric piecewise linear function Eq. (32).

The coupled electronic circuit investigated here is shown in Fig. 23 as a block diagram. The individual time-delay units have a ring structure and comprise of a diode based nonlinear device unit (ND), a variable time-delay unit (DELAY) along with an integrator (R₀C₀) unit. The block diagram also contains a differential amplifier circuit (A) with a gain ε = R_f/R used to find the difference between the two voltage signals U1 and U2. By changing the feedback resistance (R_f), the coupling parameter ε can be varied. We have fixed the same circuit parameter values of as in the above studies and demonstrate here the existence of chaotic phase synchronization (CPS) as a function of the coupling strength ε in both chaotic and hyperchaotic regimes for suitable values of the delay time τ.

Existence of CPS can now be demonstrated using the framework of localized sets in the chaotic regime. The sets obtained by sampling the time series of one of the systems whenever a maximum occurs in the other one are plotted along with the chaotic attractor of the same system for the delay time τ = 1.33 experimentally in Fig. 24(i). The sets distributed over the entire attractor of both the drive [Figs. 24(a)i] and the response [Figs. 24(b)i] systems for the coupling strength ε = 0.3 indicate that the time-delay systems evolve independently. The sets that are localized on the chaotic attractor of both the drive [Figs. 24(c)i] and the response [Figs. 24(d)i] systems for the coupling strength ε = 0.9 correspond to a perfect locking of the phases of both circuits, indicating CPS.

# 8.3. Zero-lag synchronization in coupled time-delay systems

In this section we have considered the following three coupled piecewise linear time-delay systems with threshold nonlinear function,

```
ẋ₁(t) = −βx₁(t) + αF[x₁(t − τ)] + C[x₂(t − τ) − 2x₁(t) + x₃(t − τ)],
ẋ₂(t) = −βx₂(t) + αF[x₂(t − τ)] + C[x₁(t − τ) − x₂(t)],
ẋ₃(t) = −βx₃(t) + αF[x₃(t − τ)] + C[x₁(t − τ) − x₃(t)], (36)
```

the parameter values are fixed as follows: β = 1.0, α = 1.2, τ = 6.0 and C is the coupling strength. The function F(x) is taken to be a symmetric piecewise linear function Eq. (32). We note that in contrast