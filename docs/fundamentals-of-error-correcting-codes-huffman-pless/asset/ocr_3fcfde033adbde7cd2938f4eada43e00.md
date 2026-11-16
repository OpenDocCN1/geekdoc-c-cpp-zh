Again this means that when the left-hand side is written as a rational function, the numerator is a multiple of $G(x)$. (Working modulo $G(x)$ is like working in the ring $\mathbb{F}_q[x]/(G(x))$; requiring that $G(y_i) \neq 0$ guarantees that $x - y_i$ is invertible in this ring.) $G(x)$ is the Goppa polynomial of $\Gamma(L, G)$. The narrow-sense BCH code of length $n$ and designed distance $\delta$ is the Goppa code $\Gamma(L, G)$ with $L = \{1, \beta^{-1}, \beta^{-2}, \dots, \beta^{1-n}\}$ and $G(x) = x^{q-1}$.

# Exercise 767

Construct a binary Goppa code of length 4 using (13.4) as follows. Use the field $\mathbb{F}_8$ given in Example 3.4.3 with primitive element $\alpha$. Let $L = \{y_0, y_1, y_2, y_3\} = \{1, \alpha, \alpha^2, \alpha^4\}$ and $G(x) = x - \alpha^3$.

+   (a) When writing the left-hand side of (13.4) as a rational function $a(x)/b(x)$, the numerator $a(x)$ begins $c_0(x - \alpha)(x - \alpha^2)(x - \alpha^4) + \cdots$. Complete the rest of the numerator (but do not simplify).

+   (b) The numerator $a(x)$ found in part (a) is a multiple of $G(x) = x - \alpha^3$, which, in this case, is equivalent to saying $a(\alpha^3) = 0$. Simplify $a(\alpha^3)$ to obtain an $\mathbb{F}_8$-linear combination of $c_0, c_1, c_2$, and $c_3$. Hint: First compute $\alpha^3, 1, \alpha^2, \alpha - \alpha^2$, and $\alpha^3 - \alpha^4$.

+   (c) There are 16 choices for $c_0 \alpha_i + c_3$ in $\mathbb{F}_4^2$. Test each of these using the results of part (b) to find a codewords in $\Gamma(L, G)$.

We now find a parity check matrix for $\Gamma(L, G)$. Notice that

$\frac{1}{x - y_i} \equiv -\frac{1}{G(y_i)} \frac{G(x) - G(y_i)}{x - y_i} \pmod{G(x)}$

since, by comparing numerators, $1 \equiv -G(y_i)^{-1}(G(x) - G(y_i)) \pmod{G(x)}$. So by (13.4) $\mathbf{c} = c_0 c_1 \cdots c_{v-1} \in \Gamma(L, G)$ if and only if

$\sum_{i=0}^{v-1} c_i \frac{G(x) - G(y_i)}{x - y_i} (G(y_i))^{-1} \equiv 0 \pmod{G(x)}. \quad (13.5)$

Suppose $G(x) = \sum_{j=0}^w g_j x^j$ with $g_j \in \mathbb{F}_q$, where $w = \deg(G(x))$. Then

$\frac{G(x) - G(y_i)}{x - y_i} (G(y_i))^{-1} = G(y_i)^{-1} \sum_{j=1}^w g_j \sum_{k=0}^{j-1} x^k y_i^{j-1-k} = G(y_i)^{-1} \sum_{k=0}^{w-1} x^k \left( \sum_{j=k+1}^w g_j y_i^{j-1-k} \right).$

Therefore, by (13.5), setting the coefficients of $x^k$ equal to 0, in the order $k = w-1, w-2, \dots, 0$, we have that $\mathbf{c} \in \Gamma(L, G)$ if and only if $H \mathbf{c}^T = \mathbf{0}$, where

$H = \begin{bmatrix} h_{0g_w} & h_{1g_w} & \cdots & h_{n-1g_w} \\ h_0(g_{w-1} + g_w y_0) & h_1(g_{w-1} + g_w y_1) & \cdots & h_{n-1}(g_{w-1} + g_w y_{n-1}) \\ \vdots & \vdots & & \vdots \\ h_0 \sum_{j=1}^w g_j y_0^{j-1} & h_1 \sum_{j=1}^w g_j y_1^{j-1} & \cdots & h_{n-1} \sum_{j=1}^w g_j y_{n-1}^{j-1} \end{bmatrix} \quad (13.6)$