+   2. Var $[X(h^k)] = \sigma^2 < \infty$
+   3. $E[(X(h^k)-\mu)(X(h^k h^j)-\mu)] = R_X(h^j)$

for all $t_k = h^k \in S$. Then $X(t_k)$ is a discrete $M$-stationary process with the discrete stationary dual process $Y^*_k = X(h^k)$.

Let $C_{Y^*}(j) = E[(Y^*_k - \mu)(Y^*_{k+j} - \mu)]$. This can be rewritten $C_{Y^*}(j) = E[(X(h^k)-\mu)(X(h^{k+j})-\mu)] = R_X(h^j)$. Since $C_{Y^*}(j) = C_{Y^*}(-j)$, it follows that $R_X(h^j) = R_X(h^{-j})$. If $t_k = h^k$ and $u = g(t) = \ln t / \ln h$, then $u_k = g(t_k) = g(h^k) = \ln h^k / \ln h = k$. Then, $t_k = g^{-1}(u_k) = h^{u_k} = h^k$. So

$g^{-1}(g(t_k)+g(t_j)) = h^{g(t_k)+g(t_j)}$
$= h^{k+j}$
$= h^k h^j.$

Thus, a discrete M-stationary process is a discrete G-stationary process with $u_t = g(t_k) = \ln t_k / \ln h$ and $\mathcal{S} = \{t_k : t_k = h^k,\ k = 0, \pm 1, \dots\}$. That is, $u_k = k$.

# 13.2.3 Discrete Euler(p) Model

Making use of Definition 13.3, Vijverberg and Gray (2009) and Gray et al. (2005) introduced and studied discrete Euler(p) processes. See also Vijverberg and Gray (2009).

# Definition 13.4

Let $t_k \in \mathcal{S} = \{t_k = h^k,\ k = 0, \pm 1, \pm 2, \dots\}$, and suppose $X(t_k)$ is the M-stationary solution of

$(X(h^k)-\mu) - \phi_1(X(h^{k-1})-\mu) - \dots - \phi_p(X(h^{k-p})-\mu) = a(h^k), \quad (13.5)$

where $a(h^k)$ is white noise. Then $X(t_k)$ is called a discrete Euler(p) process.