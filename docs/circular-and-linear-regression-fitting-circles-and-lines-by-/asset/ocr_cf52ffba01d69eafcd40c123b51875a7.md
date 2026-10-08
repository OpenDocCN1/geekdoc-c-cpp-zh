+   1. Form the matrix **X** and compute **X**$^{T}$**X**.
2. Compute the coefficients (5.32) of the characteristic equation (5.31).
3. Initialize $\eta = 0$, and apply Newton’s procedure to find a root $\eta$. 
4. Compute **A** as a null vector of **X**$^{T}$**X** − $\eta$**B**.

Table 5.2: *Pratt circle fit (Newton-based).*

denote the roots of (5.31).

**Theorem 9** *In the nonsingular case we have P(0) < 0 and P*''*$($\eta$) < 0 for all 0*\*≤*\*$\eta*\*≤*\*$\eta*$_{2}$. Thus, a simple Newton method supplied with the initial guess*\*$\eta*\*= 0 always converges to the smallest positive root*\*$\eta*$_{2}$*of P(\*$\eta$)*

*Proof. Denote by*\*$\eta*$_{1}^{\prime}$*≤*\*$\eta*$_{2}^{\prime}$*≤*\*$\eta*$_{3}^{\prime}$*the zeroes of the derivative P'($\eta$), and by*\*$\eta*$_{1}^{\prime\prime}$*<*\*$\eta*$_{2}^{\prime\prime}$*the zeroes of the second derivative P*''*$($\eta$) = 48*$\eta*$^{2}+c*$_{2}$. Note that the cubic term is missing in (5.31), so there is no linear term in P*''*$($\eta$). Since c*$_{2}$*< 0, it follows that*\*$\eta*$_{1}^{\prime\prime}$*< 0 <*\*$\eta*$_{2}^{\prime\prime}$. Now due to the interlacing property of the roots of a polynomial and its derivative we conclude that

$\eta_{1}^{\prime} \le \eta_{1}^{\prime\prime} < 0 < \eta_{2} \le \eta_{2}^{\prime} \le \eta_{2}^{\prime\prime}.$

This implies that P(0) < 0, P'(0) > 0, and P($\eta$) is a convex function (meaning that P*''*$($\eta$) < 0) in the interval between 0 and the smallest positive root*\*$\eta*$_{2}$. Thus the Newton procedure is bound to converge, and its limit point will be the desired root*\*$\eta*$_{2}$. Theorem is proved.$\Box$

In practice, the Newton procedure converges in 3 to 5 iterations, on the average, with the tolerance set to 10$^{−12}$. Once the smallest positive root*\*$\eta*$_{2}$*of (5.31) is located, the parameter vector*\***A***is chosen as a null vector of*\***X***$^{T}$***X***−*\*$\eta$***B***according to (5.28). We call this algorithm the*\*$Newton-based$*Pratt fit.

**Computational issues.** We have determined experimentally, working with MATLAB, that the above Newton-based implementation of the Pratt fit is just as fast as the Kåsa method (see Table 5.3). The numerically stable SVD-based implementation of the Pratt fit described earlier in this section is about 2 to 3 times slower than the Kåsa method. For comparison, all geometric fits are at least 10 times slower than the Kåsa method.

MATLAB codes of both versions of the Pratt method (as well as many other circle fits) are available from our web page [84].