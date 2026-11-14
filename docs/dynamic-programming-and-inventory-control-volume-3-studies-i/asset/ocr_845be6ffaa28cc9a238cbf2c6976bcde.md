Let \xi > 0. We shall consider the domain x \ge x_0 - \xi. Therefore values lower than s are possible and even negative values are possible. We can write the inequality

(9.2.28) \quad H(x) \le g_s(x) + \alpha E(H(x - D) \mathbb{1}_{x - D \ge x_0 - \xi}), \forall x.

This follows from the fact that

E(H(x - D) \mathbb{1}_{x - D \le x_0 - \xi}) \le 0.

Define next

M(x) = H(x + \xi) + K.

Clearly M(x) \ge 0. We can write thanks to this positivity

M(x) \ge \alpha E(M(x - D) \mathbb{1}_{x - D \ge x_0 - \xi}) + M(x) - \alpha E M(x - D).

Now for x \ge x_0 - \xi we have

H(x + \xi) - \alpha E H(x + \xi - D) = g_s(x + \xi),

hence

M(x) - \alpha E M(x - D) = g_s(x + \xi) + K(1 - \alpha).

Therefore we have

(9.2.29) \quad M(x) \ge g_s(x + \xi) + \alpha E(M(x - D) \mathbb{1}_{x - D \ge x_0 - \xi}), \forall x \ge x_0 - \xi.

We claim that

(9.2.30) \quad g_s(x + \xi) \ge g_s(x), \forall x \ge x_0 - \xi.

Indeed, note that g_s(x + \xi) \ge g_s(x_0) \ge 0 since g is increasing on [s, \infty). So the inequality is obvious, whenever x < s. If x \ge s the inequality amounts to g(x + \xi) \ge g(x). This is true whenever x \ge s, by the monotonicity property. So it remains the case x < s < \xi. But in this case g_s(x) < 0 and the inequality is satisfied.

Let us define Y(x) = H(x) - M(x). From the inequalities (9.2.29) and (9.2.30) we can state that

Y(x) \le \alpha E(Y(x - D) \mathbb{1}_{x - D \ge x_0 - \xi}), \forall x \ge x_0 - \xi,

and Y(x_0 - \xi) \le -K.

These two properties imply Y(x) \le 0, \forall x \ge x_0 - \xi Therefore we have obtained (9.2.27) \forall x \ge x_0 - \xi and in particular for x > x_0 as desired. We have completed the proof of the fact that the function u(x) characterized by the function H(x) and defined by (9.2.23) is a solution of (9.2.11) or (9.2.5). So it the value function.

Moreover the s, S policy is associated a feedback

(9.2.31) \quad \hat{v}(x) = \begin{cases} S - x, & \text{if } x \le s \\ 0, & \text{if } x > s \end{cases}

and it is an optimal feedback corresponding to u, which means

u(x) = l(x, \hat{v}(x)) + \alpha E u((x + \hat{v}(x) - D)^+).

To this feedback rule we can associate a probability P^{\hat{v}, x} for which the canonical process y_n evolves as

y_{n+1} = (y_n + \hat{v}_n - D_n)^+ ,