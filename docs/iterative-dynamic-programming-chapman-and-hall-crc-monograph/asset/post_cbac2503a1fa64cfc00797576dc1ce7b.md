
Here, the control policies obtained by IDP and LJ optimization procedure are almost identical, where a sudden change at stage 69 occurs in the control variables $u_1$ and $u_2$. Therefore, LJ optimization procedure is ideally suited for checking results obtained by other methods, especially when the optimal control policy differs from what is expected, as is the case with this particular example. There are some problems, for example, model reduction, where LJ optimization method is well suited [24]. To illustrate the procedure, we consider several examples.

## 2.3.2 Simple example — 5 food diet problem

Let us first consider the food problem as specified in Table 2.1 which we solved by linear programming earlier. To solve this with the LJ optimization procedure is straightforward, since the number of variables is small and no auxiliary variables are required.

By denoting the amount of each food by $x_i$, let us choose as starting conditions $x_i = 0.5, i = 1, \cdots, 5$, and the initial region size for each variable 2.0. Although the initial starting point is infeasible, that does not matter, because the initial starting point simply sets the centre point around which the randomly chosen points will be chosen. Let us choose the reduction factor for reducing the region sizes after every iteration $\gamma = 0.95$, 101 iterations per pass, and a maximum of 20 passes. Let us use the number of randomly chosen points per iteration as a parameter and use the 50, 100, 150, 200, and 300 for this parameter. After every pass we put the region sizes equal to the extent of the variation of that particular variable. If the variation is less than $10^{-6}$, then the region size is put equal to $10^{-6}$. This scheme of determining the initial region sizes for variables has been found effective in solving several optimization problems [22, 23, 25]. The listing of the computer program for this problem is given in Appendix C.

The results of the computations are given in Table 2.2. When more than 50 randomly chosen points were chosen, there was no problem in getting convergence to the maximum utility of $I = 247.06390$ with $x_1 = 2.0000, x_2 = 0.3368, x_3 = 1.2090, x_4 = 0.0000$ and $x_5 = 0.0000$. These values correspond very closely to the values obtained by linear programming and reported in Figure 2.2. It is interesting to note that with $R = 200$ randomly chosen points, convergence results already after 4 passes. The computation time for 20 passes with $R = 200$ was 5.83 s on a Pentium/120 digital computer, which is considerably greater than required by linear programming, but is still quite small.

## 2.3.3 Model reduction example

An important problem encountered in process control is how to reduce the complexity of a transfer function without losing essential information. Transfer functions of very high order are difficult to use, and if a transfer function of lower order gives essentially

Table 2.2: Convergence of the LJ optimization procedure showing the effect of the number of randomly chosen points per iteration R on the performance index as a function of the pass number

| Pass Number | R = 50 | R = 100 | R = 150 | R = 200 | R = 300 |
|---|---|---|---|---|---|
| 1 | 246.91464 | 245.72210 | 246.97915 | 246.93550 | 247.03129 |
| 2 | 247.02599 | 245.83314 | 246.99476 | 247.01367 | 247.05779 |
| 3 | 247.06385 | 245.88798 | 247.06383 | 247.06376 | 247.06389 |
| 4 | 247.06385 | 245.93883 | 247.06388 | 247.06390 | 247.06390 |
| 5 | 247.06389 | 246.00646 | 247.06388 | 247.06390 | 247.06390 |
| 10 | 247.06389 | 246.61040 | 247.06389 | 247.06390 | 247.06390 |
| 20 | 247.06389 | 247.06390 | 247.06390 | 247.06390 | 247.06390 |

the same behavior, then it is natural to use the lower order transfer function. Many methods suggested for model reduction give unsatisfactory results [24]. The method of reducing the order of the transfer function as suggested by Luus [18] is to minimize the deviations between the reduced model and the original model in the Nyquist plot.

Let us consider the eighth-order system of Krishnamurthy and Seshadri [9]

$F(s) = \frac{194480 + 482964s + 511812s^2 + 278376s^3 + 82402s^4 + 13285s^5 + 1086s^6 + 35s^7}{9600 + 28880s + 37492s^2 + 27470s^3 + 11870s^4 + 3017s^5 + 437s^6 + 33s^7 + s^8}$ (2.54)

where we wish to get a reduced model of lower order. The zeroes (roots of the numerator) of the transfer function are $-1.0346 \pm 0.63102j$, $-2.6369$, $-3.6345$, $-4.9021$, $-7.8014$, and $-9.7845$. The poles (roots of the denominator) of the transfer function are $-1$, $-1 \pm j$, $-3$, $-4$, $-5$, $-8$, and $-10$.

Let us first choose the third order reduced model in the form

$G(s) = \frac{20.2583(1 + x_1 s + x_2 s^2)}{(1 + x_3 s)(1 + x_4 s + x_5 s^2)}$ (2.55)

where we have chosen the constant in the numerator to preserve the steady-state gain.

As was suggested in [18], we choose 100 values for the frequency by taking $\omega_1 = 0.01$ and $\omega_{i+1} = 1.1\omega_i$ to cover the frequency range from 0.01 to 125 and choose the parameters $x_i, i = 1, 2, \cdots, 5$ by minimizing the sum of squares of deviations expressed as

$I = \sum_{i=1}^{100}[Re(F(j\omega_i)) - Re(G(j\omega_i))]^2 + [Im(F(j\omega_i)) - Im(G(j\omega_i))]^2.$ (2.56)

The initial values for the five parameters are chosen from the dominant zeroes and poles of the original system to be $x_1 = 1.4090$, $x_2 = 0.680928$, $x_3 = 1.0$, $x_4 = 1.0$,

and $x_5 = 0.5$. For the region sizes, we choose for the beginning of the first pass 0.1 times the initial values of the parameters; for the second pass we choose 0.95 times this initial values for the parameters. For all subsequent passes the initial region sizes were calculated from the extent of the variation of each particular variable. The region sizes were reduced by $\gamma = 0.95$ after every iteration.

There is a trade-off between the number of random points $R$ used per iteration and the number of passes, each consisting of 50 iterations, required for convergence to the minimum value of the sum of squares of deviations in the Nyquist plot, $I_{min} = 0.32782509$. This is shown in Table 2.3. The computation time is given for the total number of passes used for the run.

Table 2.3: Effect of the number of randomly chosen points per iteration for convergence to $I_{min} = 0.3278251$

| Random Points per Iteration $R$ | Number of Passes for Convergence | Number of Function Evaluations | CPU Time s | Passes |
|---:|---:|---:|---:|---:|
| 25 | 543 | 13575 | 176 | 600 |
| 50 | 424 | 21200 | 299 | 500 |
| 100 | 169 | 16900 | 348 | 300 |
| 200 | 75 | 15000 | 231 | 100 |
| 250 | 39 | 9750 | 434 | 150 |
| 500 | 32 | 16000 | 577 | 100 |
| 1000 | 18 | 18000 | 462 | 40 |
| 2000 | 11 | 22000 | 471 | 20 |
| 5000 | 9 | 45000 | 635 | 10 |

The convergence profile tends to be quite smooth, as is shown in Figure 2.6. Although faster convergence in terms of number of passes is obtained when $R$ is increased, the computational effort increases substantially when $R$ exceeds 2000.

When we measure the computational effort in terms of the number of times the performance index has been calculated (number of function evaluations), we see that in the range between $R = 100$ to $R = 1000$ we need approximately 20000 function evaluations, requiring about 4 min of computation time. It is also clear that it is not advisable here to take $R$ to be greater than 2000. In fact, it is actually most economical to take $R = 25$ and allow a large number of passes.

The resulting third order reduced model is

$$G(s)=\frac{20.2583(1+0.84076s+0.55067s^2)}{(1+0.61769s)(1+0.73908s+0.53529s^2)}.$$(2.57)

Let us now consider a fourth order reduced model with the following structure

$$G(s)=\frac{20.2583(1+x_1s)(1+x_2s+x_3s^2)}{(1+x_4s+x_5s^2)(1+x_6s+x_7s^2)}.$$ (2.58)

![](img/06ae75163df4fdf5e1eec243d497d393_65_0.png)

Figure 2.6: Convergence profile for the third order reduced model using N = 50 iterations per pass

where again we want to preserve the steady-state gain. There are now 7 parameters to be determined. The initial values are again chosen from the dominant zeroes and poles of the original transfer function: x1 = 0.37923, x2 = 1.40900, x3 = 0.68093, x4 = 1.33333, x5 = 0.33333, x6 = 1.0, and x7 = 0.5. From the experience gained by the third order model reduction, we take a small number of random points per iteration ( R = 25), but a large number of passes. The convergence rate is very much dependent on the tolerance ε used as the minimum value for the initial region size to be used to prevent collapse of the particular region. As can be seen in Figures 2.7 and 2.8, the trend is similar whether 60 iterations are used per pass, or 40 iterations are used per pass.

This leads us to use the scheme where the tolerance parameter ε = 10⁻⁵ is used for the first 2000 passes; it is then decreased to ε = 10⁻⁶ for the next 1000 passes, and decreased again for the last 1000 passes, as is shown in Figure 2.9. As is seen, convergence is obtained within 4000 passes with this adaptive choice of the tolerance parameter. The computation time on a Pentium/120 with R = 25 and N = 50 iterations per pass was 2077s, and very accurate results are obtained. The use of R = 200, with the use of adaptive method of specifying the tolerance parameter, yielded convergence to I_min = 0.00073136556 in 2929 passes. Computationally, however,
