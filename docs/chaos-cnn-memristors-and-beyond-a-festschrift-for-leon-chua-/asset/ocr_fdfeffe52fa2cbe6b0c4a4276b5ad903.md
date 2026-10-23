![](bbox=[0.24, 0.09, 0.75, 0.26])

Fig. 1. Quasi-periodic regime in Eq. (6) obtained by numerical simulation. Parameters: a = 0.2, ω = π and μ = 1.8. Time step: δt = 0.001 s.

Mark Levi investigated rotation numbers of periodic solutions to the driven van der Pol equation [12], thus enabling the topological analysis which was later applied to chaotic attractors.

Using Liénard’s [13] familiar nonlinear transformation (cf. [14]), the periodically forced van der Pol oscillator

```
ẍ − μ ẋ (1 − x²) + x = a cos bt,
```

can be written in the form

```
ε ẋ = x − 1/3 x³ − y
ẏ = x + a cos bt,
```

where ε = 1/μ. Cartwright and Littlewood considered Eq. (2) under the condition of very small values of ε. Later it was shown that such an equation can lead to chaotic behaviors [15].

# 3. A Related Prototype

The matter discussed in this section was mostly extracted from a textbook the first author wrote in the early 1980’s but which was never published. With the help of Reimara Rössler, we found again the first draft of this textbook and we are preparing a publication of it, more than thirty years after its writing. As we will show in this chapter, Otto’s views remain original even when they are considered after a so long time (says Christophe). In what follows, we preserved the content but not the writing.

The purpose was to provide a dynamical system producing a toroidal chaos governed by a mechanism simpler than the process underlying the

van der Pol equation. Let us start from the two-dimensional system

```
ẋ = x/r f(x) + ω y
ẏ = − ω x + y/r f(x)
```

in Cartesian coordinates which may be rewritten as the following two-dimensional system

```
ṙ = 1/2 (2x dx + 2y dy)/√(x²+y²) = (x²/r + y²/r)·f(r) + (ωxy − ωxy)/r = r·f(r)
θ̇ = 1.
```

in polar coordinates. This system defines the evolution of the radius which is associated with a constant angular velocity. Using f(r) = 1, system (3) can be rewritten as the two-variable autonomous system

```
ẋ = x/r + ω y
ẏ = − ω x + y/r,
```

which is an expansive system with a single fixed point which is an unstable focus. To prevent this system from diverging to infinity, a second condition is added to bound the radius. One of the simplest ways is to use, for example,

```
(r − 1) mod (1 + a cos π ω t).
```