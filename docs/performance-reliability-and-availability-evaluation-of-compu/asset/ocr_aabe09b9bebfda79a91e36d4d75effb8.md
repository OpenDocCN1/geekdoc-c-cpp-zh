# Performance, Reliability, and Availability Evaluation of Computational Systems

![](bbox=[0.223, 0.114, 0.777, 0.423])

**Figure 19.6** AND Gate.

the system is operational as long as at least one server ($S_1$, $S_2$, or $S_3$) is functional, and a parallel block diagram represents such a behavior.

Let us obtain the reliability from the logical function. Assume the name of each component is also adopted to represent the logical variables. Thus, let us define the Boolean function as $B = (S_1, S_2, S_3)$. Therefore, the logical function that represents a failure is

> $\overline{\overline{(B)}} = \overline{S_1} \wedge \overline{S_2} \wedge \overline{S_3}$.

Hence, negating both sides of the expression above, we obtain

> $\overline{\overline{(B)}} = S_1 \wedge \overline{S_2} \wedge \overline{S_3}$.

Thus,

> $\overline{\overline{(B)}} = \overline{S_1} \wedge S_2 \wedge \overline{S_3}$.

The respective structure-function is obtained by applying the transformations rules shown in Table 18.3. Hence

> $\Phi(X) = 1 - ((1-x_{S_1}) \times (1-x_{S_2}) \times (1-x_{S_3}))$.