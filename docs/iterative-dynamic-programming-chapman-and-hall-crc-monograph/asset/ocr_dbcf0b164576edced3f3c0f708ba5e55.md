![](bbox=[0.395, 0.085, 0.652, 0.364])

Figure 11.16: Optimal state trajectories for Example 6 resulting from the use of the control policy in Figure 11.15

# 11.3.2  State constraint variables

To deal with inequality constraints on the state, we follow the approach of Luus [10], which was also used in Example 6 in the previous section, with a small variation. Instead of difference equations, we use differential equations as suggested by Mekarapiruk and Luus [21] to construct the penalty functions. We therefore introduce *k state constraint variables* through the differential equations

$$\frac{dx_{n+i}}{dt}=\begin{cases}0 & \text{if } \psi_i(\mathbf{x})\leq 0\\ \psi_i(\mathbf{x}) & \text{if } \psi_i(\mathbf{x})>0\end{cases} \tag{11.121}$$

for $i=1,2,\ldots,k$, with the initial condition

$$x_{n+i}(0)=0,\qquad i=1,2,\ldots,k. \tag{11.122}$$

At the final time $t_f$, $x_{n+i}(t_f)$ therefore gives the total violation of the $i^{th}$ inequality constraint integrated over time. The advantage of taking such value is that sometimes a violation may occur for a short time inside a time stage, and such a violation may go by unnoticed if the difference equation approach is used where the violations are checked only at the ends of the time stages. We choose the augmented performance index to be minimized as

$$J=I+\sum_{i=1}^{k}\theta_i x_{n+i}(t_f) \tag{11.123}$$

where $\theta_i>0$ are penalty function factors for the inequality state constraints. Let us consider some illustrative examples.