# 10.3 Yeo’s singular control problem

One of the earliest examples tried with iterative dynamic programming ([9], [10]) is the singular control problem used by Yeo [18] to illustrate the use of quasilinearization to solve nonlinear singular control problems. The system is described by

$$\frac{dx_1}{dt} = x_2 \tag{10.32}$$

$$\frac{dx_2}{dt} = -x_3 u + 16 x_5 - 8 \tag{10.33}$$

$$\frac{dx_3}{dt} = u \tag{10.34}$$

$$\frac{dx_4}{dt} = x_1^2 + x_2^2 + 0.0005(x_2 + 16 x_5 - 8 - 0.1 x_3 u^2)^2 \tag{10.35}$$

$$\frac{dx_5}{dt} = 1 \tag{10.36}$$

with $\mathbf{x}(0) = \begin{bmatrix}0 & -1 & -\sqrt{5} & 0 & 0\end{bmatrix}^T$, and final time $t_f = 1$. The constraints on the control are

$$-4 \le u \le 10. \tag{10.37}$$

It is required to find the control policy that minimizes the performance index

$$I = x_4(t_f). \tag{10.38}$$

The optimal value of the performance index depends very much on the number of time stages, if the stages are of equal length, as was shown by Luus [9], and is given in Table 10.2. Although there is an improvement in the performance index as the number of time stages is increased, this improvement is not uniform because the optimal control policy involves two switches and the time of the switches is important. We now consider this optimal control problem by using stages of variable lengths, as we did for the other examples, and consider the augmented performance index

$$J = x_4(t_f) + \theta(t_{fc} - t_f - s)^2 \tag{10.39}$$

where $t_{fc}$ is the sum of the variable stage lengths, the penalty function factor $\theta$ is chosen to be 1, and $s$ is a shifting parameter, chosen initially zero, and is then updated after every pass by the deviation of the calculated final time from the specified final time $t_f$

$$s^{q+1} = s^q - (t_{fc} - t_f) \tag{10.40}$$

where $q$ is the pass number.

To minimize the augmented performance index we choose $P = 25$ stages, each of length 0.04 initially, $R = 25$, $\gamma = 0.95$, $\eta = 0.88$, 30 iterations per pass, and allow