hence Q(x) is an increasing function with

$$Q(-\infty) = \frac{2}{\beta \sigma_2^2}(p - \alpha c), Q(x) = -\frac{2}{\beta \sigma_2^2}(h + \alpha c), \forall x \ge 0$$

**Proposition 15.2.** Assuming (15.3.17), the function G_s(x) defined by (15.3.15) attains its infimum for x > s. Taking the smallest minimum, we define in a unique way a function S(s) such that

$$(15.3.19) \quad G_s(S(s)) = \inf_{\eta \ge s} G_s(\eta).$$

**PROOF.** Let x_0 < 0 the unique point such that Q(x_0) = 0. It is given explicitly by

$$\exp -\beta_2 x_0 = \frac{p - \alpha c}{h + p}.$$

Then for s > x_0 we have H_s(x) > 0. Therefore G_s(x) is increasing for x > s, and the minimum is attained in s. So in this case, S(s) = s. We next assume that s < x_0. For s < x < x_0 we have H_s(x) < 0 and thus G_s(x) decreases on (s, x_0). Considering x > 0 we can write

$$H_s(x) = \int_s^x \Gamma(x - \xi) Q(\xi) d\xi = -\frac{2}{\sigma^2 \beta_2}(h + \alpha c) \int_0^x \Gamma(\xi) d\xi.$$

Using the estimates on \Gamma(x) and the minimum value of Q(x) we can show easily the inequality

$$H_s(x) \ge \frac{2}{\sigma^2 \beta_2}(p - \alpha c) \frac{1 - \exp -\beta_1 s}{\beta_1} \exp -\beta_1 x - \frac{2}{\sigma^2 \beta_2}(h + \alpha c) \frac{1 - \exp -\beta_0 x}{\beta_0}, \forall x \ge 0.$$

Therefore also

$$\liminf_{x \to +\infty} H_s(x) \ge -\frac{2}{\sigma^2 \beta_2 \beta_0}(h + \alpha c),$$

which implies also G_s(x) \to +\infty as x \to +\infty. Collecting results we see that G_s(x) attains its infimum for x > s. Taking the smallest infimum we define in a unique way S(s). Necessarily S(s) minimizes G_s(x), hence

Consider s < x_0, S(s) minimizes G_s(x), hence

$$G'_s(S(s)) = H_s(S(s)) = 0; G''_s(S(s)) = H'_s(S(s)) > 0.$$

Also

$$S'(s) H'_s(S(s)) + \frac{\partial H_s}{\partial s}(S(s)) = 0.$$

Since

$$\frac{\partial H_s}{\partial s}(S(s)) = -\Gamma(S(s) - s) Q(s) > 0,$$

we obtain

$$(15.3.20) \quad S'(s) < 0, \text{ if } s < x_0 \quad S'(s) = 1, \text{ if } s > x_0 .$$

Let us check that

$$(15.3.21) \quad S'(x_0 - 0) = -1.$$

Indeed, since s < x_0 < S(s) we can write

$$\int_s^{x_0} \Gamma(S(s) - \xi) Q(\xi) d\xi + \int_{x_0}^{S(s)} \Gamma(S(s) - \xi) Q(\xi) d\xi = 0.$$