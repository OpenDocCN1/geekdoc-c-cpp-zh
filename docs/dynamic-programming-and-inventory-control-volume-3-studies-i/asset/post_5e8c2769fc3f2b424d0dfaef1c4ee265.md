
PROOF. Let us prove uniqueness. It means that a bounded solution of

$AH_s(x) + \alpha H_s(x) = 0 \quad x > s$
$H_s(x) = 0 \quad x \le s$

is 0. This follows from Maximum principle considerations. We have

$AH_s(x) + \alpha H_s(x) = -\frac{1}{2}\sigma^2 H_s''(x) + \nu H_s'(x) + (\lambda + \alpha)H_s(x) - \lambda \int_0^{x-s} H_s(x-\xi)\mu(\xi)d\xi.$

Suppose $H_s(x)$ becomes strictly positive. Let us prove that it cannot have a local maximum. If it has a local maximum $x^* > s$ then we may assume that it is the smallest one. In such a point

$H_s'(x^*) = 0, \quad H_s''(x^*) < 0,$

and

$\int_0^{x^*-s} H_s(x^* - \xi)\mu(\xi)d\xi \le H_s(x^*) \int_0^{x^*-s} \mu(\xi)d\xi \le H_s(x^*).$

Therefore $AH_s(x^*) > 0$, which is a contradiction. Therefore $H_s'(x) > 0$. Since $H_s(x)$ is bounded, we must have $H_s'(x) \to 0$ as $x \to +\infty$. Therefore there is a point $x^*$ such that $H_s'(x^*) < 0$. In such a point, necessarily $AH_s(x^*) > 0$, and we have a contradiction again. Therefore $H_s(x) \le 0$ and a similar reasoning shows that it cannot become strictly negative.

To prove existence, we shall construct an explicit solution. However, we need preliminaries. Let us denote

$\hat{\mu}(\pi) = \int_0^{+\infty} \exp \pi \xi \mu(\xi)d\xi, \quad \pi < \bar{\pi}$

We consider the function

$\chi(\pi) = -\frac{\sigma^2}{2}\pi^2 - \nu\pi + \lambda + \alpha - \lambda\hat{\mu}(\pi),$

for $\pi \le \bar{\pi}$. We first note that

$\chi(\bar{\pi}) = \chi(-\infty) = -\infty;$

$\chi'(\pi) = -\sigma^2\pi - \nu - \lambda \int_0^{+\infty} \xi \exp \pi \xi \mu(\xi)d\xi;$
$\chi''(\pi) = -\sigma^2 - \lambda \int_0^{+\infty} \xi^2 \exp \pi \xi \mu(\xi)d\xi < 0;$
$\chi'(\bar{\pi}) = -\infty, \quad \chi'(-\infty) = +\infty, \quad \chi'(0) < 0.$

Therefore $\chi'(\pi)$ is strictly decreasing from $+\infty$ to $-\infty$. There exists a unique $\pi_0 < 0$ such that $\chi'(\pi_0) = 0$. Hence $\pi_0$ is the maximum of $\chi(\pi)$. Since $\chi(0) = \alpha$, we get $\chi(\pi_0) > 0$. Therefore $\chi(\pi)$ has only two zeros $\beta_1$ and $\beta_2$ with

$\beta_2 < \pi_0 < 0 < \beta_1 < \bar{\pi}.$

Let also

$\chi_0(\pi) = -\frac{\sigma^2}{2}\pi^2 - \nu\pi + \lambda + \alpha,$

and let $\beta_0$ be the positive root of $\chi_0(\pi) = 0$. Since $\chi(\pi) < \chi_0(\pi)$, we have $\chi(\beta_0) < 0$ and thus

$\beta_1 < \beta_0 < \bar{\pi}.$

To proceed we introduce the following problem:

\(-\frac{1}{2}\sigma^2 \Gamma''(x) + \nu \Gamma'(x) + (\lambda + \alpha)\Gamma(x) - \lambda \int_0^x \Gamma(x-\xi)\mu(\xi)d\xi = 0, \quad \forall x > 0\)
\(\Gamma(0) = 1, \quad \Gamma(+\infty) = 0\)
(15.3.6)

We shall prove in Lemma 15.1 below that there exists one and only one solution of (15.3.6) such that

\(\exp -\beta_0 x < \Gamma(x) < \exp -\beta_1 x\)
(15.3.7)

We will also prove the property

\(\Gamma'(0) = \frac{2\nu}{\sigma^2} + \beta_2.\)
(15.3.8)

We can now exhibit the solution of (15.3.5), namely

\(H_s(x) = \int_s^x \Gamma(x-\xi)Q(\xi)d\xi,\)
(15.3.9)

with

\(Q(x) = \frac{2}{\sigma^2} \int_x^{+\infty} \exp \beta_2(\eta-x) g'(\eta)d\eta,\)
(15.3.10)

From the estimate (15.3.7) we check that \(H_s(x)\) remains bounded and a direct calculation shows that it is indeed a solution of equation (15.3.5).

Let us state the

**Lemma 15.1.** _There exists one and only one solution of equation_ (15.3.6) _such that_ (15.3.7) _holds._

**PROOF.** The uniqueness is proved by maximum principle considerations as for \(H_s(x)\) in Proposition 15.1. To prove the existence, we first check that

\(\underline{\Gamma}(x) = \exp -\beta_0 x \quad \overline{\Gamma}(x) = \exp -\beta_1 x,\)

satisfy

\(-\frac{1}{2}\sigma^2 \overline{\Gamma}''(x) + \nu \overline{\Gamma}'(x) + (\lambda + \alpha)\overline{\Gamma}(x) - \lambda \int_0^x \overline{\Gamma}(x-\xi)\mu(\xi)d\xi \ge 0;\)
(15.3.11)

\(-\frac{1}{2}\sigma^2 \underline{\Gamma}''(x) + \nu \underline{\Gamma}'(x) + (\lambda + \alpha)\underline{\Gamma}(x) - \lambda \int_0^x \underline{\Gamma}(x-\xi)\mu(\xi)d\xi \le 0.\)
(15.3.12)

We then consider the sequence

\(-\frac{1}{2}\sigma^2 \Gamma_{n+1}''(x) + \nu \Gamma_{n+1}'(x) + (\lambda + \alpha)\Gamma_{n+1}(x) = \lambda \int_0^x \Gamma_n(x-\xi)\mu(\xi)d\xi;\)
\(\Gamma_0(x) = \underline{\Gamma}(x),\)

with boundary conditions

\(\Gamma_n(0) = 1, \quad \Gamma_n(+\infty) = 0.\)

Suppose that

\(\underline{\Gamma}(x) \le \Gamma_n(x) \le \overline{\Gamma}(x),\)

then \(\Gamma_{n+1}(x)\) is easily obtained by solving a 2nd order differential equation, the important property is to check that

\(\Gamma_n(x) \le \Gamma_{n+1}(x) \le \overline{\Gamma}(x).\)

Let us prove it for $n = 0$. This amounts to

$\underline{\Gamma}(x) \le \Gamma_1(x) \le \overline{\Gamma}(x)$

which is easy to check, thanks to (15.3.11), (15.3.12) and the equation of $\Gamma_1(x)$.

Assuming the property holds at n, one checks immediately that it holds at n + 1. Therefore the sequence $\Gamma_n(x)$ is a monotone increasing sequence. The limit $\Gamma(x)$ is a solution of (15.3.6) and satisfies (15.3.7) per construction. Let us check (15.3.8).

We first check that $\Gamma'(+\infty) = 0$. Indeed, we write equation (15.3.6) as

$-\frac{1}{2}\sigma^2\Gamma''(x) + \nu\Gamma'(x) + (\lambda + \alpha)\Gamma(x) = \theta(x)$

with

$\theta(x) = \lambda \int_0^x \Gamma(x-\xi)\mu(\xi)d\xi$

and we can state the estimate

$0 \le \theta(x) \le \lambda\hat{\mu}(\beta_1) \exp-\beta_1 x$

Now we can obtain the solution of (15.3.13) as a second-order differential equation with right hand-side. Noting

$\bar{\beta}_0 = -\beta_0 - \frac{2\nu}{\sigma^2}$

which is the negative root of $\chi_0(x) = 0$, we obtain easily

$\Gamma(x) = C \exp-\beta_0 x + \frac{2}{\sigma^2(\beta_0 - \bar{\beta}_0)} \left[ \int_0^x \exp-\beta_0(x-\xi)\theta(\xi)d\xi + \int_x^{+\infty} \exp\bar{\beta}_0(\xi-x)\theta(\xi)d\xi \right]$

and

$\Gamma'(x) = -\beta_0 C \exp-\beta_0 x - \frac{2}{\sigma^2(\beta_0 - \bar{\beta}_0)} \cdot \left[ \bar{\beta}_0 \int_0^x \exp-\beta_0(x-\xi)\theta(\xi)d\xi + \bar{\beta}_0 \int_x^{+\infty} \exp\bar{\beta}_0(\xi-x)\theta(\xi)d\xi \right]$

But

$0 \le \int_0^x \exp-\beta_0(x-\xi)\theta(\xi)d\xi \le \frac{\lambda\hat{\mu}(\beta_1)}{\beta_0 - \beta_1}(\exp-\beta_1 x - \exp-\beta_0 x)$

$0 \le \int_x^{+\infty} \exp\bar{\beta}_0(\xi-x)\theta(\xi)d\xi \le \frac{\lambda\hat{\mu}(\beta_1)}{\beta_1 - \bar{\beta}_0} \exp-\beta_1 x$

which implies $\Gamma'(+\infty) = 0$. We can then test (15.3.6) with $\exp \pi x$, with $\pi < 0$. We set

$\hat{\Gamma}(\pi) = \int_0^{+\infty} \exp \pi x \Gamma(x) dx$

which is well defined.

Using boundary conditions, we compute easily

$\frac{\sigma^2}{2}(\Gamma''(0) - \pi) - \nu + \hat{\Gamma}(\pi)(\pi) = 0$

and applying this relation with $\pi = \beta_2$ we obtain the relation (15.3.8).

We must have $\Gamma'(0) < 0$. Let us check indeed this property:

Let us prove the property

(15.3.14) 
 \(\frac{2\nu}{\sigma^2} + \beta_2 < -\beta_1\)

which will imply $\Gamma'(0) < 0$. This follows from noting first \(\chi(-\frac{\nu}{\sigma^2}) < 0\). Therefore

\(-\frac{\nu}{\sigma^2} > \pi_0 \Rightarrow -2\frac{\nu}{\sigma^2} - \beta_2 > \beta_2.\)

Next

\(\chi(-\frac{\nu}{\sigma^2} - \beta_2) = \lambda \hat{\mu}(\beta_2) - \lambda \hat{\mu} (-\frac{\nu}{\sigma^2} - \beta_2) < 0.\)

Combining results, the inequality (15.3.14) follows immediately.

### 15.3.3. OBTAINING THE s, S POLICY.

We find now s, $G_s(x)$ solution of (15.3.3), (15.3.4). We first construct for any s, $G_s(x)$ solution of the first equation of (15.3.3) and of (15.3.4). For s fixed we simply define

(15.3.15) 
 \(G_s(x) = G_s(s) + \int_s^x H_s(\xi) d\xi, \, x > s\) 
 \(= G_s(s), \, x \le s\)

We define in this way a $C^1$ function, and (15.3.4) is clearly satisfied. Let us check that the first equation (15.3.3) is satisfied for a convenient choice of $G_s(s)$. The function is also $C^2$ for $x > s$. We reinterpret the first equation (15.3.3) using the definition of $G_s(x)$. We obtain, after rearrangements, for $x > s$

\(-\frac{\sigma^2}{2} H''_s(x) + \nu H'_s(x) + \alpha G_s(s) + (\lambda + \alpha) \int_s^x H_s(\xi) d\xi\) 
 \(-\lambda \int_0^{x-s} \mu(\xi) \left( \int_s^{x-\xi} H_s(\eta) d\eta \right) d\xi = g(x) + c\nu + c\lambda \tilde{\xi}.\)

On the other hand, from (15.3.3), by integration between s and x, we get

\(-\frac{\sigma^2}{2} H'_s(x) + \frac{\sigma^2}{2} H'_s(s) + \nu H_s(x) + (\lambda + \alpha) \int_s^x H_s(\xi) d\xi -\) 
 \(\lambda \int_0^{x-s} \mu(\xi) \left( \int_s^{x-\xi} H_s(\eta) d\eta \right) d\xi = g(x) - g(s).\)

Noting that $H'_s(s) = Q(s)$ and comparing the two relations we obtain the value of $G_s(s)$, namely

(15.3.16) 
 \(G_s(s) = \frac{\frac{c^2}{2} Q(s) + g(s) + c\nu + c\lambda \tilde{\xi}}{\alpha}.\)

To proceed we make the standard assumption

(15.3.17) 
 \(p - ac > 0.\)

We can give an explicit formula for $Q(x)$, namely

(15.3.18) 
 \(Q(x) = \frac{2}{\beta_2 \sigma^2} (p - ac - (h + p) \exp \beta_2 x^{-}),\)

therefore we have

\(Q'(x) = \frac{2(h+p)}{\sigma^2} \exp -\beta_2 x \mathbb{I}_{x<0},\)
