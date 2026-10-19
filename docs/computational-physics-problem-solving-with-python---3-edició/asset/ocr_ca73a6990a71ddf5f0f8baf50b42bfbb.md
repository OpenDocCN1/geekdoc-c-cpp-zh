To impose the boundary condition at $x = b$, we again add a particular solution $U_b \phi_{N-1}(x)$ and substitute it into the weak form to obtain

```
$b'_i = b_i - A_{i,N-1} U_b \ , \quad i = 1, ..., N-1 \ , \quad b'_N = U_b \ . \qquad (23.25)$
```

So now we need to solve the linear equations $\mathbf{A} \mathbf{y} = \mathbf{b}'$. For 1D problems, 100–1000 equations are common, while for 3D problems there may be millions. Because the number of calculations varies approximately as $N^2$, it is important to utilize an efficient and accurate algorithm, because otherwise the round-off error can easily dominate the solution.

# 23.5

# 1D FEM Implementation and Exercises

In Listing 23.1, we give our program LaplaceFEM_1D.py that determines the 1D FEM solution, and in Figure 23.3 we show that solution. We see on the left of the figure that three elements do not provide even visual agreement with the analytic result, whereas $N = 11$ elements do.

+   1. Examine the FEM solution for the choice of parameters

```
$a = 0 \ , \quad b = 1 \ , \quad U_a = 0 \ , \quad U_b = 1 \ . \qquad (23.26)$
```

+   2. Generate your own triangulation by assigning explicit $x$ values at the nodes over the interval $[0, 1]$.

+   3. Start with $N = 3$ and solve the equations for $N$ values up to 1000.

+   4. Examine the stiffness matrix $\mathbf{A}$ and ensure that it is triangular.

+   5. Verify that the integrations used to compute the load vector $\mathbf{b}$ are accurate.

+   6. Verify that the solution of the linear equation $\mathbf{A} \mathbf{y} = \mathbf{b}$ is correct.

+   7. Plot the numerical solution for $U(x)$ for $N = 10, 100,$ and $1000,$ and compare with the analytic solution.

![](bbox=[0.21, 0.65, 0.43, 0.825])

Figure 23.3 Exact (line) vs. FEM solution (points) for the two-plate problem for $N = 3$ and $N = 11$ finite elements ($N = 3$ displaced upwards for clarity). On this scale, the $N = 11$ solution IS identical to the exact one.