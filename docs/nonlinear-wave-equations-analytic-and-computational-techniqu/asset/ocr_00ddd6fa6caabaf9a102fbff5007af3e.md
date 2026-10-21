with the solution of the form $f(x) \approx c_1 e^{p_1 x} + c_2 e^{p_2 x} + c_3 e^{p_3 x}$. We examine $\gamma \ge 0$, and for $x \to +\infty$ we require the solution $f(x)$ of (4.18) to be bounded, and thus $$f(x) \approx f_+(x) = c_3 e^{p_3 x}.$$

Next, examine (4.19) in the form $$g''_+(x) - k^2 g_+(x) = k^2 f_+(x) + f''_+(x) = c_3 \left(k^2 + p_3^2\right) e^{p_3 x}$$ with the solution $$g_+(x) = \beta_1 e^{+k x} + \beta_2 e^{-k x} + c_3 \frac{k^2 + p_3^2}{p_3^2 - k^2} e^{p_3 x}.$$

Since this solution has to remain bounded as $x \to +\infty$, we find $$g_+(x) = \beta_2 e^{-k x} + c_3 \frac{k^2 + p_3^2}{p_3^2 - k^2} e^{p_3 x}.$$

The case $\gamma \ge 0$ and $x \to -\infty$, leads in an analogous way to $$f(x) \approx f_-(x) = c_1 e^{p_1 x} + c_2 e^{p_2 x}$$ and $$g(x) \approx g_-(x) = \beta_1 e^{+k x} + c_1 \frac{k^2 + p_1^2}{p_1^2 - k^2} e^{p_1 x} + c_2 \frac{k^2 + p_2^2}{p_2^2 - k^2} e^{p_2 x}.$$

For $0 < k^2 \ll 1$ we find (4.22) $$p_1^2 \approx \frac{4^2}{(4 - 3 k^2)^2} \gamma^2 \approx \gamma^2$$ and thus the above formula for $g(x)$ may not be valid for $\gamma^2 \approx k^2 \ll 1$. For $k = 0$ the equation for $g$ simplifies to $g''(x) = f''(x)$, and the conditions at $x = \pm \infty$ imply $g(x) = f(x)$.

# 4.3.2. Solutions for intermediate $|x|$

Choosing a large value for $M > 0$, we construct nontrivial solutions to (4.14)–(4.15) for $-\infty < x \le -M$, then for $-M \le x \le +M$, and then for $+M \le x < +\infty$. We seek nonzero values of the parameters $(c_1, c_2, c_3, \beta_1, \beta_2)$, such that we find a nonzero solution. Use the solutions $f_-$ and $g_-$ to define a matrix

$$\mathbf{T}_- = \begin{bmatrix} e^{-p_1 M} & e^{-p_2 M} & 0 & 0 & 0 \\ p_1 e^{-p_1 M} & p_2 e^{-p_2 M} & 0 & 0 & 0 \\ p_1^2 e^{-p_1 M} & p_2^2 e^{-p_2 M} & 0 & 0 & 0 \\ \frac{p_1^2 + k^2}{p_1^2 - k^2} e^{-p_1 M} & \frac{p_2^2 + k^2}{p_2^2 - k^2} e^{-p_2 M} & 0 & e^{-k M} & 0 \\ \frac{(p_1^2 + k^2) p_1}{p_1^2 - k^2} e^{-p_1 M} & \frac{(p_2^2 + k^2) p_2}{p_2^2 - k^2} e^{-p_2 M} & 0 & k e^{-k M} & 0 \end{bmatrix}$$

with $$\mathbf{T}_- \begin{pmatrix} c_1 \\ c_2 \\ c_3 \\ \beta_1 \\ \beta_2 \end{pmatrix} = \begin{pmatrix} f(-M) \\ f'(-M) \\ f''(-M) \\ g(-M) \\ g'(-M) \end{pmatrix}$$