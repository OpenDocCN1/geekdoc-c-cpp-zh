
where $D = \int_0^\infty \xi f(\xi) d\xi$. In fact

(5.1.8) $$l(x, v) = cv + hx + pE(D - x - v)^+,$$

and the last term is the penalty cost incurred when the demand is not met. Note that the assumption (4.5.4) is satisfied.

Moreover $$\Phi^{hv} l_v(x) \le cv + hx + p\bar{D} + hv.$$

More generally $$(\Phi^n)^{hv} l_v(x) \le cv + hx + p\bar{D} + nhv.$$

Also, denoting by $x$, the identity function $x \to x$, we have (5.1.9) $$\Phi^v x(x) = E(x + v - D)^+ \le x + v,$$

hence the assumption (4.5.2) is satisfied, with $\theta = 1$ and $\lambda = 1, \mu = 0$.

## 5.1.2. BELLMAN EQUATION.

We can apply the results of Theorem 4.8. The functional equation (4.3.7) reads

(5.1.10) $$u(x) = \inf_{v \ge 0} \left\{ l(x, v) + \alpha \left( u(0)\bar{F}(x+v) + \int_0^{x+v} u(x+v-\eta) f(\eta) d\eta \right) \right\}.$$

It is convenient to look at (5.1.10) as a system for a pair $u(\cdot), \lambda$ where $u(\cdot)$ is a locally integrable function with linear growth and $\lambda$ is a positive real number. The system is written as

(5.1.11) $$\begin{aligned} u(x) &= \inf_{v \ge 0} \left\{ l(x, v) + \alpha \left( \lambda \bar{F}(x+v) + \int_0^{x+v} u(x+v-\eta) f(\eta) d\eta \right) \right\} \\ \lambda &= \inf_{v \ge 0} \left\{ l(0, v) + \alpha \left( \lambda F(v) + \int_0^v u(v-\eta) f(\eta) d\eta \right) \right\} \end{aligned}$$

Naturally, the solution $u(x)$ is continuous and $u(0) = \lambda$. Moreover, the argument $v$ of the infimum in the right hand side of (5.1.11) can be taken bounded by $p\bar{D} / c(1-\alpha)$.

Recall the definition of $B_1$, space of functions with linear growth, which in the present situation, where the argument lies in $R^+$ reduces to

$$u \in B_1 \Longleftrightarrow \frac{|u(x)|}{1+x} \le C.$$

We can assert, as a consequence of Theorem 4.8 that

Theorem 5.1. Assume (5.1.2) and (5.1.6). Then the system (5.1.11) has a unique solution in the space $B_1 \times R$. The function $u(x)$ is continuous and $\lambda = u(0)$. Moreover over $u(x)$ is the value function of the control problem

$$u(x) = \inf J_x(V),$$

where

(5.1.12) $$J_x(V) = E \left[ \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n) \right].$$

Furthermore there exists an optimal control, obtained from a feedback $\hat{v}(x)$, which is a Borel function attaining the infimum in the right hand side of (5.1.11). One has $\hat{v}(x) \le \frac{p\bar{D}}{c(1-\alpha)}$.

Remark. We have not used the construction of $P^{V,x}$ developed for general Markov chains in section 4.2.1, since we have the formulation described in section 4.2.3.

## 5.1.3. BASE STOCK POLICY.

In this section we will check that $\hat{v}(x)$ is actually quite simple, and is characterized by what is called a Base Stock Policy. A Base Stock Policy is characterized by a number $S$ and the formula

(5.1.13) $$
\hat{v}(x) = \begin{cases} S - x, & \text{if } x \le S \\ 0, & \text{if } x \ge S \end{cases}
$$

Theorem 5.2. Under the assumptions (5.1.2) and (5.1.6), and $p > c$ the optimal feedback is a base stock policy. The function $u$ is convex and $C^1$. The base stock is given by the formula

(5.1.14) $$
F(S) = \frac{c(1-\alpha) + \alpha h}{p - \alpha c + \alpha h}.
$$

One has

(5.1.15) $$
u(S) = (h-c)S + \frac{cS + pE(S-D)^-}{1-\alpha} + (h-c)\frac{\alpha}{1-\alpha}E(S-D)^+.
$$

Setting

(5.1.16) $$
g(x) = (c + \alpha(h-c) - (p + \alpha(h-c))F(x))^+,
$$

then $u'(x) = h - c + z(x)$ where

(5.1.17) $$
z(x) = \sum_{n=1}^{\infty} \alpha^{n-1} g \star f^{*(n-1)},
$$

and $\varphi \star \psi$ denotes the convolution product

$$
\varphi \star \psi(x) = \int_0^x \varphi(x-\xi)\psi(\xi) d\xi,
$$

and $f^{*(0)}(x) = \delta(x)$, $f^{*(1)}(x) = f(x)$.

PROOF. Note that $S$ is uniquely defined, thanks to the assumption $p > c$. Moreover $g(x) = 0$, for $x \le S$. Consequently $z = 0$, for $x \le S$. The series $z(x)$ converges since $f$ is bounded.

Recalling that

$$
l(x,v) = cv + hx + pE(x+v-D)^-,
$$

we can write also

$$
l(x,v) = (h-c)x + l_0(x+v),
$$

with

$$
l_0(x) = cx + pE(x-D)^-.
$$

Therefore equation (5.1.11) can be also written as

(5.1.18) $$
u(x) = (h-c)x + \inf_{v \ge 0} \{l_0(x+v) + \alpha Eu((x+v-D)^+)\}.
$$

The function $l_0(x)$ is convex continuous on $R^+$ and tends to $+\infty$ as $x \to +\infty$.

There exists a unique $S_0$ such that

$$
l_0(S_0) = \inf_{x \ge 0} l_0(x).
$$

Consider the increasing sequence. We begin with $u_1(x)$. Clearly we can write

$$
u_1(x) = \begin{cases} 
(h - c)x + l_0(S_0), & \forall x \le S_0 \\ 
(h - c)x + l_0(x), & \forall x \ge S_0 
\end{cases}
$$

Its derivative is

$$
(u_1)'(x) = \begin{cases} 
h - c, & \forall x < S_0 \\ 
h - c + (l_0)'(x), & \forall x > S_0 
\end{cases}
$$

This function is continuous and increasing, from which it follows that $u_1(x)$ is convex continuous and tends to $+\infty$ as $x \to +\infty$. More generally, assume that

$$
\zeta_n(x) = l_0(x) + \alpha Eu_n((x - D)^+),
$$

is convex continuous and tends to $+\infty$ as $x \to +\infty$. Therefore there exists a unique $S_n$ defined as the smallest minimum value of the function $\zeta_n(x)$, for $x \ge 0$, if the minimum is not unique. Hence we can write

$$
u_{n+1}(x) = \begin{cases} 
(h - c)x + \zeta_n(S_n), & \forall x \le S_n \\ 
(h - c)x + \zeta_n(x), & \forall x \ge S_n 
\end{cases}
$$

It follows that

$$
u'_{n+1}(x) = h - c + \zeta'_n(x)\mathbb{I}_{x > S_n},
$$

which is an increasing function of $x$. Therefore $u_{n+1}(x)$ is also a convex continuous function which tends to $+\infty$ as $x \to +\infty$. Consider then $\zeta_{n+1}(x)$. We have

$$
\begin{aligned}
\zeta'_{n+1}(x) &= l'_0(x) + \alpha E u'_{n+1}(x - D)\mathbb{I}_{x > D} \\
&= l'_0(x) + \alpha(h - c)F(x) + \alpha E \zeta'_n(x - D)\mathbb{I}_{x - D > S_n} \\
&= c + \alpha(h - c) - (p + \alpha(h - c))\bar{F}(x) + \alpha E \zeta'_n(x - D)\mathbb{I}_{x - D > S_n},
\end{aligned}
$$

and this function is increasing in $x$. Therefore $\zeta_{n+1}(x)$ is convex continuous and tends to $+\infty$ as $x \to +\infty$.

Since all the $u_m, \zeta_n$ functions are convex, the limits $u, \zeta$ are also convex, with

$$
\zeta(x) = l_0(x) + \alpha Eu((x - D)^+).
$$

Being convex and finite for any $x$, they are also continuous for $x > 0$. They also tend to $+\infty$ as $x \to +\infty$. So the optimal feedback is defined by a base stock $S$ which is the smallest minimum of $\zeta(x)$. Next, from (5.1.18) We can write

$$
u(x) = \begin{cases} 
(h - c)x + l_0(S) + \alpha Eu((S - D)^+), & \forall x \le S \\ 
(h - c)x + l_0(x) + \alpha Eu((x - D)^+), & \forall x \ge S 
\end{cases}
$$

Since $(S - D)^+ \le S$. We can easily calculate

$$
Eu((S - D)^+) = \frac{(h - c)E(S - D)^+ + l_0(S)}{1 - \alpha},
$$

therefore formula (5.1.15) follows. Next

$$
\zeta'(x) = l'_0(x) + \alpha E[u'((x - D)^+)\mathbb{I}_{x > D}].
$$

We express the fact that \(\zeta'(S) = 0\). But \(u'((S-D)^+) = h - c\). Then \(\zeta'(S)\) can be easily expressed. The formula (5.1.14) follows easily. It follows also that \(u'(x)\) is continuous in \(S\), and thus \(u(x)\) is \(C^1\). We next define

$$
\begin{aligned}
z(x) &= u'(x) - (h-c) \\
&= \zeta'(x) \mathbf{1}_{x \ge S}.
\end{aligned}
$$

Differentiating the expression above of \(u(x)\) for \(x \ge S\) we obtain

$$
z(x) = l'_0(x) + \alpha(h-c)F(x) + \alpha E[z(x-D)\mathbf{1}_{x \ge D}].
$$

Noting that \(z(x) = 0, \forall x \le S\), we can write this equation as

$$
z(x) = g(x) + \alpha E z(x-D),
$$

and the solution of this equation is given by the series (5.1.17). This completes the proof.

We have introduced the condition \(p > c\). Let us consider now the situation in which \(c \ge p\).

Theorem 5.3. Under the assumptions (5.1.2) and (5.1.6) and \(p \le c\) then \(u(x) = u_0(x)\). Hence \(\hat{v}(x) = 0\).

PROOF. Consider the approximation of \(u\) by the increasing sequence. We have

$$
u_1(x) = (h-c)x + \inf_{v \ge 0} \{l_0(x+v)\},
$$

but, from the assumption $l_0(x)$ is monotone increasing. Therefore

$$
u_1(x) = (h-c)x + l_0(x).
$$

Then

$$
u_2(x) = (h-c)x + \inf_{v \ge 0} \{l_0(x+v) + \alpha E u_1((x+v-D)^+)\}.
$$

But

$$
l_0(x) + \alpha E u_1((x-D)^+) = l_0(x) + \alpha(h-c)E(x-D)^+ + \alpha E l_0((x-D)^+).
$$

Since $l_0$ is monotone increasing, the last term on the right hand side is monotone increasing. If we take the derivative of the first two terms we get

$$
l'_0(x) + \alpha(h-c)F(x) = c + \alpha(h-c) - (p + \alpha(h-c))F(x) \ge 0.
$$

Therefore $l_0(x) + \alpha E u_1((x-D)^+)$ is monotone increasing and again the infimum is attained at $v = 0$, and we have

$$
u_2(x) = (h-c)x + l_0(x) + \alpha E u_1((x-D)^+).
$$

By induction, we check that $l_0(x) + \alpha E u_n((x-D)^+)$ is monotone increasing and

$$
u_{n+1}(x) = (h-c)x + l_0(x) + \alpha E u_n((x-D)^+).
$$

Therefore

$$
u(x) = (h-c)x + l_0(x) + \alpha E u((x-D)^+),
$$

hence $u(x) = w_0(x)$ and $\hat{v}(x) = 0$. The proof has been completed.
