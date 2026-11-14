Integrating with respect to the invariant measure, and making use of its fundamental property we get

\(\int_{-\infty}^s (g(x)\mathbb{I}_{x>s} + g(s)\mathbb{I}_{x \le s})m(x)dx\)
\(= \alpha c\bar{D} + \int_{-\infty}^s [c(1-\alpha)x + \alpha h^+ + \alpha p^-]m(x)dx\)
\(+ c(1-\alpha) \int_{-\infty}^s (S-x)m(x)dx\)
\(= (1-\alpha) \int_{-\infty}^s H(x)m(x)dx + g(s) + H(s) \int_{-\infty}^s m(x)dx.\)

Therefore

\((1-\alpha) \int_{-\infty}^s J_x(V)m(x)dx = \int_{-\infty}^s (1-\alpha)(hx^+ + px^- - cx + H(x))m(x)dx\)
\(+(K+H(s)) \int_{-\infty}^s m(x)dx + g(s) + c\alpha \left[ \int_{-\infty}^s (S-x)m(x)dx - D \right].\)

Now we use the property

(9.3.38) \(\bar{D} = \int_{-\infty}^s (S-x)m(x)dx.\)

This follows from writing

\(\int_{-\infty}^s xm(x)dx = \int_{-\infty}^s [\mathbb{I}_{x>s}E(x-D) + \mathbb{I}_{x \le s}E(S-D)]m(x)dx,\)

which is a consequence of the fundamental property of the invariant measure.

Therefore, we obtain

(9.3.39) \(\int_{-\infty}^s J_x(V)m(x)dx = \int_{-\infty}^s (hx^+ + px^- - cx + H(x))m(x)dx\)
\(+ \frac{g(s)}{1-\alpha} + \frac{K+H(s)}{1-\alpha} \int_0^s m(x)dx.\)

We can show directly from formula (9.3.39) from the formulas giving \(J_x(V)\), formulas (9.3.27), (9.3.28). One needs to prove that the function \(\Gamma(x)\) satisfies the relation

(9.3.40) \(\Gamma(S-s) \int_{-\infty}^s m(dx) + (1-\alpha) \int_s^S \Gamma(x-s)m(dx) = 1,\)

which is similar to (9.2.71).

# 9.3.5. PARTICULAR CASE.

Consider the case \(f(x) = \beta \exp -\beta x\). We recall that

(9.3.41) \(\Gamma(x) = \frac{1}{1-\alpha} - \frac{\alpha}{1-\alpha} \exp -\beta(1-\alpha)x,\)

then

(9.3.42) \(\mu(x) = c(1-\alpha) + \alpha h - \alpha(p+h) \exp -\beta x^+,\)

and

(9.3.43) \(g(x) = c(1-\alpha)x + \alpha(hx^+ + px^-) + \alpha(c+p)\bar{D} + \alpha \frac{h+p}{\beta}(\exp -\beta x^+ - 1).\)