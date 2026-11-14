simplify notation we drop the indices s,S. We use the notation H(x) for H_s(x), with the particular s. Consider the function

(9.2.23) \( u(x) = H(x) + (h - c)x + \frac{g(s)}{1 - \alpha} \).

Since H(x) is continuous, the function u(x) is continuous. Then u(x) satisfies

(9.2.24) \( u(x) = \begin{cases} (h - c)x + \frac{g(s)}{1 - \alpha}, & x \le s \\ hx + pE(x - D)^- + \alpha Eu(x - D)^+, & x \ge s \end{cases} \)

and also, from the choice of s

(9.2.25) \( K + \inf_{\eta \ge s} [u(\eta) + (c - h)\eta] = \frac{g(s)}{1 - \alpha}, \)

hence also

(9.2.26) \(\begin{aligned} u(s) + (c - h)s &= K + \inf_{\eta \ge s} [u(\eta) + (c - h)\eta] \\ &= K + u(S) + (c - h)S \end{aligned}\)

Since

\( u(x) = -(c - h)x + \frac{g(s)}{1 - \alpha}, \quad x \le s, \)

the function u(x) + (c - h)x is constant on 0, s. Therefore

\(\inf_{\eta \ge s} [(c - h)\eta + u(\eta)] = \inf_{\eta \ge s} [(c - h)\eta + u(\eta)], \quad \forall x \le s.\)

Hence the function u satisfies

\(\begin{aligned} u(x) &= M(u(x)), \forall x \le s \\ u(x) &= T(u(x)), \forall x \ge s \end{aligned}\)

So it remains to prove that

\(\begin{aligned} u(x) \le T(u(x)), \forall x \le s \\ u(x) \le M(u(x)), \forall x \ge s \end{aligned}\)

In terms of H the first inequality amounts to g_x(x) \ge 0, \forall x \le s. This is true since \mu(\xi) < 0, \forall x \le \xi < s < S. The second inequality is more involved. In terms of H it amounts to

(9.2.27) \( H(x) \le K + \inf_{\eta \ge x} H(\eta), \forall x \ge s. \)

To prove (9.2.27) we first notice that for x \ge s we have \inf_{\eta \ge x} H(\eta) \ge \inf_{\eta \ge s} H(\eta) \ge -K. So the inequality is certainly true whenever H(x) \le 0. Consider then the smallest number called x_0 for which H becomes positive. We have then

\( H(x_0) = 0, H(x) < 0 \quad \forall x, s < x < x_0. \)

We can claim that g_s(x_0) > 0. This follows from the relation g_s(x_0) = -\alpha E H(x_0 - D) and the properties of x_0 resulting from its definition. To proceed we note that the relation (9.2.15) implies

\( H(x) = g_x(x) + \alpha E H(x - D), \)

which holds for any x, provided that we extend by 0 the definition of H whenever x \le 0.