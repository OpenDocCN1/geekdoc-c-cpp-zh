choice? By taking a single grid point, i.e., N = 1, and only R = 15 random points, while allowing 20 iterations per pass, we solved the above optimal control problem for different values of the region contraction factor γ for different values of the region restoration factor η.

As is seen in Table 6.6, the success rate is almost 100% if the restoration factor is between 0.70 and 0.85. Of the 80 cases, only two yielded values different from the global optimum of 21.7572, where a maximum of 20 passes was allowed. When the restoration factor was 0.90, the region size did not shrink sufficiently fast to yield convergence to six figures in 20 passes. The use of the multi-pass method is a good means of keeping the number of candidates for control small and still providing accurate convergence. This is especially important when we consider systems of higher dimension.

# 6.3.1 Nonlinear two-stage CSTR system

Let us consider a very difficult optimal control problem that arose from trying to get a good initial control policy for a time-delay system [8]. The system consists of a series of two CSTRs, where there is a transportation delay τ = 0.1 from the first tank to the second. This system was first investigated by Oh and Luus [11] and is described in greater detail in Chapter 8. Here we use a truncated Taylor series expansion for the time delay terms according to Mutharasan and Luus [9], to give a nondelay approximation

```
dx₁/dt = f₁  (6.28)

dx₂/dt = f₂  (6.29)

dx₃/dt = x₁ − x₃ − τ f₁ − R₂ + 0.25  (6.30)

dx₄/dt = x₂ − 2 x₄ − u₂[x₄ + 0.25] − τ f₂ + r₂ − 0.25  (6.31)

dx₅/dt = x₁² + x₂² + x₃² + x₄² + 0.1(u₁² + u₂²)  (6.32)
```

where

```
f₁ = 0.5 − x₁ − R₁  (6.33)

f₂ = −2[x₂ + 0.25] − u₁[x₂ + 0.25] + R₁  (6.34)

R₁ = [x₁ + 0.5] exp(25 x₂ / (x₂ + 2))  (6.35)

R₂ = [x₃ + 0.25] exp(25 x₄ / (x₄ + 2)).  (6.36)
```

The state variables x₁ and x₃ are normalized concentration variables in tanks 1 and 2, respectively, and x₂ and x₄ are normalized temperature variables in tanks 1 and