We check easily that for $x > 0$
$$ \beta_2(\exp \beta_1 x - 1) - \beta_1(\exp \beta_2 x - 1) < 0 $$
$$ \beta_1 \exp \beta_1 x (\exp \beta_2 x - 1) - \beta_2 \exp \beta_2 x (\exp \beta_1 x - 1) < 0 $$
therefore $Z'(x) \le 0$. Moreover $Z(0) = 0$ and $Z( +\infty ) = -\infty$. This implies the result.

From (17.5.3) we can assert that
(17.5.5) $$ A(a(b), b) - a(b) = \varpi \quad \text{if } A(a(b), b) \le 0. $$

Going back to the second condition we can write
(17.5.6) $$ \begin{aligned} h - \alpha c^- - (p+h) \frac{\beta_1 \exp \beta_2 b - \beta_2 \exp \beta_1 b}{\exp \beta_1 b - \exp \beta_2 b} &= (p - \alpha c^+) \ \frac{\exp \beta_1 b (a-b) (\exp \beta_2 \varpi - 1) - \exp \beta_2 b (a-b) (\exp \beta_1 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi} \end{aligned} $$

which defines $a$ as a function of $b$. Let us introduce the number
(17.5.7) $$ \varphi(\varpi) = \frac{\beta_1(\exp \beta_2 \varpi - 1) - \beta_2(\exp \beta_1 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi}, $$

then we have
$$ \varphi(\varpi) + \beta_1 = \frac{(\beta_1 - \beta_2)(\exp \beta_1 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi}; \quad \varphi(\varpi) + \beta_2 = \frac{(\beta_1 - \beta_2)(\exp \beta_2 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi}, $$

and (17.5.6) becomes after rearranging
(17.5.8) $$ L_\varpi(b-a) = \frac{\alpha(c^+ + c^-)(\beta_2 - \beta_1) + (p+h)[\beta_2(\exp \beta_1 b - 1) - \beta_1(\exp \beta_2 b - 1)]}{p - \alpha c^+}, $$

with
(17.5.9) $$ L_\varpi(x) = (\exp \beta_1 x - 1)(\varphi(\varpi) + \beta_2) - (\exp \beta_2 x - 1)(\varphi(\varpi) + \beta_1), \quad x \ge 0. $$

We can also give another formulation of equation (17.5.8). Recalling the definition of $Z^+(a, b)$ we check easily that (17.5.8) is equivalent to

(17.5.10) $$ \frac{Z^+(a, b)}{\exp \beta_1 b (a - b) - \exp \beta_2 b (a - b)} = \frac{\varphi(\varpi) - \alpha c^+}{\alpha(\beta_2 - \beta_1)}. $$

Now, we check easily that $\varphi(0) = 0$. From (17.3.13) we see also that $a_0(b)$ is the unique solution of (17.5.10) when $\varpi = 0$. More generally, we state the

# **Lemma 17.4.** For any $\varpi \ge 0$, there exists a unique $a_\varpi(b)$ solution of (17.5.10).

**PROOF.** It is of course equivalent to consider the equation (17.5.8). The function $L_\varpi(x)$ satisfies

$$ \begin{aligned} L'_\varpi(x) &= \beta_1(\varphi(\varpi) + \beta_2) \exp \beta_1 x - \beta_2(\varphi(\varpi) + \beta_1) \exp \beta_2 x; \ L''_\varpi(x) &= (\beta_1)^2(\varphi(\varpi) + \beta_2) \exp \beta_1 x - (\beta_2)^2(\varphi(\varpi) + \beta_1) \exp \beta_2 x. \end{aligned} $$

We note that

(17.5.11) $$ \varphi(\varpi) > 0, \quad \varphi(\varpi) + \beta_2 < 0, $$
hence $L''_\varpi(x)$ is decreasing and
$$ L'_\varpi(0) = (\beta_1 - \beta_2)\varphi(\varpi), \quad L'_\varpi( +\infty ) = -\infty. $$