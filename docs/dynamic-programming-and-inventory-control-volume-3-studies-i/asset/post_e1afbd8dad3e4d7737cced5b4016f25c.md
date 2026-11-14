
hence Q(x) is an increasing function with

$$Q(-\infty) = \frac{2}{\beta \sigma_2^2}(p - \alpha c), Q(x) = -\frac{2}{\beta \sigma_2^2}(h + \alpha c), \forall x \ge 0$$

### Proposition 15.2.
Assuming (15.3.17), the function G_s(x) defined by (15.3.15) attains its infimum for x > s. Taking the smallest minimum, we define in a unique way a function S(s) such that

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

As \( s \uparrow x_0 \) we have \( S(s) \downarrow x_0 \). In the two integrals

\(\Gamma(S(s) - \xi) \simeq 1, \quad Q(\xi) \simeq Q'(x_0)(\xi - x_0),\)

which implies

\((s - x_0)^2 \simeq (S(s) - x_0)^2,\)

and taking account of the signs we get

\(x_0 - s \simeq S(s) - x_0,\)

hence

\(\frac{S(s) - x_0}{s - x_0} \to -1,\)

which implies the result.

We can turn to the problem of finding \( s \) such that the second equation (15.3.3) is satisfied. Since we look for a single number, we need one equation. We write

\(G_*(s) = K + \inf_{\eta > s} G_*(\eta),\)

which is equivalent to

(15.3.22) \(0 = K + \int_s^{S(s)} H_s(\eta) d\eta.\)

It is then natural to study the function

\(\gamma(s) = \int_s^{S(s)} H_s(\eta) d\eta,\)

we have \(\gamma(s) = 0\) for \( s \ge x_0 \) and for \( s < x_0 \)

\(\gamma'(s) = \int_s^{S(s)} \frac{\partial H_s}{\partial s}(\eta) d\eta = -Q(s) \int_s^{S(s)} \Gamma(\eta - s) d\eta > 0.\)

Note also that \(\gamma(s)\) is \(C^1\). Remembering the estimate on \(\Gamma(x)\) we obtain the estimate

\(\gamma'(s) \ge -\frac{Q(s)}{\beta_0}(1 - \exp -\beta_0(S(s) - s)) \ge -\frac{Q(s)}{\beta_0}(1 - \exp -\beta_0(x_0 - s)).\)

Let us take \( s < s_1 < x_0 \), since \( Q(s) \) increases we get easily

\(\gamma'(s) \ge -\frac{Q(s_1)}{\beta_0}(1 - \exp -\beta_0(x_0 - s_1)) > 0.\)

This implies that \(\gamma(s) \to -\infty\) as \( s \to -\infty \). Therefore it is strictly monotone increasing from \(-\infty\) to 0, as \( s \) increases from \(-\infty\) to \( x_0 \). It follows that there exists a unique \( s < x_0 \) such that \(\gamma(s) = -K\). We can now state the

### Theorem 15.1.
We assume (15.2.4) (15.3.17). Then there exists a unique pair \( s, G_*(s) \) such that \( G_* \in C^1 \) and (15.3.3), (15.3.4) are satisfied.

**PROOF.** We have proved that the number \( s \) such that \(\gamma(s) = -K\) and the corresponding function \( G_*(x) \) defined by (15.3.15), (15.3.16) satisfy the (15.3.3), (15.3.4). It is unique since its derivative must coincide with \( H_s(x) \) which is uniquely defined by (15.3.5), and the value \( G_*(s) \) is uniquely defined by (15.3.16). Furthermore, because of the second relation (15.3.3), the number \( s \) must satisfy \(\gamma(s) = -K\), which has a unique solution. \(\square\)

Setting \( S(s) = S \) for the unique value \( s \) defined in Theorem 15.1, we obtain the \( s, S \) policy.

## 15.4. SOLVING THE Q.V.I

It remains to show that the s,S policy solves the problem. This amounts to showing that the function G_s(x) defined by (15.3.3), (15.3.4) solves the Q.V.I. (15.3.1), (15.3.2).

### Theorem 15.2.
Same assumptions as in Theorem 15.1. The function G_s(x) defined by (15.3.3), (15.3.4) solves the Q.V.I. (15.3.1), (15.3.2).

**PROOF.** We first note that

$$ \inf_{\eta > x} G_s(\eta) = \inf_{\eta > s} G_s(\eta), \quad \forall x \le s. $$

Indeed we note that for x < \eta < s we have

$$ G_s(\eta) = G_s(s) > \inf_{\eta > s} G_s(\eta). $$

Therefore the function G_s(x) satisfies the complementarity slackness condition (15.3.2). It remains to show that it satisfies the inequalities (15.3.1). This amounts to

(15.4.1) \( A G_s(x) + \alpha G_s(x) \le g(x) + c\nu + c\lambda\xi \quad x \le s; \)

(15.4.2) \( G_s(x) \le K + \inf_{\eta > x} G_s(\eta) \quad x \ge s. \)

We begin with (15.4.1). Since G_s(x) = G_s(s) for x \le s, the inequality (15.4.1) amounts to

$$ \alpha G_s(s) \le g(x) + c\nu + c\lambda\xi \quad x \le s, $$

and from the definition of G_s(s) we get

$$ \frac{\sigma^2}{2} Q(s) + g(s) \le g(x) \quad x \le s, $$

which is true since Q(s) \le 0 and g(s) \le g(x) \quad x \le s \le 0.

We turn now to (15.4.2). Define

$$ B_s(x) = G_s(x) - \inf_{\eta > x} G_s(\eta). $$

We want to show that

(15.4.3) \( B_s(x) \le K, \quad \forall x \ge s. \)

We begin with s \le x \le x_0. The function G_s(x) decreases on (s, x_0), therefore

$$ \begin{aligned} G_s(x) &\le G_s(s) = K + \inf_{\eta > s} G_s(\eta) \\ &\le K + \inf_{\eta > x} G_s(\eta), \end{aligned} $$

and (15.4.3) is satisfied. We can then assume x > x_0. Suppose there exists a point x' > x_0 such that B_s(x') \ge K. We can assume it is the first point such that this occurs. Necessarily

$$ B_s(x') = K, \quad B_s(x) < K, \forall s < x < x' $$

Consider G_s(\eta), \eta > x'. Its infimum is attained, since G_s(x) \to +\infty, as x \to +\infty. Taking the smallest minimum we define a unique point x_3 such that

(15.4.4) \( G_s(x_3) = \inf_{\eta \ge x'} G_s(\eta). \)

We can claim that \(x_3 \neq x'\) since

\(B_s(x') = G_s(x') - G_s(x_3) = K,\)

therefore \(x_3\) is a local minimum, which implies

(15.4.5) \(G'_s(x_3) = 0, \quad G''_s(x_3) > 0\)

Define next \(x_2\) to be the smallest maximum of \(G_s(\eta), \eta \le x_3\)

(15.4.6) \(G_s(x_2) = \sup_{\eta \le x_3} G_s(\eta)\)

The maximum is attained since

\(\sup_{\eta \le x_3} G_s(\eta) = \sup_{s \le \eta \le x_3} G_s(\eta),\)

and the function \(G_s(x)\) is continuous. Let us check that \(x_2 \ge x'\). Indeed suppose that \(x_2 < x'\). Then

\(\inf_{\eta \ge x_2} G_s(\eta) \le \inf_{\eta \ge x'} G_s(\eta),\)

and

\(G_s(x_2) - \inf_{\eta \ge x_2} G_s(\eta) \ge G_s(x') - \inf_{\eta \ge x'} G_s(\eta) = K\)

which contradicts the definition of \(x'\). Moreover \(x_2 \neq x_3\) since

\(G_s(x_2) - G_s(x_3) \ge G_s(x') - G_s(x_3) = K.\)

Therefore \(x_2\) is also a local maximum and we have

(15.4.7) \(G'_s(x_2) = 0 \quad G''_s(x_2) < 0.\)

So we have \(x' \le x_2 < x_3\). Let us prove the property

(15.4.8) \(G_s(x) - G_s(y) \le G_s(x_2) - G_s(x_3), \quad \forall x \le y \le x_3.\)

Indeed, if \(x < x'\) then

\(G_s(x) - G_s(y) \le G_s(x) - \inf_{\eta \ge x} G_s(\eta) < K \le G_s(x_2) - G_s(x_3),\)

and if \(x \ge x'\) then \(x' \le x \le y \le x_3\) and

\(G_s(x) - G_s(y) \le G_s(x_2) - G_s(x_3),\)

from the definition of \(x_2\) and \(x_3\).

Finally, let us define \(x_1\) such that

(15.4.9) \(G_s(x_1) = \inf_{\eta \le x'} G_s(\eta).\)

For the same reasons as in the definition of \(x_2\) the point \(x_1\) is well defined as the smallest minimum. Moreover \(x_1 \neq x'\). Indeed

\(G_s(x') = K + \inf_{\eta \ge x'} G_s(\eta),\)

and recalling that \(x' > x_0 > s\) and \(G_s(x)\) decreases on \((s, x_0)\)

\(G_s(x') \ge K + \inf_{\eta \ge x_2} G_s(\eta) = G_s(s) > G_s(x_0) \ge \inf_{\eta \le x'} G_s(\eta) = G_s(x_1),\)

consequently \(x_1\) is a local minimum and thus

(15.4.10) \(G'_s(x_1) = 0, \quad G''_s(x_1) > 0.\)

Note the sequence

(15.4.11) \(s < x_0 \le x_1 < x' \le x_2 < x_3.\)
