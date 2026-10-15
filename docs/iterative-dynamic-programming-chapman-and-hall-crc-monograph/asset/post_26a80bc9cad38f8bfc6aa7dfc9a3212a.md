
![](img/06ae75163df4fdf5e1eec243d497d393_126_0.png)

*Figure 6.3: Convergence profile of IDP, showing the deviation from the optimum \(I = 6226.047\) with \(\eta = 0.70\) and \(\gamma = 0.95\) using the number of randomly chosen points \(R\) as parameter*

When \(\eta\) is increased to \(0.75\), the convergence rate is slightly slower than with \(\eta = 0.70\), as is shown in Figure 6.5.

## 6.4.2 Effect of the region contraction factor \(\gamma\)

As is the case for the region restoration factor \(\eta\), there is also a range for the region contraction factor \(\gamma\) for which reasonable rate of convergence is obtained with a small number of randomly chosen values for control. As is shown in Figure 6.6, when using \(\eta = 0.70\), there is a range \(0.93 < \gamma < 0.98\) for which convergence is obtained with the use of \(R = 3\).

## 6.4.3 Effect of the number of time stages

The optimal control policy obtained for this example is shown for typical control variables in Figure 6.7 and the state trajectories for some typical state variables are given in Figure 6.8. It is seen that the control policy is very smooth. The smoothness is increased by using a larger number of time stages, yielding a better approximation to the continuous control policy.

By doubling the number of time stages to \(P = 80\), we obtained the minimum performance index of \(I = 6225.568\). This result was obtained with the use of \(R = 3\) with \(\eta = 0.70\) and \(\gamma = 0.95\) in 24 passes, each consisting of 30 iterations as before.

![](img/06ae75163df4fdf5e1eec243d497d393_127_0.png)

*Figure 6.4: Convergence profile of IDP, showing the deviation from the optimum \(I = 6226.047\) with \(\eta = 0.65\) and \(\gamma = 0.95\) using the number of randomly chosen points \(R\) as parameter*

The computation time for 30 passes with 80 stages was 200.5 s. The doubling of the number of time stages did not slow the convergence rate at all, but the computation time was doubled.

The use of a smaller number of stages, namely, \(P = 30\) stages, gave \(I = 6226.543\). By using the same parameters, the computation time was 80.6 s for 30 passes.

Since the state equation is linear and the performance index is quadratic, the problem is ideally suited for solution by the use of Pontryagin’s maximum principle, where the optimal control policy is obtained by minimizing the Hamiltonian. This leads to the \(n \times n\) Riccati equation [6]

\[
\frac{d\mathbf{J}}{dt}+\mathbf{J}\mathbf{A}+\mathbf{A}^{T}\mathbf{J}-0.5\mathbf{J}\mathbf{J}+2\mathbf{I}=0 \tag{6.44}
\]

with the final condition

\[
\mathbf{J}(t_f)=20\mathbf{I}. \tag{6.45}
\]

The Riccati equation is solved backwards, yielding the symmetric matrix \(\mathbf{J}\), which is stored at the end of each integration time step. Then the optimal control policy is obtained by integrating the state equation forward in time and using the stored values of \(\mathbf{J}\)

\[
\mathbf{u}=-0.5\mathbf{J}\mathbf{x}(t). \tag{6.46}
\]

![](img/06ae75163df4fdf5e1eec243d497d393_128_0.png)

*Figure 6.5: Convergence profile of IDP, showing the deviation from the optimum \(I = 6226.047\) with \(\eta = 0.75\) and \(\gamma = 0.95\) using the number of randomly chosen points \(R\) as parameter*

To ensure sufficient accuracy and stability in the integration we used the integration subroutine DVERK [4] with local error tolerance of \(10^{-4}\). The accuracy of the solution depends on the number of time stages at which the feedback matrices are stored, but generally at least 100 time stages are required for a good approximation. Here we will illustrate the effect of the number of stages by taking a different number of stages. This also enables us to see the relationship of this standard method to the results obtained by IDP. The computations are very fast, even when 200 stages are used, as is shown in Table 6.8.

**Table 6.8: Values for the performance index obtained by solving the Riccati equation**

| Number of stages \(P\) | Performance index \(I\) | Computation time on PentiumII/350, s |
|---:|---:|---:|
| 30 | 6228.42 | 1.60 |
| 40 | 6227.13 | 1.92 |
| 80 | 6225.85 | 3.24 |
| 150 | 6225.53 | 5.76 |
| 200 | 6225.48 | 7.69 |

It is obvious that the solution of the Riccati equation here with \(n = 20\) is considerably faster than IDP, but for the same number of stages the use of IDP gives slightly better results. In the next chapter we will see that when piecewise linear control is used in IDP and the dimensionality increases, then the computation time for IDP becomes quite comparable to the computation time required to solve the Riccati equation.

![](img/06ae75163df4fdf5e1eec243d497d393_129_0.png)

*Figure 6.6: Convergence profile of IDP, showing the deviation from the optimum \(I = 6226.047\) with \(\eta = 0.70\) and 3 randomly chosen points, with region contraction factor \(\gamma\) used as a parameter*

When these values of the performance index are plotted against \(1/P^2\), as shown in Figure 6.9, the extrapolated value of the linear plots gives 6225.4, which is the same value as reported by Nagurka et al. [10]. It is quite clear that piecewise constant control is not the best choice when the control policy is very smooth. Rather than using a large number of stages with piecewise constant control, greater accuracy can be gained by using piecewise linear continuous control for such situations. The benefits in using piecewise linear continuous control for very high dimensional systems are illustrated in Chapter 7.

![](img/06ae75163df4fdf5e1eec243d497d393_130_0.png)

*Figure 6.7: Optimal control policy, showing the piecewise constant control for typical control variables with \(P = 40\) stages*

![](img/06ae75163df4fdf5e1eec243d497d393_130_1.png)

*Figure 6.8: State trajectories for typical state variables resulting from the optimal control policy*

- [8] Luus, R., Zhang, X., Hartig, F., and Keu, F.J.: “Use of piecewise linear control continuous optimal control for time-delay systems”, *Ind. Eng. Chem. Res.* **34** (1995), 4136-4139.
- [9] Mutharasan, R. and Luus, R.: “Analysis of time-delay systems by series approximation”, *AIChE J.* **21** (1975), 567-571.
- [10] Nagurka, M., Wang, S., and Yen, V.: “Solving linear quadratic optimal control problems by Chebychev-based state parameterization”, *Proceedings of the 1991 American Control Conference*, Boston, MA; American Control Council, IEEE Service Center: Piscataway, NJ, 1991; pp. 104-109.
- [11] Oh, S.H. and Luus, R.: “Optimal feedback control of time-delay systems”, *AIChE J.* **22** (1975), 144-147.
- [12] Rosen, O. and Luus, R.: “Evaluation of gradients for piecewise constant optimal control”, *Comput. Chem. Eng.* **15** (1991), 273-281.

where \(\phi\) is a positive definite function of \(\mathbf{x}\) at the given final time \(t_f\). The optimal control problem is to find the control policy \(\mathbf{u}(t)\) in the time interval \(0 \leq t \leq t_f\) so that the performance index is minimized.

Let us divide the given time interval \((0,t_f)\) into \(P\) subintervals \((0,t_1)\), \((t_1,t_2)\), \(\ldots,(t_k,t_{k+1}),\ldots,(t_{P-1},t_P)\), each of length \(L\), so that

\[
L=\frac{t_f}{P}.
\]

We seek a piecewise linear continuous control policy to minimize the performance index. Therefore, we calculate the control policy in the time interval \((t_k,t_{k+1})\) by the expression

\[
\mathbf{u}(t)=\mathbf{u}(k)+\frac{\mathbf{u}(k+1)-\mathbf{u}(k)}{L}(t-t_k)
\]

where \(\mathbf{u}(k)\) is the value of \(\mathbf{u}\) at the time \(t_k\) and \(\mathbf{u}(k+1)\) is the value of \(\mathbf{u}\) at time \(t_{k+1}\). The optimal control problem is now to find \(\mathbf{u}(k)\), \(k=0,1,2,\ldots,P\), inside the range specified by Eq. (7.2), so that the performance index in Eq. (7.3) is minimized. At the last stage we must determine both \(\mathbf{u}(P)\) and \(\mathbf{u}(P-1)\). This means that for the last stage we must determine \(2m\) values for the \(m\) control variables. For all the other stages there are only \(m\) values to be determined because of the continuity restriction.

## 7.3 Algorithm for IDP for piecewise linear control

Here we use IDP with a single grid point, i.e., \(N=1\), in a multi-pass fashion, where the region size is contracted by an amount \(\gamma\) after every iteration. After a specified number of iterations making up a pass, the region size is restored to a value \(\eta\) times the region size at the beginning of the pass to give the region size to be used in the subsequent pass. To illustrate this underlying logic in IDP, an algorithm is given to solve the optimal control problem as outlined in Eq. (7.1)–Eq. (7.4), where it is required to minimize the performance index in Eq. (7.3) with the use of piecewise linear control, as specified in Eq. (7.5) over \(P\) stages, each of the same length:

- 1. Divide the time interval \([0,t_f]\) into \(P\) time stages, each of length \(L\).
- 2. Choose the number of test values for \(\mathbf{u}\) denoted by \(R\), an initial control policy and the initial region size \(\mathbf{r}_{in}\); also choose the region contraction factor \(\gamma\) used after every iteration and the region restoration factor \(\eta\) used after every pass.
- 3. Choose the number of iterations to be used in every pass and the number of passes to be used in the run.
- 4. Set the pass number index \(q=1\) and the iteration number index to \(j=1\).
- 5. Set the region size vector \(\mathbf{r}^{j}=\eta^{q}\mathbf{r}_{in}\).
- 6. By using the best control policy (the initial control policy for the first iteration of the first pass), integrate Eq. (7.1) from \(t=0\) to \(t_f\) to generate the \(\mathbf{x}\)-trajectory and
