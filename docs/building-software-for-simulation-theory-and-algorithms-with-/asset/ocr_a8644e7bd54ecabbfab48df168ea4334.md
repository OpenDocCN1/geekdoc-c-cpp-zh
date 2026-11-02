and

$$
x_4[(2,0),(2,2)],\ \text{with } x_4(t)=
\begin{cases}
2 & \text{if } t=(2,0)\\
\Phi & \text{otherwise}
\end{cases}
$$

The system starts with \(q=\infty\) and has been in that state for one unit of time. Using Equation 4.7 to compute its response to \(x_1\), we have

$$
\begin{aligned}
\delta((\infty,1), x_1[(0,0),(1,0)]) &= \delta((1,0), x_1[(0,1),(1,0)]) && \text{(Case 1)}\\
&= \delta((1,1), x_1[(1,0),(1,0)]) && \text{(Case 4)}\\
&= (1,1) && \text{(Case 5)}
\end{aligned}
$$

With the system in total state \((1,1)\), applying \(x_2\) gives

$$
\begin{aligned}
\delta((1,1), x_2[(1,0),(1,1)]) &= \delta((0,0), x_2[(1,1),(1,1)]) && \text{(Case 2)}\\
&= (0,0) && \text{(Case 5)}
\end{aligned}
$$

With the system in total state \((0,0)\), we apply \(x_3\) and get

$$
\begin{aligned}
\delta((0,0), x_3[(1,1),(2,0)]) &= \delta((\infty,0), x_3[(1,2),(2,0)]) && \text{(Case 3)}\\
&= (\infty,1) && \text{(Case 5)}
\end{aligned}
$$

and the system returns to where it began. Finally, injecting \(x_4\) gives

$$
\begin{aligned}
\delta((\infty,1), x_4[(2,0),(2,2)]) &= \delta((2,0), x_4[(2,1),(2,2)]) && \text{(Case 1)}\\
&= (2,0) && \text{(Case 5)}
\end{aligned}
$$

and the final, total state is \((2,0)\).

The output trajectory \(y[(0,0),(2,2)]\) produced by this simulation is

$$
y(t)=
\begin{cases}
1 & \text{if } t=(1,0)\\
0 & \text{if } t=(1,1)\\
\Phi & \text{otherwise}
\end{cases}
$$