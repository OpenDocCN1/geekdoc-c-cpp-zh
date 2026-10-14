+ \frac{1}{\left(\Gamma(\alpha)\right)^2}\left\|\int_0^t (t-s)^{\alpha-1} \sigma(s,x(s))\mathrm{d}W(s)\right\|^2\right)
\le \frac{4}{\left(\Gamma(\alpha)\right)^2}\left[\left(\sup_{t\in I}\|A(t,x(t))\|_{L(X,X)}^2 \sup_{t\in I}\|x(t)\|_X^2 + \sup_{t\in I}\|f(t,x(t))\|^2
+ T^{-1}\int_0^t \|B\|_{L(U,X)}^2 \|u(s)\|_U^2 \mathrm{d}s\right]\frac{\tilde T^{2\alpha}}{(2\alpha-1)}
+ \left\|\int_0^t (t-s)^{\alpha-1} \sigma(s,x(s))\mathrm{d}W(s)\right\|^2\right).

Therefore using Itô isometry and hypotheses (H1), (H2), and (H3) we have

\mathbf{E}\sup_{t\in I}\|\Lambda x(t)-x_0\|^2 \le \frac{4}{\left(\Gamma(\alpha)\right)^2}\left[\left(\mathrm{EC}_1\sup_{t\in I}\|x(t)\|_X^2 + 2\mathrm{EL}_2\sup_{t\in I}\|x(t)\|^2
+ 2\sup_{t\in I}\|f(t,0)\|^2 + T^{-1}K_1\mathbf{E}\int_0^{\tilde T}\|u(s)\|_U^2 \mathrm{d}s\right]\frac{\tilde T^{2\alpha}}{(2\alpha-1)}
+ \frac{\tilde T^{2\alpha-1}}{(2\alpha-1)}\left[2\mathrm{EL}_3\sup_{t\in I}\|x(t)\|_X^2 + 2\sup_{t\in I}\|\sigma(t,0)\|^2\right]\right).

Using the definition of stopping time, Equation (18.5), and the fact that \|x(t)-x_0\|_X^2 \le r we obtain

\mathbf{E}\sup_{t\in I}\|\Lambda x(t)-x_0\|^2 \le \frac{4}{\left(\Gamma(\alpha)\right)^2}\left(\frac{\tilde T^{2\alpha}}{(2\alpha-1)}\left[6N\left(r+\|x_0\|^2\right)+2\sup_{t\in I}\|f(t,0)\|^2
+ K_1\mathbf{E}\int_0^{\tilde T}\|u(s)\|_U^2 \mathrm{d}s\right]+\frac{\tilde T^{2\alpha-1}}{(2\alpha-1)}\left[4N(r+\|x_0\|^2)+2\sup_{t\in I}\|\sigma(t,0)\|^2\right]\right)(5\tilde T K+1). \tag{18.6}

Also we have

\mathbf{E}\int_0^{\tilde T}\|u(t)\|_U^2 \mathrm{d}t \le 5\tilde T K\left(\|x_1\|_X^2+\|x_0\|_X^2+\left[(6N\tilde T+4N)(r+\|x_0\|^2)
+2\tilde T\sup_{t\in I}\|f(t,0)\|^2+2\sup_{t\in I}\|\sigma(t,0)\|^2\right]\frac{\tilde T^{2\alpha-1}}{(2\alpha-1)}\right). \tag{18.7}

From the above inequalities, Equations (18.6) and (18.7), and (H5) it follows that