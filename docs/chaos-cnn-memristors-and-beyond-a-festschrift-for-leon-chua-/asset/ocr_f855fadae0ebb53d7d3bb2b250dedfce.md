from below, r is replaced with r − (1 + a cos πωt). The principle of modulation of the maximum value of the radius reached at each oscillation is shown in Fig. 1. These oscillations correspond to relaxation oscillations as introduced by van der Pol and Liénard.

System (6) corresponds to a particular linear combination of two periodic behaviors and, consequently, only quasi-periodic regimes are obtained. An example of them is shown in an x − y plane projection of the phase space. The toroidal structure appears squeezed in this plane. A first-return map, built as a first-return to the maxima of the radius, clearly shows the quasi-periodic nature of the regime, whose strong signature is an annular map (Fig. 2b).

Systems (6) and (5) cannot produce more complex behaviors due their linear character. Chaotic behaviors can only be expected when a nonlinearly growing radius is involved. We thus introduced nonlinear terms in Eq. (5) to obtain the following equation

```
\begin{cases}
\dot{x}=\mu\dfrac{x(1-y)}{r}+\omega y\\
\dot{y}=-\omega x+\mu\dfrac{y(1-x)}{r}
\end{cases}\tag{7}
```

where (r − 1) is mod(1 + a cos πωt) as in the previous example. The behavior is now chaotic as evidenced by the first-return map built from the maxima of the radius (Fig. 3(b)). The map looks like a layered annular structure, thus confirming that the behavior is toroidal chaos. Better characterizing such toroidal chaos remains a great challenge. This apparently does not result from the emergence of a folding-in in a quasi-periodic regime. The stiff dynamics induced by the “mod( )” function squeezes the attractor onto itself, inducing some domains of the phase space (at the upper left corner of the return map, Fig. 3(b)) where the different trajectories cannot be distinguished, rendering the dynamics non-observable. The simplicity of the mechanism used to produce this behavior has an advantage: it is easy to understand; but the resulting dynamics is quite hard to fully characterize.

An “avatar” of Eq. (7) can be written in a slightly different way. The principle underlying the construction of this new model is the same as in the two previous examples but the equations are simpler

![](bbox=[0.56, 0.096, 0.898, 0.353])

(a) Numerical simulation of Eq. (5)

![](bbox=[0.56, 0.398, 0.898, 0.647])

(b) The corresponding first-return map

Fig. 2. Quasi-periodic regime solution to Eq. (6), or equivalently to Eq. (5), obtained by numerical simulations. The first-return map is built as a return map to the maxima of radius r_max. Parameters: a = 0.2 and ω = π/4. Initial conditions: x₀ = 1 and y₀ = 0.

since there are no longer any fractional terms

```
\begin{cases}
\dot{x}=\mu x(1-y)-\omega y\\
\dot{y}=\omega x+\mu y(1-x)
\end{cases}\tag{8}
```

These equations with y as before produce the chaotic regimes shown in Fig. 4. It is far more difficult to show that this chaotic behavior has a toroidal character. In fact it has, because the first-return map is basically a closed loop with