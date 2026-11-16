The first step in the algorithm is to compute the syndromes $S_i = y(\alpha^i)$ for $1 \le i \le 2t$ from the received vector. This process is aided by the following theorem proved in Exercise 296. In the theorem we allow $S_i$ to be defined as $y(\alpha^i)$ even when $i > 2t$; these may not be legitimate syndromes as $c(\alpha^i)$ may not be 0 in those cases.

# Theorem 5.4.1 $S_i^q = S_{iq}$ for all $i \ge 1$.

# Exercise 295 Let $H$ be the $t \times n$ matrix

$$ H = \begin{bmatrix} 1 & \alpha & \alpha^2 & \cdots & \alpha^{n-1} \\ 1 & \alpha^2 & \alpha^4 & \cdots & \alpha^{(n-1)2} \\ \vdots & & & & \vdots \\ 1 & \alpha^t & \alpha^{2t} & \cdots & \alpha^{(n-1)t} \end{bmatrix} $$

If $y(x) = y_0 + y_1 x + \cdots + y_{n-1} x^{n-1}$, let $\mathbf{y} = (y_0, y_1, \dots, y_{n-1})$. Finally, let $\mathbf{S} = (S_1, S_2, \dots, S_t)$, where $S_i = y(\alpha^i)$.

+   (a) Show that $H\mathbf{y}^T = \mathbf{S}^T$.

+   (b) Use Exercise 4.4.3 and part (a) to explain the connection between the notion of syndrome given in this section and the notion of syndrome given in Section 1.11.

# Exercise 296 Prove Theorem 5.4.1.

The syndromes lead to a system of equations involving the unknown error locations and the unknown error magnitudes. Notice that from (5.5) the syndromes satisfy

$$ S_i = y(\alpha^i) = \sum_{j=1}^v e_{k_j} (\alpha^{k_j})^i = \sum_{j=1}^v e_{k_j} (\alpha^i)^{k_j}. $$

for $1 \le i \le 2t$. To simplify the notation, for $1 \le j \le v$, let $E_j = e_{k_j}$ denote the error magnitude at coordinate $k_j$ and $X_j = \alpha^{k_j}$ denote the error location number corresponding to the error location $k_j$. By Theorem 3.3.1, if $\alpha^i = \alpha^k$ for $i$ and $k$ between 0 and $n - 1$, then $i = k$. Thus knowing $X_j$ uniquely determines the error location $k_j$. With this notation (5.6) becomes

$$ S_i = \sum_{j=1}^v E_j X_j^i, \quad \text{for } 1 \le i \le 2t, $$

which in turn leads to the system of equations:

$$ \begin{aligned} S_1 &= E_1 X_1 + E_2 X_2 + \cdots + E_v X_v, \\ S_2 &= E_1 X_1^2 + E_2 X_2^2 + \cdots + E_v X_v^2, \\ S_3 &= E_1 X_1^3 + E_2 X_2^3 + \cdots + E_v X_v^3, \\ &\vdots \\ S_{2t} &= E_1 X_1^{2t} + E_2 X_2^{2t} + \cdots + E_v X_v^{2t}. \end{aligned} $$

This system is nonlinear in the $X_j$'s with unknown coefficients $E_j$. The strategy is to use (5.7) to set up a linear system, involving new variables $\sigma_1, \sigma_2, \dots, \sigma_v$, that will lead directly