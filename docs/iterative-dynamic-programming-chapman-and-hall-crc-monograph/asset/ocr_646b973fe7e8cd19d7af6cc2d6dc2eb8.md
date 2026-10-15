![](bbox=[0.401, 0.073, 0.657, 0.362])

Figure 12.11: Time optimal control policy for Example 5

is shown in Figure 12.10. The resulting four stage bang-bang control policy was used then as the initial condition for the refined run which gave a final time of $t_f = 4.8319$ with the sum of absolute deviations from the final state of $S = 2.89 \times 10^{-8}$. The values of the shifting terms are $s_1 = -0.006372$, $s_2 = 0.013975$, $s_3 = -0.012346$, and $s_4 = 0.005000$.

The resulting time optimal control policy is given in Figure 12.11 and the state trajectories are shown in Figure 12.12. The computation time on a PentiumII/350 for $P = 20$ was 329 s, and for $P = 4$ the computation time was 59 s.

# 12.5  High dimensional systems

The use of IDP for time optimal control of high dimensional systems has not been fully explored. The approaches used by Bojkov and Luus [2] have been found very useful in the time optimal control of a 20-plate gas absorber. Here we want to just outline the main ideas and the interested reader can refer to this paper for the details. To simplify the discussion, let us assume that the variables have been transformed so that the desired state is the origin.

Rosen et al. [16] showed that there is a significant effect of the tolerance to which the origin is reached on the final time $t_f$ in the time optimal control. Although mathematically it is nice to reach the origin to within the computational accuracy of the computer, this is not necessary. For the 6-plate gas absorber, for example, to get to the origin within $10^{-6}$ tolerance gives a minimum time of $t_f = 6$ min, whereas to get to within $10^{-3}$ of the origin (within the measurement error) reduces the time