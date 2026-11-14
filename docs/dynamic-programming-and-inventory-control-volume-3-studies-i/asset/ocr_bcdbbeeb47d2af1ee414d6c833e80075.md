PROOF. Let us prove uniqueness. It means that a bounded solution of

$AH_s(x) + \alpha H_s(x) = 0 \quad x > s$
$H_s(x) = 0 \quad x \le s$

is 0. This follows from Maximum principle considerations. We have

$AH_s(x) + \alpha H_s(x) = -\frac{1}{2}\sigma^2 H_s''(x) + \nu H_s'(x) + (\lambda + \alpha)H_s(x) - \lambda \int_0^{x-s} H_s(x-\xi)\mu(\xi)d\xi.$

Suppose $H_s(x)$ becomes strictly positive. Let us prove that it cannot have a local maximum. If it has a local maximum $x^* > s$ then we may assume that it is the smallest one. In such a point

$H_s'(x^*) = 0, \quad H_s^*(x^*) < 0,$

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