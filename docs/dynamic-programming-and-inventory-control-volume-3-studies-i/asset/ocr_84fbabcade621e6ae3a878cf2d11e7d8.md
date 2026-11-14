PROOF. The only thing which has to be proven is the $K$-convexity. It is sufficient to prove the $K$-convexity of the increasing sequence This is proved by induction. We note that

$$u_{n+1}(x) = (h-c)x + \inf_{\eta \ge x} \{K \mathbb{I}_{\eta > x} + G_n(\eta)\};$$

with

$$G_n(\eta) = c\eta + pE((\eta - D)^-) + \alpha E u_n((\eta - D)^+).$$

We prove by induction that the functions $u_n(x), G_n(x)$ are $K$-convex. Assume that they are continuous and $\to +\infty$ as $x \to +\infty$. From Theorem 9.5, we associate with $G_n(x)$ two numbers $s_n, S_n$. We have the representation

$$u_{n+1}(x) = (h-c)x + G_n(\max(x, s_n)).$$

From exercise 9.1 we deduce that $u_{n+1}$ is also $K$-convex and continuous. Also $u_{n+1}(x) \to +\infty$, as $x \to +\infty$. Then we have

$$G_{n+1}(x) = cx + pE((x-D)^-) + \alpha(h-c)E(x-D)^+) + \alpha E G_n(\max(x-D, s_n)).$$

The function

$$cx + pE((x-D)^-) + \alpha(h-c)E((x-D)^+) = (c(1-\alpha) + \alpha h)x + \alpha(h-c)D + (p+\alpha(h-c))E((x-D)^-)),$$

is convex, and $G_n(\max(x-D, s_n))$ is $K$-convex. It follows that $G_{n+1}(x)$ is $K$-convex. It is continuous and $\to +\infty$ as $x \to +\infty$.

This property is preserved, when going to the limit.

# 9.2.4. PROBABILISTIC APPROACH.

We are going to evaluate directly the cost corresponding to an arbitrary $s,S$ policy. We have the following

Theorem 9.7. Let $V_{s,S}$ be the control corresponding to an $s,S$ policy, defined by the feedback

$$V_{s,S} = \begin{cases} S-x, & \text{if } x \le s \\ 0, & \text{if } x > s \end{cases}$$

The corresponding cost is: For $x \le s$

$$J_x(V_{s,S}) = (h-c)x + \frac{g(s)}{1-\alpha} + \frac{K+H_1(S)}{(1-\alpha)\Gamma(S-s)}.$$

For $x > s$, one has

$$J_x(V_{s,S}) = (h-c)x + H_s(x) + \frac{g(s)}{1-\alpha} + (1-(1-\alpha)\Gamma(x-s)) \frac{K+H_1(S)}{(1-\alpha)\Gamma(S-s)}.$$

This function is continuous except for $x=s$.

PROOF. Let $V_{s,S} = (v_1, \cdots, v_n \cdots)$ and $y_1, y_2 \cdots, y_n \cdots$ be the corresponding evolution of stocks. We have $y_1 = x$. We begin by considering the case

I- $x \le s$:

We then have $v_1 = S-x$. We set $\tau_1 = 1$ and we define the sequence of stopping times

$$\tau_{k+1} = \tau_k + 1 + \inf \{n \ge 0 | D_{\tau_k} + \cdots + D_{\tau_k+n} \ge S-s\}.$$

Recalling the filtration $\mathcal{F}^n = \sigma(D_1, \cdots, D_n), n \ge 1$ We have the