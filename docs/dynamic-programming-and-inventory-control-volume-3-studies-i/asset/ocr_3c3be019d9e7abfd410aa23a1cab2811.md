We also can write

(10.1.8) 
\( z(x) + \rho = hx + \inf_{v \ge (D-x)^+} [K \mathbb{I}_{v>0} + cv + z(x+v-D)], \)

and the pair \( z(x), \rho \) given by (10.1.11), (10.1.4) is the unique solution of (10.1.8). Moreover the optimal feedback is

(10.1.9) 
\( \hat{v}(x) = \begin{cases} 0, & \text{if } x \ge D \\ D(\hat{k}+1) - x, & \text{if } x < D \end{cases} \)

PROOF. The solution of (10.1.11) is simply

(10.1.10) 
\( z(kD + \xi) = hD \frac{k(k+1)}{2} + \xi h(k+1) - k\rho, \forall 0 \le \xi < D; \) 
\( z(((k+1)D)^+) = hD \frac{(k+1)(k+2)}{2} - (k+1)\rho, \)

where again \( z(((k+1)D)^+) \) represents the limit to the right at point \( (k+1)D \). We know that

\( u_a(0) = \lambda(\hat{k}_a), \)

and it is easy to check that

\( (1-\lambda)\alpha_a(k) \to cD + \lambda_1(k), \forall k. \)

This property carries over to the infimum,

\( \hat{k}_a \to \hat{k}, \)

which proves (10.1.5). By definition,

(10.1.11) 
\( z_a(x) = \begin{cases} (h-c)x, & \text{if } x < D \\ hx - \rho_a + z_a(x-D), & \text{if } x \ge D \end{cases} \)

Thanks to (10.1.5), the convergence of \( z_a(x) \) to \( z(x) \) follows easily. To prove (10.1.8), one looks at (10.1.11), which can be written as

(10.1.12) 
\( z_a(x) + \rho_a = hx + \inf_{v \ge (D-x)^+} [K \mathbb{I}_{v>0} + cv + \alpha z_a(x+v-D)]. \)

We note the relation

(10.1.13) 
\( \rho_a = K + Dc(\hat{k}_a+1) + \alpha z_a(\hat{k}_a D). \)

Denote

\( G_a(x, v) = K \mathbb{I}_{v>0} + c(v+x) + \alpha z_a(x+v-D), \)

and

\( G_a(x) = \inf_{v \ge (D-x)^+} G_a(x, v) = G_a(x, \hat{v}_a(x)), \)

and similarly

\( G(x, v) = K \mathbb{I}_{v>0} + c(v+x) + z(x+v-D); \) 
\( G(x) = \inf_{v \ge (D-x)^+} G(x, v) = G(x, \hat{v}(x)). \)

We claim that

(10.1.14) 
\( G_a(x) \to G(x). \)

Indeed, when \( x \ge D \), \( G_a(x) = G_a(x, 0) \to G(x, 0) = G(x) \). When \( x < D \), then from (10.1.13) and the expression of \( \hat{v}_a(x) \)

\( G_a(x) = \rho_a \to \rho = G(x). \)