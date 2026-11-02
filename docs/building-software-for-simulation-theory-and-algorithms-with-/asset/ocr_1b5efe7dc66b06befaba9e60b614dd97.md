```
~~~text
91  delete sim; delete hybrid_model;
92  return 0;
93 }
~~~
```

# ## 5.6 INTERACTIVE SIMULATION OF THE ROBOTIC TANK

In Chapter 4 the robot’s computer was modeled, and now the gears, tracks, motors, and equations of motion can be connected to it. Section 2.2.3 gives the complete set of equations.

# ### 5.6.1 Correcting the Dynamics of a Turn

An inflectional description of the event condition that initiates and ends a turn is obtained by rearranging Equation 2.19 to obtain the zero-crossing function

\[
g = \frac{B}{2}|F_l - F_r| - S_l \tag{5.14}
\]

When $g$ is equal to zero, the discrete variable *turning* switches its binary value. Brief consideration reveals that this model is unable to begin or end a turn. After *turning* changes value, $g$ is still zero, and so the model switches forever from turning to not turning and back, producing an illegitimate event trajectory.

This illegitimate behavior can be corrected with a hysteresis value $\epsilon$ to separate the torques that begin and end a turn. If $\epsilon$ is small, then the behavior of the model should very nearly approximate what was intended by Equation 5.14. This adjustment creates an event surface that moves when *turning* changes:

\[
g = \begin{cases}
\frac{B}{2}|F_l - F_r| - (S_l - \epsilon) & \text{if } turning = \text{true} \\
\frac{B}{2}|F_l - F_r| - S_l & \text{if } turning = \text{false}
\end{cases}
\tag{5.15}
\]

This solves the illegitimacy problem, but a smooth $g$ is also desirable so that linear interpolation gives a reasonable approximation. The absolute values are removed by creating two event surfaces, one for $F_l - F_r > 0$ and another for $F_l - F_r < 0$. The functions

\[
g_r = \begin{cases}
\frac{B}{2}(F_l - F_r) - (S_l - \epsilon) & \text{if } turning = \text{true} \\
\frac{B}{2}(F_l - F_r) - S_l & \text{if } turning = \text{false}
\end{cases}
\tag{5.16}
\]