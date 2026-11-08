The connection condition at the left end is given as

$$
\begin{aligned}
p_1(000) &= (1 - \alpha)(p_1(111) + p_1(1000)) + p_1(0000), \\
p_1(001) &= p_1(0001) + (1 - \alpha)(p_1(101) + p_1(1001)), \\
p_1(010) &= \alpha p_1(01), \\
p_1(100) &= \alpha(p_1(11) + p_1(1000)), \\
p_1(110) &= (1 - \alpha)p_1(01),
\end{aligned}
\qquad
\begin{aligned}
p_1(011) &= p_1(001), \\
p_1(101) &= \alpha(p_1(101) + p_1(1001)), \\
p_1(111) &= 0. \quad (33)
\end{aligned}
$$

In this case, if either of the uniform stationary solutions is inserted into $p_1$, the equations are not satisfied. Instead, if we assume that $p_2$ equals the stationary solution for $\frac{1}{2} \le \rho \le 1$, we have

$$
\begin{aligned}
p_1(000) &= \frac{(1 - \alpha)^2}{4 - 3\alpha + \alpha^2}, &
 p_1(001) &= \frac{1 - \alpha}{4 - 3\alpha + \alpha^2}, \\
p_1(010) &= \frac{\alpha}{4 - 3\alpha + \alpha^2}, &
 p_1(011) &= \frac{1 - \alpha}{4 - 3\alpha + \alpha^2}, \\
p_1(100) &= \frac{\alpha(1 - \alpha)}{4 - 3\alpha + \alpha^2}, &
 p_1(101) &= \frac{\alpha^2}{4 - 3\alpha + \alpha^2}, \\
p_1(110) &= \frac{1 - \alpha}{4 - 3\alpha + \alpha^2}, &
 p_1(111) &= 0. \quad (34)
\end{aligned}
$$

Note that only the property $p_2(000) = 0$ has been used to derive the above. The relation between $\alpha$ and $\rho$ should be obtained by $p_1(000) + p_1(100) = p_2(000) + p_2(001) = \frac{1 - \rho}{2}$, which leads to

$$\rho = \rho_L = \frac{2 - \alpha + \alpha^2}{4 - 3\alpha + \alpha^2}. \quad (35)$$

However, this is inconsistent with another condition $p_1(001) + p_1(101) = p_2(010) + p_2(011) = \frac{\rho}{2}$. Namely, the two conditions cannot be satisfied at the same time by the uniform solution. This inconsistency is resolved by considering a periodic solution for the stationary distribution. If we assume period two for the distribution and denote the distribution function starting from an even-numbered cell by $p_e$ and that starting from an odd-numbered cell by $p_o$, Eqs. 28 are replaced with

$$
\begin{aligned}
p_e(000) &= p_o(111) + p_e(0000) + p_o(10000), &
 p_e(001) &= p_e(0001) + p_o(1101) + p_o(11001), \\
p_e(010) &= p_o(101), &
 p_e(011) &= p_e(001), \\
p_e(100) &= p_o(011) + p_o(01000), &
 p_e(101) &= p_o(0101) + p_o(01001), \\
p_e(110) &= p_o(001) &
 p_e(111) &= 0 \quad (36)
\end{aligned}
$$

and those with $p_e$ and $p_o$ interchanged. For $\rho \ge \frac{1}{2}$ we have the solution similar to (30) except

$$p_e(010) = p_o(101) = \rho - \frac{1}{2} + \epsilon, \quad p_e(101) = p_o(010) = \rho - \frac{1}{2} - \epsilon, \quad (37)$$

where $\epsilon$ is a parameter satisfying $-(\rho - 1/2) \le \epsilon \le \rho - 1/2$. Then, if we assume $p_2 = p_e$ with

$$\epsilon = -\frac{\alpha(1 - \alpha)}{2(4 - 3\alpha + \alpha^2)}, \quad (38)$$