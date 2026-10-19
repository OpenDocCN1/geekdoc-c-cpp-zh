# 14.5.3

# Feigenbaum Constants (Exploration)

Feigenbaum discovered that the sequence of μ_k values (14.17) at which bifurcations occur follows a regular pattern (Feigenbaum, 1979). Specifically, the μ values converge geometrically when expressed in terms of the distance between bifurcations δ:

```
μ_k → μ_∞ − c / δ^k ,
```

```
δ = lim_{k→∞} (μ_k − μ_{k−1}) / (μ_{k+1} − μ_k) .
```

Use your sequence of μ_k values to determine the constants in (14.18) and compare them to those found by Feigenbaum:

```
μ_∞ ≈ 3.569 95 ,   c ≈ 2.637 ,   δ ≈ 4.6692 .
```

Amazingly, the value of the Feigenbaum constant δ is universal for all second-order maps.

# 14.6

# Logistic Map Random Numbers (Exploration) ⊙

Although we have emphasized that chaos, with its short-term predictability, is different from random, with has no predictability, it is nevertheless possible for the logistic map in the chaotic region (μ ≥ 4) to be used to generate pseudo random numbers (Phatak and Rao, 1995). This is carried out in two steps:

```
x_{i+1} ≈ 4 x_i (1 − x_i) ,
```

```
y_i = (1/π) cos^{−1} (1 − 2 x_i) .
```

Although successive x_i's are correlated, if the population for every sixth generation or so is examined, the correlation is effectively gone and pseudorandom numbers result. To make the sequence more uniform, the trigonometric transformation is then used.

# Exercise Use the random-number tests discussed in Chapter 4, or an actual Monte Carlo simulation, to test this claim.

# 14.7

# Other Maps (Exploration)

Bifurcations and chaos are characteristic properties of nonlinear systems. Yet systems can be nonlinear in a number of ways. The table below lists four maps that generate x_i sequences containing bifurcations.