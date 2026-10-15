# ### 5.2 Comparison of uniform distribution to random choice

Let us consider the CSTR outlined in Chapter 1, where the inlet flow rate for species A in dimensionless units is specified as $q_1 = 6$, and there are three control variables. The equations describing the system are:

```
$$\begin{aligned}
\frac{dx_1}{dt} &= q_1-qx_1-17.6x_1x_2-23x_1x_6u_3 \tag{5.1}\\
\frac{dx_2}{dt} &= u_1-qx_2-17.6x_1x_2-146x_2x_3 \tag{5.2}\\
\frac{dx_3}{dt} &= u_2-qx_3-73x_2x_3 \tag{5.3}\\
\frac{dx_4}{dt} &= -qx_4+35.2x_1x_2-51.3x_4x_5 \tag{5.4}\\
\frac{dx_5}{dt} &= -qx_5+219x_2x_3-51.3x_4x_5 \tag{5.5}\\
\frac{dx_6}{dt} &= -qx_6+102.6x_4x_5-23x_1x_6u_3 \tag{5.6}\\
\frac{dx_7}{dt} &= -qx_7+46x_1x_6u_3 \tag{5.7}\\
\frac{dx_8}{dt} &= 5.8(qx_1-q_1)-3.7u_1-4.1u_2+q(23x_4+11x_5+28x_6+35x_7)-5u_3^2-0.099 \tag{5.8}
\end{aligned}$$
```

where $q=q_1+u_1+u_2$ and $q_1=6$. Later we allow $q_1$ to be another control variable, but here we want to restrict the number of control variables to 3, as was done by Rao and Luus [6]. The last differential equation gives the performance index. The problem is to maximize

```
$$I=x_8(t_f) \tag{5.9}$$
```

where the final time $t_f$ is specified as 0.2. The initial state is specified as $\mathbf{x}(0)=[0.1883\ 0.2507\ 0.0467\ 0.0899\ 0.1804\ 0.1394\ 0.1046\ 0]^T$. The control variables are constrained by

```
$$\begin{aligned}
0\le u_1\le20 \tag{5.10}\\
0\le u_2\le6 \tag{5.11}\\
0\le u_3\le4 \tag{5.12}
\end{aligned}$$
```

This example was used by Rao and Luus [6] to evaluate numerous algorithms employing control vector iteration based on Pontryagin’s maximum principle. They found that the algorithms yielded results between $I=20.05$ and $I=20.09$ for the maximum performance index. This example was also used by Luus [2] in showing how iterative dynamic programming overcomes the curse of dimensionality, and by Luus [3] in