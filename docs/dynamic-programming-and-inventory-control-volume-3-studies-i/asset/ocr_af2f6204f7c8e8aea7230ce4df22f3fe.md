# 17.4. SOLUTION OF THE Q.V.I.

From the $a, A, B, b$ policy, we are going to construct $G^+(x), G^-(x)$ satisfying (17.2.11), (17.2.12), (17.2.13). We define

(17.4.1) 
$G^+_{ab}(x) = G^+_{ab}(a), \forall x \le a; \quad G^+_{ab}(x) = G^+_{ab}(a) + \int_a^x H^+_{ab}(\xi) d\xi, \forall x \ge a$

(17.4.2) 
$G^-_{ab}(x) = G^-_{ab}(b), \forall x \ge b; \quad G^-_{ab}(x) = G^-_{ab}(b) - \int_x^b H^-_{ab}(\xi) d\xi, \forall x \le b,$

with

(17.4.3) 
$G^+_{ab}(a) = \frac{g^+(a) - c^+ \mu + \frac{\sigma^2}{2}(H^+_{ab})'(a)}{\alpha};$

(17.4.4) 
$G^-_{ab}(b) = \frac{g^-(b) + c^- \mu + \frac{\sigma^2}{2}(H^-_{ab})'(b)}{\alpha}.$

We first check that

(17.4.5) 
$G^+_{ab}(x) - G^-_{ab}(x) = (c^+ + c^-)x.$

Since

$(G^+_{ab})'(x) - (G^-_{ab})'(x) = H^+_{ab}(x) - H^-_{ab}(x) = c^+ + c^-,$

it is sufficient to check that

(17.4.6) 
$G^+_{ab}(a) - G^-_{ab}(a) = (c^+ + c^-)a.$

Using

$$
G^-_{ab}(a) = G^-_{ab}(b) - \int_a^b H^-_{ab}(\xi) d\xi \\
= G^-_{ab}(b) - \int_a^b H^+_{ab}(\xi) d\xi + (c^+ + c^-)(b - a),
$$

and formulas (17.4.3), (17.4.4) we must check the relation

$$
\begin{aligned}
g^+(a) - c^+ \mu + \frac{\sigma^2}{2}(H^+_{ab})'(a) \\
= g^-(b) + c^- \mu + \frac{\sigma^2}{2}(H^-_{ab})'(b) - a \int_a^b H^+_{ab}(\xi) d\xi + \alpha(c^+ + c^-)b,
\end{aligned}
$$

or

$$
-\frac{\sigma^2}{2}((H^-_{ab})'(b) - (H^+_{ab})'(a)) + \alpha \int_a^b H^+_{ab}(\xi) d\xi - (c^+ + c^-) \mu = f(b) - f(a) + \alpha c^+(b - a),
$$

which follows immediately from (17.3.6) after integrating between $a$ and $b$. The functions $G^+_{ab}(x)$ and $G^-_{ab}(x)$ satisfy (17.3.1), (17.3.2). (17.3.3). We then define

We note that

$$
\begin{aligned}
AG^+(x) + \alpha G^+(x) &= g^+(x) - c^+ \mu, & \forall a < x < b \\
G^+(x) &= G^+_{ab}(a), & \forall x \le a \\
G^+(x) &= G^-_{ab}(b) + (c^+ + c^-)x, & \forall x \ge b
\end{aligned}
$$