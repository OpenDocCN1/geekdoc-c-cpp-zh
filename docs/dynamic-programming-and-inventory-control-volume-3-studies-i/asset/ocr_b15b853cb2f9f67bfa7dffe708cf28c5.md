We can now proceed with a contradiction argument, to show that a point like \(x'\) cannot exist. We recall that for \(x > s\) the function \(G_s(x)\) satisfies

\(-\frac{1}{2}\sigma^2 G_s''(x) + \nu G_s'(x) + (\alpha + \lambda)G_s(x) - \lambda \int_0^\infty G_s(x-\xi)\mu(\xi)d\xi = l(x),\)

with

\(l(x) = g(x) + cv + cx\tilde{\xi}.\)

Recalling that \(x_0 < 0\), we examine two possibilities:

+   - If \(x_2 < 0\) then we write (15.4.12) at points \(x_1\) and \(x_2\). We have

\(-\frac{1}{2}\sigma^2 G_s''(x_1) + \nu G_s'(x_1) + (\alpha + \lambda)G_s(x_1) - \lambda \int_0^\infty G_s(x_1-\xi)\mu(\xi)d\xi = l(x_1);\)

\(-\frac{1}{2}\sigma^2 G_s''(x_2) + \nu G_s'(x_2) + (\alpha + \lambda)G_s(x_2) - \lambda \int_0^\infty G_s(x_2-\xi)\mu(\xi)d\xi = l(x_2),\)

and we use

\(G_s'(x_1) = G_s'(x_2) = 0;\)
\(G_s''(x_1) > 0, \quad G_s''(x_2) < 0;\)
\(G_s(x_2) - G_s(x_2-\xi) > 0, \quad G_s(x_1) - G_s(x_1-\xi) < 0;\)
\((x_1) > l(x_2),\)

therefore necessarily \(G_s(x_1) > G_s(x_2)\) which is impossible.

+   - If \(x_2 \ge 0\) then we write (15.4.12) at points \(x_2\) and \(x_3\). We have

\(-\frac{1}{2}\sigma^2 G_s''(x_3) + \nu G_s'(x_3) + (\alpha + \lambda)G_s(x_3) - \lambda \int_0^\infty G_s(x_3-\xi)\mu(\xi)d\xi = l(x_3)\)

We have then

\(G_s'(x_3) = G_s'(x_2) = 0\)
\(G_s''(x_3) > 0 \quad G_s''(x_2) < 0\)
\(G_s(x_2-\xi) - G_s(x_3-\xi) \le G_s(x_2) - G_s(x_3)\)
\(l(x_2) < l(x_3),\)

it follows that \(G_s(x_2) - G_s(x_3) < 0\) which is also a contradiction. Hence a point like \(x'\) cannot exist, which proves that (15.4.3) is satisfied and completes the proof that the function \(G_s(x)\) solves the Q.V.I.

# 15.5. ERGODIC THEORY

# 15.5.1. NOTATION AND MODEL.

We want now let \(\alpha \to 0\). We will index the functions with \(\alpha\). So we have the quasi-variational inequality

\(\alpha G_\alpha(x) + \alpha G_\alpha(x) \le g_\alpha(x)\)
\(G_\alpha(x) \le K + \inf_{\eta > x} G_\alpha(\eta)\)

\((\alpha G_\alpha(x) + \alpha G_\alpha(x) - g_\alpha(x)) \left( G_\alpha(x) - K + \inf_{\eta > x} G_\alpha(\eta) \right) = 0,\)

with

\(g_\alpha(x) = f(x) + \alpha cx + cv + c\lambda\tilde{\xi},\)