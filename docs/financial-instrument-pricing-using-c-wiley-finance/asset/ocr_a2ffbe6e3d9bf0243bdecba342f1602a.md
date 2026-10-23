Horizontal Method of Lines (Rothe’s Method): we can reduce an initial boundary value problem to a TPBVP by discretising in the t direction (Ladyženskaja, Solonnikov and Ural’ceva, 1988, p. 241; Meyer, 2015, p. 61; Rothe, 1930). For example, we can discretise equation (20.13) in time by the fully implicit method (BTCS) (for notation, see Chapter 13) to produce the system of second-order ordinary differential equations:

```
− (u^{n+1} − u^{n})/Δt + σ(x, t_{n+1}) d²u^{n+1}/dx² + μ(x, t_{n+1}) du^{n+1}/dx + b(x, t_{n+1}) u^{n+1} = f(x, t_{n+1}),
0 ≤ n ≤ N − 1.
```

In this case we use first-order backward divided differences to approximate the time derivative (another choice is the second-order Crank–Nicolson method based on centred differencing). We augment these ODEs with appropriate boundary and initial conditions.

+   Rothe’s method is useful for problems with discontinuous payoffs, early-exercise features and problems with jumps and solutions of the Black–Scholes equation that change rapidly with respect to the underlying S at any given time (Meyer, 2015).

+   The example shows how some finite difference methods lead to non-monotone schemes and how they can be made monotone by applying the exponential fitting method (Duffy, 1980, 2006). For a detailed discussion of numerical methods for two-point boundary value problems, see Keller (1968).

# 20.7.1 The Example

Our aim is to approximate the initial boundary value problem (20.14)–(20.16) by finite difference schemes. We first define some notation. To this end, we divide the interval [A, B] into J equal subintervals:

```
A = x₀ < x₁ < … < x_J = B
```

and we assume for convenience that the mesh points {x_j}_{j=0}^J are equidistant, that is:

```
x_j = x_{j−1} + h,   j = 1, …, J (h = (B − A)/J).
```

Furthermore, we divide the interval [0, T] into N equal subintervals:

```
0 = t₀ < t₁ < … < t_N = T
```