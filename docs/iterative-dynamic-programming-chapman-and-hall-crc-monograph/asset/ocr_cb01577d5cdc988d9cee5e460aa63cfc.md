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

$$G(s)=\frac{20.2583(1+0.84076s+0.55067s^2)}{(1+0.61769s)(1+0.73908s+0.53529s^2)}. \tag{2.57}$$

Let us now consider a fourth order reduced model with the following structure

$$G(s)=\frac{20.2583(1+x_1s)(1+x_2s+x_3s^2)}{(1+x_4s+x_5s^2)(1+x_6s+x_7s^2)}. \tag{2.58}$$