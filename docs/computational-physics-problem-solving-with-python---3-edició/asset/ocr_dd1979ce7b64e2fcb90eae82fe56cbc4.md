![](bbox=[0.18, 0.15, 0.52, 0.31])

Figure 20.2 The algorithm for the heat equation in which the temperature at the location x = iΔx and time t = (j + 1)Δt is computed from the temperature values at three points of an earlier time. The nodes with white centers correspond to known initial and boundary conditions (the boundaries are placed artificially close for illustrative purposes).

As is often the case with PDEs, the algorithm is customized for the equation being solved and for the constraints imposed by the particular set of initial and boundary conditions. With only one row of times to start with, we use a forward-difference approximation for the time derivative of the temperature:

```
∂T(x,t)/∂t ≈ [T(x,t + Δt) − T(x,t)] / Δt .  (20.14)
```

Because we know the spatial variation of the temperature along the entire top row and the left and right sides, we are less constrained with the space derivative as with the time derivative. Consequently, as we did with the Laplace equation, we use the more accurate central-difference approximation for the space derivative:

```
∂²T(x,t)/∂x² ≈ [T(x + Δx,t) + T(x − Δx,t) − 2T(x,t)] / (Δx)² .  (20.15)
```

Substitution of these approximations into (20.4) yields the heat difference equation

```
[T(x,t + Δt) − T(x,t)] / Δt = K/(Cρ) [T(x + Δx,t) + T(x − Δx,t) − 2T(x,t)] / Δx² .  (20.16)
```

We reorder (20.16) into a form in which T can be stepped forward in t:

```
T_{i,j+1} = T_{i,j} + η [T_{i+1,j} + T_{i-1,j} − 2T_{i,j}] ,   η = KΔt / (CρΔx²) ,  (20.17)
```

where x = iΔx and t = jΔt. This algorithm is explicit because it provides a solution in terms of known values of the temperature. If we tried to solve for the temperature at all lattice sites in Figure 20.2 simultaneously, then we would have an implicit algorithm that requires us to solve equations involving unknown values of the temperature. We see that the temperature at space–time point (i, j + 1)