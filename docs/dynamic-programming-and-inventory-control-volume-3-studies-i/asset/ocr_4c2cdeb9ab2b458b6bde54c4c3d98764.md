Remark. We have not used the construction of $P^{V,x}$ developed for general Markov chains in section 4.2.1, since we have the formulation described in section 4.2.3.

# 5.1.3. BASE STOCK POLICY.

In this section we will check that $\hat{v}(x)$ is actually quite simple, and is characterized by what is called a Base Stock Policy. A Base Stock Policy is characterized by a number $S$ and the formula

(5.1.13) $$
\hat{v}(x) = \begin{cases} S - x, & \text{if } x \le S \\ 0, & \text{if } x \ge S 
\end{cases}$$


**Theorem 5.2.** Under the assumptions (5.1.2) and (5.1.6), and $p > c$ the optimal feedback is a base stock policy. The function $u$ is convex and $C^1$. The base stock is given by the formula

(5.1.14) $$
F(S) = \frac{c(1-\alpha) + \alpha h}{p - \alpha c + \alpha h}.$$


One has

(5.1.15) $$
u(S) = (h-c)S + \frac{cS + pE(S-D)^-}{1-\alpha} + (h-c)\frac{\alpha}{1-\alpha}E(S-D)^+.$$


Setting

(5.1.16) $$
g(x) = (c + \alpha(h-c) - (p + \alpha(h-c))F(x))^+,$$
then $u'(x) = h - c + z(x)$ where

(5.1.17) $$
z(x) = \sum_{n=1}^{\infty} \alpha^{n-1} g \star f^{*(n-1)},$$


and $\varphi \star \psi$ denotes the convolution product

$$
\varphi \star \psi(x) = \int_0^x \varphi(x-\xi)\psi(\xi) d\xi,$$


and $f^{*(0)}(x) = \delta(x)$, $f^{*(1)}(x) = f(x)$.

**PROOF.** Note that $S$ is uniquely defined, thanks to the assumption $p > c$. Moreover $g(x) = 0$, for $x \le S$. Consequently $z = 0$, for $x \le S$. The series $z(x)$ converges since $f$ is bounded.

Recalling that

$$
l(x,v) = cv + hx + pE(x+v-D)^-,$$


we can write also

$$
l(x,v) = (h-c)x + l_0(x+v),$$


with

$$
l_0(x) = cx + pE(x-D)^-.$$


Therefore equation (5.1.11) can be also written as

(5.1.18) $$
u(x) = (h-c)x + \inf_{v \ge 0} \{l_0(x+v) + \alpha Eu((x+v-D)^+)\}.$$


The function $l_0(x)$ is convex continuous on $R^+$ and tends to $+\infty$ as $x \to +\infty$.

There exists a unique $S_0$ such that

$$
l_0(S_0) = \inf_{x \ge 0} l_0(x).$$