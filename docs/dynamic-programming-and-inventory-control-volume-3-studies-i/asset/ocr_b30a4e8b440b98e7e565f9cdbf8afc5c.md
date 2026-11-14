PROOF. We recall that

$$0 = K + \inf_{\eta > \alpha(z)} \int_{s(z)}^\eta \chi(\xi, z) d\xi.$$

Therefore if $s(z) < 0$ we can write

$$0 \le K + \int_0^0 \chi(\xi, z) d\xi$$

However for $s(z) < \xi < 0$, we have $\chi(\xi, z) \le c(1-\alpha) - \alpha p$, which implies (12.5.27) immediately.

Since $s_\alpha(z) > -m_\alpha$, we have successively

$$u(-m_\alpha, z) = (p+c)m_\alpha + K + G(S(z), z).$$

Set

$$\hat{y}_2 = S(z) - z_2, \quad \hat{v}_2 = \hat{v}(\hat{y}_2, z_2),$$

then

$$G(S(z), z) = cS(z) + \alpha E[u(\hat{y}_2, z_2)|z_1 = z].$$

Also we can write

$$u(\hat{y}_2, z_2) = h\hat{y}_2^+ + p\hat{y}_2^- + K \mathbf{1}_{\hat{v}_2 > 0} + c\hat{v}_2 + \alpha E[u(\hat{y}_2 + \hat{v}_2 - z_3, z_3)|z_2].$$

Therefore, we can write

(12.5.29) $$u(-m_\alpha, z) = (p+c)m_\alpha + K + cS(z) + \alpha E[h\hat{y}_2^+ + p\hat{y}_2^- + K \mathbf{1}_{\hat{v}_2 > 0} + c\hat{v}_2 + \alpha u(\hat{y}_2 + \hat{v}_2 - z_3, z_3)|z_1 = z].$$

We next have

$$u(-m_\alpha, z) \le p m_\alpha + \alpha E[u(-m_\alpha - z_2, z_2)|z_1 = z].$$

Furthermore

$$u(-m_\alpha - z_2, z_2) \le K + p(z_2 + m_\alpha) + c(\hat{y}_2 + \hat{v}_2 + z_2 + m_\alpha) + \alpha E[u(\hat{y}_2 + \hat{v}_2 - z_3, z_3)|z_2].$$

Combining the two inequalities we get

$$u(-m_\alpha, z) \le p m_\alpha + \alpha K + \alpha(p+c)m_\alpha + \alpha E[(p+c)z_2 + c(\hat{y}_2 + \hat{v}_2) + \alpha u(\hat{y}_2 + \hat{v}_2 - z_3, z_3)|z_1 = z].$$

Comparing with (12.5.29) we obtain inequality

$$cS(z) + \alpha(h-\alpha)E[(S(z)-z_2)^+|z_1 = z] = z] + \alpha(p+c)E[(S(z)-z_2)^+|z_1 = z]$$\n$$\le \alpha p m_\alpha + \alpha(p+c)E[z_2|z_1 = z],$$

from which we deduce easily (12.5.28), which completes the proof.

We deduce from the Lemma that if $\alpha p > c + \alpha(h-c)$ one has also

(12.5.30) $$|s_\alpha(z)| \le \frac{\alpha(p+h)E[z_2|z_1=z] + \alpha p m_\alpha}{c + \alpha(h-c)}.$$

Since $\alpha \to 1$, we may assume $\alpha > \frac{1}{2}$ and thus if $c_0 = 0$

$$|s_\alpha(z)|, S_\alpha(z) \le m_0 = \frac{(p+h)c_1 + \frac{2Kp}{p-c}}{\min(c,h)}$$

We now state the