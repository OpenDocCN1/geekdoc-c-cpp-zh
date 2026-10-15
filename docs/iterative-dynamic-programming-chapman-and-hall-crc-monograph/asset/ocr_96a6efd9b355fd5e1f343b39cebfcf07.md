![](bbox=[0.35, 0.08, 0.62, 0.38])

Figure 10.14: Optimal control policy, consisting of 13 stages, for Yeo’s problem, giving I = 0.11928, obtained by using initially 25 stages

# 10.4 Nonlinear two-stage CSTR problem

Let us now consider the two-stage CSTR system used for optimal control studies by Edgar and Lapidus [4], Luus [8], Nishida et al. [15], Rosen and Luus [17], Dadebo and McAuley [3], and by Luus et al. [14]. The system is described by

```
dx₁/dt = -3x₁ + g₁(x)  (10.41)
```

```
dx₂/dt = -11.1558x₂ + g₁(x) - 8.1558(x₂ + 0.1592)u₁  (10.42)
```

```
dx₃/dt = 1.5(0.5x₁ - x₃) + g₂(x)  (10.43)
```

```
dx₄/dt = 0.75x₂ - 4.9385x₄ + g₂(x) - 3.4385(x₄ + 0.122)u₂  (10.44)
```

where the reaction term in the first tank is given by

```
g₁(x) = 1.5 × 10⁷(0.5251 - x₁)exp(-10/(x₂ + 0.6932)) - 1.5 × 10¹⁰(0.4748 + x₁)exp(-15/(x₂ + 0.6932)) - 1.4280  (10.45)
```