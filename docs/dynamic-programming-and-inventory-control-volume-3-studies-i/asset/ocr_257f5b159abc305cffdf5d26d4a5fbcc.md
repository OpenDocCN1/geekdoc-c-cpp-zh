To prove (9.3.22) we first notice that for \(x \ge s\) we have \(\inf_{\eta \ge x} H(\eta) \ge \inf_{\eta \ge x} H(\eta) = -K\). So the inequality is certainly true whenever \(H(x) \le 0\). Consider then the smallest number called \(x_0\) for which \(H\) becomes positive. We have then \(H(x_0) = 0, H(x) < 0 \forall x, s < x < x_0\).

We can claim that \(g_s(x_0) > 0\). This follows from the relation \(g_s(x_0) = -\alpha EH(x_0 - D)\) and the properties of \(x_0\) resulting from its definition.

Let \(\xi > 0\). We shall consider the domain \(x \ge x_0 - \xi\). We can write the inequality \(H(x) \le g_s(x) + \alpha E(H(x - D)\mathbb{I}_{x - D \ge x_0 - \xi}), \forall x \ge x_0 - \xi\), which follows from the fact that \(E(H(x - D)\mathbb{I}_{x - D \le x_0 - \xi}) \le 0\).

Define next \(M(x) = H(x + \xi) + K\).

Clearly \(M(x) \ge 0\). We can write thanks to this positivity \(EM(x - D) \ge E(M(x - D)\mathbb{I}_{x - D \ge x_0 - \xi})\).

Now for \(x \ge x_0 - \xi\) we have \(H(x + \xi) - \alpha EH(x + \xi - D) = g_s(x + \xi)\), hence \(M(x) - \alpha EM(x - D) = g_s(x + \xi) + K(1 - \alpha)\).

Therefore we have \(M(x) \ge g_s(x + \xi) + \alpha E(M(x - D)\mathbb{I}_{x - D \ge x_0 - \xi}), \forall x \ge x_0 - \xi\).

We can claim that \(g_s(x + \xi) \ge g_s(x), \forall x \ge x_0 - \xi\).

Indeed, note that \(g_s(x + \xi) \ge g_s(x_0) \ge 0\) since \(g\) is increasing on \([s, \infty)\). So the inequality is obvious, whenever \(x < s\). If \(x \ge s\) the inequality amounts to \(g(x + \xi) \ge g(x)\). This is true whenever \(x \ge s\), by the monotonicity property. So it remains the case \(s < x < s\). But in this case \(g_s(x) < 0\) and the inequality is satisfied.

Let us define \(Y(x) = H(x) - M(x)\). From the inequalities above we can state that \(Y(x) \le \alpha E(Y(x - D)\mathbb{I}_{x - D \ge x_0 - \xi}), \forall x \ge x_0 - \xi\), and \(Y(x_0 - \xi) \le -K\).

These two properties imply \(Y(x) \le 0, \forall x \ge x_0 - \xi\) Therefore we have obtained (9.3.22) \(\forall x \ge x_0 - \xi\) and in particular for \(x > x_0\) as desired. So \(u\) is solution of the functional equation (9.3.3) and thus is the value function. The feedback defined from the \(s, S\) policy is optimal.

Remark. Another proof of (9.3.22) We will give another proof of (9.3.22), using an idea originated by [3].

PROOF. We recall that \(H(x) = g_s(x) + \alpha EH(x - D)\), and we want to prove \(H(x) \le K + \inf_{\eta \ge x} H(\eta)\).