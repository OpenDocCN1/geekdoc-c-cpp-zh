A variation of this method, *successive over-relaxation*, increases the speed at which the residuals approach zero via an amplifying factor ω:

```
ν^x_{i,j} = ν*_{i,j} + ω r_{i,j}  (SOR) .  (25.20)
```

The standard relaxation algorithm (25.18) is obtained with ω = 1, an accelerated convergence (*over-relaxation*) is obtained with ω ≥ 1, and *underrelaxation* occurs for ω < 1. Values ω > 2 are found to lead to numerical instabilities. Although a detailed analysis of the algorithm is necessary to predict the optimal value for ω, we suggest that you test different values for ω to see which one provides the fastest convergence for your problem.

# 25.2.3
Successive Overrelaxation Implementation

+   1. Modify the program Beam.py, or write your own, to solve the Navier–Stokes equation for the velocity of a fluid in a 2D flow. Represent the x and y components of the velocity by the arrays vx[Nx,Ny] and vy[Nx,Ny].
+   2. Specialize your solution to the rectangular domain and boundary conditions indicated in Figure 25.2.
+   3. Use of the following parameter values,
+   ν = 1 m²/s ,  ρ = 10³ kg/m³ ,  (flow parameters) ,
+   Nx = 400 ,  Ny = 40 ,  h = 1 ,  (grid parameters) ,
+   leads to the analytic solution
+   ∂P/∂x = -12 ,  ∂P/∂y = 0 ,  ν^x = 3j/20 (1 - j/40) ,  ν^y = 0 .  (25.21)
+   4. For the relaxation method, output the iteration number and the computed ν^x and then compare the analytic and numeric results.
+   5. Repeat the calculation and see if SOR speeds up the convergence.

# 25.3
2D Flow over a Beam

Now that the comparison with an analytic solution has shown that our CFD simulation works, we return to determining if the beam in Figure 25.1 might produce a good resting place for salmon. While we have no analytic solution with which to compare, our canoeing and fishing adventures have taught us that *standing waves* with fish in them are often formed behind rocks in streams, and so we expect there will be a standing wave formed behind the beam.