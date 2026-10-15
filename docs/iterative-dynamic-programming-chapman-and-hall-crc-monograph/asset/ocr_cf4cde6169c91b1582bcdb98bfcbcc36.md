$$\frac{dx_2}{dt}=g_2x_3-\frac{u}{x_5}x_2 \tag{9.43}$$

$$\frac{dx_3}{dt}=g_3x_3-\frac{u}{x_5}x_3 \tag{9.44}$$

$$\frac{dx_4}{dt}=-7.3g_3x_3+\frac{u}{x_5}(20-x_4) \tag{9.45}$$

$$\frac{dx_5}{dt}=u \tag{9.46}$$

where

$$g_3=\frac{21.87x_4}{(x_4+0.4)(x_4+62.5)} \tag{9.47}$$

$$g_2=\frac{x_4e^{-5x_4}}{0.1+x_4} \tag{9.48}$$

$$g_1=\frac{4.75g_3}{0.12+g_3} \tag{9.49}$$

with the initial condition

$$\mathbf{x}(0)=[\,0\quad 0\quad 1\quad 5\quad 1\,]^T. \tag{9.50}$$

Here $x_1$ denotes the concentration of secreted SUC-s2 in culture and $x_2$ denotes the concentration of total SUC-s2 in culture, both expressed in arbitrary units; $x_3$ is the culture cell density (g/L), $x_4$ is the culture glucose level (g/L), and $x_5$ is the culture volume (L). The feed rate to the reactor $u$ is bounded by

$$0\leq u\leq 2. \tag{9.51}$$

The performance index to be maximized is the amount of secreted SUC2-s2 produced at the final time $t_f$

$$I=x_1(t_f)x_5(t_f) \tag{9.52}$$

where the final time $t_f$ is specified as 15 h. We also analyze the effect of changing $t_f$. For integration of the differential equations with DVERK [5], the local error tolerance of $10^{-6}$ was used. However, to ensure stability during integration, each time step was broken into a number of subsections approximately one-half of the number of stages $P$. The first run consisted of taking $P=15$, and the number of subsections for integration was chosen as 7 to ensure stability. For the first run it was decided to use $R=5$, $\gamma=0.95$, $\eta=0.85$, initial values for control and stage lengths of 1 and 0.5, respectively, 50 passes, each consisting of 40 iterations, penalty function factor $\theta=100$, and initial value for the shifting parameter $s=0$. The computer program is listed in Appendix D. In a computation time of 372 s on a PentiumII/350, convergence to $I=32.6691$ and $s=-0.04878$ was obtained, yielding the control policy shown in Figure 9.17.