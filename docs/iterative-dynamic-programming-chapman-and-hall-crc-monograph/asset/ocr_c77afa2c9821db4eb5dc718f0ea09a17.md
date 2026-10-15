At the final time $t_f$, there are $k$ state variables that must be at the desired values, i.e.,

$$h_i=x_i(t_f)-x_i^d=0,\qquad i=1,2,\ldots,k\leq n.$$

The optimal control problem is to find the control policy $\mathbf{u}(t)$ in the time interval $0\leq t<t_f$ that minimizes the performance index

$$I=\Phi(\mathbf{x}(t_f))$$

where the final time $t_f$ is specified. This problem differs from what we have considered earlier by having the $k$ equality constraints that must be satisfied at the final time. Numerically the equality constraints are expressed explicitly as

$$\left|x_i(t_f)-x_i^d\right|\leq\epsilon_i,\qquad i=1,2,\ldots,k,$$

where $\epsilon_i$ is the tolerance for the $i^{th}$ constraint and is chosen sufficiently small. We would also like to know how the choice of the tolerance $\epsilon_i$ affects the value of the performance index $I$ at the optimum.

# 11.2.2  Quadratic penalty function with shifting terms

Let us construct an augmented performance index to take into account the $k$ equality constraints by adding to the performance index a quadratic penalty function containing shifting terms

$$J=I+\theta\sum_{i=1}^{k}(h_i-s_i)^2$$

where $\theta$ is a positive penalty function factor and the shifting terms $s_i$ are chosen so that computationally Eq. (11.3) becomes satisfied and the performance index in Eq. (11.4) becomes minimized as the iterative procedure progresses. The use of such shifting terms in the quadratic penalty function was first explored by Luus [13] for steady state optimization. It is noted that

$$(h_i-s_i)^2=h_i^2-2s_i h_i+s_i^2$$

so that near the optimum when Eq. (11.3) is almost satisfied, the term $h_i^2$ is negligibly small with respect to the other two terms and the minimization of the augmented performance index in Eq. (11.6) becomes equivalent to minimizing

$$J=I-2\theta\sum_{i=1}^{k}s_i h_i$$

since the term involving the square of the shifting term is simply a constant. Thus, the product $-2\theta s_i$ gives the Lagrange multiplier or sensitivity of the performance index to the change in the $i^{th}$ equality constraint in Eq. (11.3). This aspect of the