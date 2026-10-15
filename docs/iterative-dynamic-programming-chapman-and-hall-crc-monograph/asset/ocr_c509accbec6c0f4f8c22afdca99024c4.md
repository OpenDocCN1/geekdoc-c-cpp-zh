and
$$-0.809 \le u_2 \le 0.713.$$ \tag{11.106}

In addition, we have the state constraints on $x_4$ and $x_5$:
$$-2.5 \le x_4 \le 2.5$$ \tag{11.107}
$$-1 \le x_5 \le 1.$$ \tag{11.108}

The optimal control problem is to find $u_1$ and $u_2$ in the time interval $0 \le t < 1$, so that the performance index
$$I = x_7(t_f)$$ \tag{11.109}
is minimized, when $t_f = 1$.

Here we choose the augmented performance index to be minimized, as suggested by Luus[10],
$$J = I + \sum_{i=1}^{6} \theta_i |x_i(t_f) - x_i^d| + \rho \sum_{j=1}^{P} (p_{4j} + p_{5j})$$ \tag{11.110}

where
$$p_{4j} = \begin{cases} -2.5 - x_4(t_j) & \text{if } x_4(t_j) < -2.5 \\ 0 & \text{if } -2.5 \le x_4(t_j) \le 2.5 \\ x_4(t_j) - 2.5 & \text{if } x_4(t_j) > 2.5 \end{cases}$$ \tag{11.111}

and
$$p_{5j} = \begin{cases} -1 - x_5(t_j) & \text{if } x_5(t_j) < -1 \\ 0 & \text{if } -1 \le x_5(t_j) \le 1 \\ x_5(t_j) - 1 & \text{if } x_5(t_j) > 1. \end{cases}$$ \tag{11.112}

In the augmented performance index we set $\rho = 1$, which is sufficiently large to ensure that the state inequality constraints are satisfied, and concentrate on the determination of the six penalty function factors $\theta_1, \theta_2, \cdots, \theta_6$.

For the starting point for the first run we chose $\theta_i = 10^{-2}, \epsilon_i = 10^{-3}, i = 1,2,\cdots,6$, $\delta = 0.05$ and chose $P = 10$ time stages, each of length $0.1$. For integration we chose the Runge-Kutta method with an integration step size of $0.01$. We took initial values for the control variables $u_1^{(0)} = 0.5$ and $u_2^{(0)} = 0$ and initial region sizes for the control variables as $r_1^{(0)} = 1.3$ and $r_2^{(0)} = 0.3$. For IDP we chose $N = 3$ grid points, $R = 25$, $\gamma = 0.70$, $\eta = 0.95$, and allowed $150$ passes, each consisting of $30$ iterations. After every pass $\delta$ was decreased by $1\%$, and the penalty function factors were updated. The computation time for $150$ passes was $617$ s on a PentiumII/350. The convergence profile as measured by the sum of absolute deviations of the final states from their desired values is shown in Figure 11.13. The value of the performance index is $I = 0.005370$. The final state is

$$\mathbf{x}(t_f) = \begin{bmatrix} 10.001479 & 14.000000 & -0.000931 & 2.500000 \\ 0.000000 & -0.001116 & 0.005370 \end{bmatrix}^T$$ \tag{11.113}