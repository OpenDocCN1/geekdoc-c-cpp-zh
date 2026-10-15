![](bbox=[0.371, 0.092, 0.66, 0.386])

Figure 6.4: Convergence profile of IDP, showing the deviation from the optimum I = 6226.047 with η = 0.65 and γ = 0.95 using the number of randomly chosen points R as parameter

The computation time for 30 passes with 80 stages was 200.5 s. The doubling of the number of time stages did not slow the convergence rate at all, but the computation time was doubled.

The use of a smaller number of stages, namely, P = 30 stages, gave I = 6226.543. By using the same parameters, the computation time was 80.6 s for 30 passes.

Since the state equation is linear and the performance index is quadratic, the problem is ideally suited for solution by the use of Pontryagin’s maximum principle, where the optimal control policy is obtained by minimizing the Hamiltonian. This leads to the (n × n) Riccati equation [6]

$$\frac{d\mathbf{J}}{dt}+\mathbf{J}\mathbf{A}+\mathbf{A}^{T}\mathbf{J}-0.5\mathbf{J}\mathbf{J}+2\mathbf{I}=0 \tag{6.44}$$

with the final condition

$$\mathbf{J}(t_f)=20\mathbf{I}. \tag{6.45}$$

The Riccati equation is solved backwards, yielding the symmetric matrix J, which is stored at the end of each integration time step. Then the optimal control policy is obtained by integrating the state equation forward in time and using the stored values of J

$$\mathbf{u}=-0.5\mathbf{J}\mathbf{x}(t). \tag{6.46}$$

To ensure sufficient accuracy and stability in the integration we used the integration subroutine DVERK [4] with local error tolerance of 10⁻⁴. The accuracy of the