Now take $0 < x_1 < x_2 < s$, by $K$ convexity again we have

$K + f(S) - f(x_2) \ge \frac{S - x_2}{x_2 - x_1} (f(x_2) - f(x_1)),$

and since the left hand side is negative, we get $f(x_2) - f(x_1) < 0$.

Let now $s < x < S$ we have

$f(s) - f(x) = K + f(S) - f(x) \ge \frac{S - x}{x - s} (f(x) - f(s)),$

which implies $f(s) > f(x)$. Finally, for $s < x < y$ we can write

$K + f(y) - f(x) \ge \frac{y - x}{x - S} (f(x) - f(S)) \ge 0.$

The proof has been completed.

Consider

$h(x) = \inf_{\eta \ge x} [f(\eta) + K \mathbf{1}_{\{\eta > x\}}],$

then

# **Exercise 9.1.** Show that

$h(x) = \begin{cases} f(x), & \text{if } s = 0 \ f(s) = K + f(s), & \text{if } 0 < x \le s, \ f(x), & \text{if } x \ge s \end{cases}$

and that $h(x)$ is $K$ convex and continuous. Note that $h(x) = f(\max(s, x))$.

# **Exercise 9.2.**

Show that when $s > 0$

$h(x) \le h(y) + K, \forall x < y$

We apply this theory to the functional equation (9.2.5). We set

$G(\eta) = c\eta + p\mathbb{E}((\eta - D)^-) + \alpha \mathbb{E}u((\eta - D)^+),$

then equation (9.2.5) can be written as

(9.2.32) $u(x) = (h - c)x + \inf_{\eta \ge x} \{K \mathbf{1}_{\{\eta > x\}} + G(\eta)\}.$

We shall prove that

$u(x), G(x) \text{ are } K - \text{convex}.$

Clearly $G(x) \uparrow \infty$ as $x \uparrow \infty$. In order to guarantee that $G(x)$ is continuous, we shall make the technical assumption

(9.2.33) $f \text{ is continuous}.$

**Exercise 9.3.** Show that whenever (9.2.33) is satisfied, then $Eu((y - D)^+)$ is continuous, hence $G(y)$ is also continuous. Since $G(x)$ is $K$-convex, continuous and tends to $\infty$ as $x$ tends to $\infty$, the optimal feedback is described by an $s, S$ policy.

**Theorem 9.6.** Under the assumptions of Theorem 9.9 and (9.12), (9.2.21), (9.2.33) the solution of the functional equation (9.2.5) is continuous, $K$-convex and tends to $\infty$ as $x \uparrow \infty$. The optimal feedback is defined by an $s, S$ policy.