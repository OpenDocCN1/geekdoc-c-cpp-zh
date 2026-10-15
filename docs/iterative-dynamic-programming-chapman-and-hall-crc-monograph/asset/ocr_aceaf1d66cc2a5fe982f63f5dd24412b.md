![](bbox=[0.367, 0.091, 0.652, 0.391])

Figure 6.3: Convergence profile of IDP, showing the deviation from the optimum $I = 6226.047$ with $\eta = 0.70$ and $\gamma = 0.95$ using the number of randomly chosen points $R$ as parameter

When $\eta$ is increased to 0.75, the convergence rate is slightly slower than with $\eta = 0.70$, as is shown in Figure 6.5.

# 6.4.2  Effect of the region contraction factor $\gamma$

As is the case for the region restoration factor $\eta$, there is also a range for the region contraction factor $\gamma$ for which reasonable rate of convergence is obtained with a small number of randomly chosen values for control. As is shown in Figure 6.6, when using $\eta = 0.70$, there is a range $0.93 < \gamma < 0.98$ for which convergence is obtained with the use of $R = 3$.

# 6.4.3  Effect of the number of time stages

The optimal control policy obtained for this example is shown for typical control variables in Figure 6.7 and the state trajectories for some typical state variables are given in Figure 6.8. It is seen that the control policy is very smooth. The smoothness is increased by using a larger number of time stages, yielding a better approximation to the continuous control policy.

By doubling the number of time stages to $P = 80$, we obtained the minimum performance index of $I = 6225.568$. This result was obtained with the use of $R = 3$ with $\eta = 0.70$ and $\gamma = 0.95$ in 24 passes, each consisting of 30 iterations as before.