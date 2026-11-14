
Define also

(6.2.5) $$g(x) = (h - (p + h - c)F(x))^+,$$

then \( S_\alpha \uparrow S \) and

$$u_\alpha(x) - \frac{\rho}{1-\alpha} \to u(x),$$

where \( u \) is defined by

(6.2.6) $$
\begin{aligned}
u(S) &= (h - c)(S - E(S - D)^+); \\
u'(x) &= h + c + z(x),
\end{aligned}$$

where \( z \) is defined by

(6.2.7) $$z(x) = \sum_{n=1}^{+\infty} g * f^{*(n-1)},$$

with the same notation as in equation (5.1.17).

The function \( u(x) \) also satisfies

(6.2.8) $$u(x) = hx + pE(x - D)^- - \rho + Eu((x - D)^+), \forall x > S$$

(6.2.9) $$u(x) = hx + c(S - x) + pE(S - D)^- - \rho, \forall x \le S$$

and also

(6.2.10) $$
\begin{aligned}
u(x) &= (h - c)x - \rho + \inf_{v \ge 0} [l_0(x + v) + Eu((x + v - D)^+)] \\
Eu((S - D)^+) &= 0
\end{aligned}$$

PROOF. From the formula (6.2.2) the convergence of \( S_\alpha \) to \( S \) is easy. Noting that

$$F(S_\alpha) = \frac{p - c}{p + \alpha(h - c)},$$

we see that \( S_\alpha \) increases with \( \alpha \). Moreover an easy calculation shows that

$$u_\alpha(S_\alpha) = \frac{1}{1-\alpha}[pD + S_\alpha(h(1-\alpha) - p + \alpha c)] + (p + \alpha(h - c))E((S_\alpha - D)^+)],$$

from which it follows, thanks to the choice of \( \rho \) that

(6.2.11) $$u_\alpha(S_\alpha) - \frac{\rho}{1-\alpha} \to (h - c)(S - E(S - D)^+).$$

Now we have, from Theorem 5.2

Since

$$u'_\alpha(x) = h - c + z_\alpha(x),$$

where

$$z_\alpha(x) = \sum_{n=1}^\infty \alpha^{n-1} g_\alpha * f^{*(n-1)}(x),$$

with

$$g_\alpha(x) = (c + \alpha(h - c) - (p + \alpha(h - c))F(x))^+.$$

Clearly \( g_\alpha(x) \to g(x) \), as \( \alpha \to 1 \). So \( z_\alpha(x) \to z(x) \), defined by (6.2.7), provided this function is well defined, which means that the series converges.

Consider the series

$$H(x) = \sum_{n=2}^{+\infty} f^{*(n-1)}.$$

We prove by induction that

$f^{*(n-1)}(x) \le ||f|| F^{n-2}(x), \forall n \ge 2$

therefore

$H(x) \le ||f|| \sum_{n=2}^\infty F^{n-2}(x) = \frac{||f||}{F(x)}$

This bound is well defined for any \(x \ge 0\). Note that this requires the implicit assumption that \(f(x) > 0, \forall x\). Therefore we can assert that

$u'_\alpha(x) \to h - c + z(x).$

Consider \(x > S\). We can also assume that \(x > S_\alpha\). Therefore

$u_\alpha(x) - u_\alpha(S_\alpha) = (h-c)(x-S_\alpha) + \int_{S_\alpha}^x z_\alpha(\xi) \, d\xi$
\(\to (h-c)(x-S) + \int_S^x z(\xi) \, d\xi\)

and from (6.2.8), we deduce

(6.2.12) \(u_\alpha(x) - \frac{\rho}{1-\alpha} \to u(x) = (h-c)(S-E(S-D)^+) + (h-c)(x-S) + \int_S^x z(\xi) d\xi,\)

If \(x < S\), we obtain similarly

(6.2.13) \(u_\alpha(x) - \frac{\rho}{1-\alpha} \to u(x) = (h-c)(x-E(S-D)^+),\)

and both formulas coincide for \(x = S\), with the first formula (6.2.6). To prove (6.2.9), we write for \(x \le S\),

$u(S) - u(x) = (h-c)(S-x),$

and we note that

$u(S) = hS + pE(S-D)^- - \rho.$

We then conclude easily. To prove (6.2.8), we note that we can write

$z(x) = g(x) + Ez(x-D)$
$= g(x) + E[z(x-D) \mathbf{1}_{x>D}].$

Replacing \(z(x)\) by \(u'(x) - (h-c)\) we get

$u'(x) - (h-c) = g(x) + E[u'(x-D) \mathbf{1}_{x>D}] - (h-c)F(x).$

But we can see that, for \(x \ge S\), we have

$g(x) = c + (h-c)F(x) - pF(x),$

so the previous relation becomes

$u'(x) = h - pF(x) + E[u'(x-D) \mathbf{1}_{x>D}],$

which can also be written as

$u'(x) = h + \frac{d}{dx} pE(x-D)^- + \frac{d}{dx} Eu((x-D)^+),$

Integrating between \(S\) and \(x\) and using the fact that \(Eu((S-D)^+) = 0\), as well as the value of \(u(S)\), we conclude easily to obtain (6.2.8).

The proof has been completed.

### 6.2.2. PROBABILISTIC INTERPRETATION.

Suppose we apply a Base stock policy, with base stock S. Consider \( x \le S \) and the following sequence (where \( LS_n \) represents the lost sales of period n:

- \( y_1 = x, v_1 = S - x, LS_1 = (S - D_1)^- \);
- \( y_2 = (S - D_1)^+, v_2 = S - (S - D_1)^+, LS_2 = (S - D_2)^+ \);
- \(\dots\)
- \( y_{n+1} = (S - D_n)^+, v_{n+1} = (S - D_n)^+, LS_{n+1} = (S - D_{n+1})^+ \).

Except \( y_1 \) all the random variables \( y_n, n \ge 2 \) have the same probability distribution, which is simply

(6.2.14) \( \bar{F}(S)\delta(\eta) + f(S - \eta) 1_{\eta < S} d\eta \).

The process \( y_n \) is clearly ergodic and the formula (6.2.14) gives the invariant measure.

If we discount with rate \( \alpha \) we obtain the cost

\( u_\alpha(x) = hx + c(S - x) + pE(S - D_1)^- + \sum_{n=1}^\infty \alpha^n E[c(S - (S - D_n)^+) + h(S - D_n)^+ + p(S - D_{n+1})^-] \),

therefore

\( u_\alpha(x) = (h - c)(x - E(S - D)^+) + \frac{\rho}{1 - \alpha}, \)

and we obtain the value of \( u(x) \). The quantity

(6.2.15) \( E[c(S - (S - D)^+) + h(S - D)^+ + p(S - D)^-] \),

represents the cost of one period, except the first one. Minimizing in S gives the optimal base stock. This gives the interpretation of \( \rho \). Consider now the case \( x > S \). We define first

\( y_{n+1} = y_n - D_n, y_1 = x, \)

\( LS_n = (y_n - D_n)^- \).

Let

\( \tau = \inf\{n \ge 1 | y_n \le S\}; \)

Starting at period \( \tau \) we are back in the situation where the stock is below S and we proceed as follows

- \( y_\tau = y_\tau, v_\tau = S - y_\tau, LS_\tau = (S - D_\tau)^- \),
- \( y_{\tau+n} = (S - D_{\tau+n-1})^+, v_{\tau+n} = S - (S - D_{\tau+n-1})^+, LS_{\tau+n} = (S - D_{\tau+n})^- \).

The corresponding cost is given by

\( u_\alpha(x) = E \left[ \sum_{n=1}^{\tau-1} \alpha^{n-1} (hy_n + p(y_n - D_{n-1})^- \right] + E \alpha^{\tau-1} [(h - c)y_\tau + cS + p(S - D_\tau)^-] + \sum_{n=1}^\infty E \alpha^{\tau-1+n} [c(S - (S - D_{\tau+n-1})^+) + h(S - D_{\tau+n-1})^+ + p(S - D_{\tau+n})^-] \),

hence also by appropriate conditioning

$$u_\alpha(x) - \frac{\rho}{1-\alpha} = E \left[ \sum_{n=1}^{\tau-1} \alpha^{n-1} (hy_n + p(y_n - D_{n+1})^- - \rho) \right] + E \alpha^{\tau-1} (h - c)(y_\tau - E(S - D)^+)$$

and letting \(\alpha\) tend to 1 we obtain

$$u_\alpha(x) - \frac{\rho}{1-\alpha} \to E \left[ \sum_{n=1}^{\tau-1} (hy_n + p(y_n - D_{n+1})^- - \rho) \right] + E(h-c)(y_\tau - E(S - D)^+).$$

Replacing \(-(h-c)E(S-D)^+\) by \(cS + pE(S-D)^- - \rho\), we obtain the probabilistic interpretation of the function \(u(x)\) as defined by (6.2.8). (6.2.9).

## 6.3. ERGODIC CONTROL OF INVENTORIES WITH BACKLOG

### 6.3.1. CONVERGENCE RESULTS.

We consider the situation of Theorem 5.6.1. The functional equation is given by

(6.3.1) \(u_\alpha(x) = -cx + hx^+ + px^- + \inf_{v \ge 0} [c(x+v) + \alpha E u_\alpha(x+v-D)].\)

We know that the optimal feedback is defined by a Base stock policy \(S_\alpha\) with

(6.3.2) \(F(S_\alpha) = \frac{\alpha(h+c)-c}{\alpha(h+p)},\)

which has a unique solution provided \(\alpha > \frac{c}{p+c}\). This will be assumed since we will let \(\alpha\) tend to 1.

Our objective is to prove the

### Theorem 6.5.

Define \(S\) uniquely by

(6.3.3) \(F(S) = \frac{h}{p+h},\)

the number \(\rho\) by

(6.3.4) \(\rho = c\bar{D} + pE(S - D)^- + hE(S - D)^+,\)

and

(6.3.5) \(g(x) = (h - (h + p)\bar{F}(x))^+,\)

then \(S_\alpha \uparrow S\) and

\(u_\alpha(x) - \frac{\rho}{1 - \alpha} \to u(x),\)

where \(u\) is defined by

(6.3.6) \(\begin{cases} u(S) = (h - c)\bar{D} - (p + h)E(S - D)^- \\ u'(x) = -c + h\bar{I}_{x>0} - p\bar{I}_{x<0} + z(x) \end{cases},\)

where

(6.3.7) \(z(x) = \sum_{n=1}^{+\infty} g * f^{*(n-1)}(x).\)

The function u is also solution of

(6.3.8) \( u(x) = hx - \rho + Eu(x - D), \quad \forall x > S \)
(6.3.9) \( u(x) = c(S - x) - \rho + hx^+ + px^-, \quad \forall x \le S \)

PROOF. From the formula (6.3.2) the convergence of \( S_\alpha \) to \( S \) is clear. Noting that

\( F(S_\alpha) = \frac{p+c}{p+h} - \frac{c}{\alpha(h+p)}, \)

we see that \( S_\alpha \) increases with \( \alpha \). Moreover an easy calculation shows that

\( u_\alpha(S_\alpha) = hS_\alpha^+ + pS_\alpha^- + \frac{\alpha}{1-\alpha}[c\bar{D} + hE((S_\alpha - D)^+) + pE((S_\alpha - D)^-)], \)

from which it follows, thanks to the choice of \( \rho \) that

\( u_\alpha(S_\alpha) - \frac{\rho}{1-\alpha} \to hS - [c\bar{D} + hE((S - D)^+) + pE((S - D)^-)]. \)

Now from Theorem 5.6, we have

\( u'_\alpha(x) = -c + h\mathbb{I}_{x>0} - p\mathbb{I}_{x<0} + z_\alpha(x), \)

where

\( z_\alpha(x) = \sum_{n=1}^\infty \alpha^{n-1} g_\alpha * f^{*(n-1)}(x), \)

with

\( g_\alpha(x) = (c(1 - \alpha) + \alpha h - \alpha(h + p)F(x))^+. \)

Again we can see that \( z_\alpha(x) \to z(x) \), defined in equation (6.3.7). So we obtain (6.3.6). To prove (6.3.9) we use \( z(x) = 0, \forall x \le S \), hence

\( u'(x) = -c + h\mathbb{I}_{x>0} - p\mathbb{I}_{x<0}, \forall x \le S. \)

Integrating between \( x \) and \( S \), and using \( u(S) = hS - \rho \), formula (6.3.9) follows. To prove (6.3.8), we note that

\( u'(x) = h + Eu'(x - D), \forall x > S. \)

Next we verify that \( Eu(S - D) = 0 \). This follows from (6.3.8), applied at \( x = S - D \) and taking the mathematical expectation. So integrating between \( S \) and \( x \), we obtain easily (6.3.9).

The proof has been completed. Note that \( u \in C^1 \), except for \( x = 0 \).

### 6.3.2. PROBABILISTIC INTERPRETATION.

We proceed as in the no shortage case. We first interpret the number \( \rho \). Consider one period, starting with an inventory equal to \( S \). At the end of the period the inventory is \( S - D \). In order to face the new demand with an inventory equal to \( S \) in the next period, we have to order \( D \). At the end of the period we pay for storage \( h(S - D)^+ \) and if we have shortage we pay \( pE(S - D)^- \). Therefore the expected cost on a period is

\( cD + hE(S - D)^+ + pE(S - D)^-, \)

which is exactly \( \rho \). To find the optimal \( S \) we minimize this expression in \( S \).
