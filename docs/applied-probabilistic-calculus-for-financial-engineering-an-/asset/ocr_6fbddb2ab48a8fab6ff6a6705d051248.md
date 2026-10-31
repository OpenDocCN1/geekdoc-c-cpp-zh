```
> ##
> ## Arithmetic Brownian motion
> set.seed(1234)
> X <- ABM(N=1000, M=50)
> plot(X, plot.type="single")
```

> # Output: Figure 2.11 Sim.DiffProc-8

![](bbox=[0.1, 0.33, 0.9, 0.6])

Figure 2.11 Sim.DiffProc-8 (Ordinates are arbitrary)

```
> lines(as.vector(time(X)), rowMeans(X), col="red")
> ##
```

> # Output: Figure 2.12 Sim.DiffProc-9

![](bbox=[0.1, 0.86, 0.9, 1.0])

Figure 2.12 Sim.DiffProc-9 (Ordinates are arbitrary)

```
> ##
> par(op)
>
```