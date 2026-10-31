Thus, for x_A = 1, 0.75, 0.50, 0.25, 0, 1.5, and −0.5, the following R code segment would undertake the computation. The results follow, together with some graphic presentations of the results:

# In the R domain:

```
> muA <- -0.2
> sigmasqA <- -0.05
> muB <- -0.04
> sigmasqB <- -0.01
> sigA <- -0.2236
> sigB <- -0.1000
> sigAB <- -0.0038
> rhoAB <- -0.17
>
> A <- c(1, 0.75, 0.50, 0.25, 0, 1.5, -0.5)
> B <- c(0, 0.25, 0.50, 0.75, 1, -0.5, 1.5)
> mu <- A*muA + B*muB
> var <- A*A*sigA*sigA + B*B*sigB*sigB + 2*A*B*sigAB
> sigma <- sqrt(var)
>
> mu
[1] 0.20 0.16 0.12 0.08 0.04 0.28 -0.04
>
> sigma
[1] 0.2236000  0.1652976  0.1144519  0.0855851
[5] 0.1000000  0.3474092  0.2017405
>
> plot(A, sigma) # Outputting: Figure 3.4
> RER <- mu/sigma
> RER
[1] 0.8944544 0.9679513 1.0484753 0.9347421
[5] 0.4000000 0.8059660 -0.1982745
>
> plot(A, RER) # Outputting: Figure 3.5
```

# 3.2.3.2 Evaluating a Portfolio

Consider an initial investment I₀ in a portfolio of assets A and B, for which

+   a) the return is to be given by (3.23),