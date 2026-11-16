(6.48) \(\sum_k \left|\hat{\phi}_{M,m}(\omega + 2\pi k)\right|^2 = 1\)

is satisfied. In (6.48) the index \(m\) indicates the degree of smoothness—that is, the \(m\)th order corner smoothing function \(S_m(\omega)\) is \(m\) times continuously differentiable. To satisfy the orthogonality requirement (6.48), these corner smoothing functions should have the following properties:

\(\begin{cases} S_m(y)+S_m(1-y)=1, & 0 \le y \le 1; \\ S_m(y)=0, & y < 0; \\ S_m(y)=1, & y > 1. \end{cases}\)

Examples of corner smoothing functions are given below.

\(S_0(y) = \begin{cases} 0, & y < 0; \\ y, & 0 \le y \le 1; \\ 1, & y > 1. \end{cases}\)

\(S_1(y) = \begin{cases} 0, & y < 0; \\ 2y^2, & 0 \le y < 0.5; \\ -2y^2 + 4y - 1, & 0.5 \le y \le 1; \\ 1, & y > 1. \end{cases}\)

Let \(S_m(y)\) be a desirable corner smoothing function. Then