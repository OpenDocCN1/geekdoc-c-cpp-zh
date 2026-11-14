
### Theorem 9.3.
Under the assumptions (9.2.1) and (5.1.2), there exists one and only one solution of the equation (9.2.4) in the space $B_1$. This function is l.s.c. There exists an optimal feedback $\hat{v}(x)$ with the estimate

(9.2.8)
\(\hat{v}(x) \le \frac{p\bar{D}}{c(1-\alpha)}.\)

The solution \(u(x) = \inf_v J_v(x)\), the value function. There exists an optimal control policy \(\hat{V}\), derived from the feedback \(\hat{v}(x)\).

## 9.2.2. OPTIMAL POLICY.

The important question is to characterize the optimal feedback, as we did in case without fixed cost \(K = 0\), see Chapter 5, section 5.1.3. When there is a fixed cost, we cannot get a Base stock policy. We have already seen in the deterministic case, see section 9.1, that the optimal feedback is obtained from an s, S policy, with \(s = D\). We shall see that this structure remains valid in the stochastic case, with naturally different values of s, S. Following the theory of impulse control developed in Chapter 8, we will determine the values of s, S.

We introduce the operators

(9.2.9)
\(T(u)(x) = hx + pE((x - D)^-) + \alpha Eu((x - D)^+),\)

(9.2.10)
\(M(u)(x) = K + \inf_{\eta \ge x} [(c - h)(\eta - x) + u(\eta)].\)

We have now a situation similar to that of section 8.3. We note that the functional equation (9.2.5) is equivalent to

\(u(x) = \min[T(u)(x), M(T(u))(x)].\)

However, this is also equivalent to

(9.2.11)
\(u(x) = \min[T(u)(x), M(u)(x)].\)

This formulation is the impulse control formulation of (9.2.5). There is no "continuous" control, so the operator \(T(u)(x)\) is affine. We are in the conditions of Theorem 8.4, with the important difference concerning the boundedness of the costs. Note that the variable ordering cost is here \((c - h)v\) so we shall assume

(9.2.12)
\(p > c > h.\)

The first inequality is essential, since otherwise there is no incentive to order. The second one is less essential but will be made in coherence with our general formulation of impulse control problems. Moreover it will be essential to obtain an s, S policy. We cannot use Theorem 8.4, to prove the existence and uniqueness of the solution, since the function \((x, v)\) is not bounded. However, by the equivalence with the formulation (9.2.5), we know that it is the case. It is therefore sufficient to construct a solution for which the optimal feedback is given by an s, S policy.

We begin with some notation. Define

(9.2.13)
\(g(x) = (p - \alpha(c - h))E(x - D)^+ - (p - c)x + p\bar{D}.\)

For any \(s \ge 0\), define next

(9.2.14)
\(g_s(x) = (g(x) - g(s)) \mathbb{1}_{x > s}.\)

Let us set

(9.2.15)
$$H_s(x) = \sum_{n=1}^\infty \alpha^{n-1} g_s * f^{*(n-1)}(x),$$

with the notation of (5.1.17).

### Lemma 9.4.
The function $H_s(x)$ attains its minimum in points larger or equal to $s$. Taking the smallest minimum one defines a function $S(s)$ and

(9.2.16)
$$H_s(S(s)) = \inf_{\eta \ge s} H_s(\eta).$$

Proof. We can write $H_s(x)$ as

$$H_s(x) = g_s(x) + \alpha g_s * f + \sum_{n=2}^\infty \alpha^n g_s * f^{*(n)}(x).$$

Consider

$$F^{(n)}(x) = \int_0^x f^{(n)}(\xi) \, d\xi,$$

then $F^{(0)}(x) = 1, F^{(1)}(x) = F(x)$. If

$$\Gamma(x) = \sum_{n=0}^\infty \alpha^n F^{(n)}(x),$$

then we can easily verify the formula

(9.2.17)
$$H_s(x) = \int_s^x \Gamma(x-\xi) \mu(\xi) d\xi,$$

with $\mu = g'$. It is useful to give a probabilistic interpretation of the function $F^{(n)}(x)$. In fact, we have

$$F^{(n)}(x) = P(D_1 + \cdots + D_n \le x),$$

in which $D_1, \cdots, D_n$ are $n$ independent identically distributed random variables with the same probability density $f(x)$. In this way, it is clear that

$$F^{(n)}(x) \uparrow 1, \text{ as } x \to \infty, \quad \Gamma(x) \uparrow \frac{1}{1-\alpha}, \text{ as } x \uparrow \infty.$$

Therefore $H_s(x) \to +\infty$ as $x \uparrow \infty$. We can check that

$$H'_s(s+0) = \mu(s) = c(1-\alpha) + \alpha h - (p-\alpha(c-h))\bar{F}(s).$$

Since $p > c$ the function $\mu(s)$ increases from $-(p-c)$ to $(c(1-\alpha)+\alpha h)$. Therefore it vanishes in a point $\bar{s}$ and is strictly negative for $0 \le s < \bar{s}$. This $\bar{s}$ is simply the Base stock identified by formula (5.1.14).

Consider first $s \in [0, \bar{s}]$. Therefore $H'_s(s+0) < 0$ and the function $H_s(x)$ becomes strictly negative for $x$ close to $s$. Moreover

$$\begin{aligned} H_s(x) &= \int_s^x \Gamma(x-\xi)\mu(\xi)d\xi + \int_x^\infty \Gamma(x-\xi)\mu(\xi)d\xi \\ \ge \frac{1}{1-\alpha}(g(s) - g(s)) + g(x) - g(s). \end{aligned}$$

Therefore $H_s(x)$ goes to $\infty$ as $x$ goes to $\infty$. Since it is a continuous function, it attains its minimum on $[0, \infty)$. By taking the smallest minimum, if there are several of them, we define uniquely the number \( S(s) \). Note also, that if \( s \ge \bar{s} H_s(x) \) is increasing in \( x \), and for \( s < \bar{s} H_s(x) \) is decreasing in \( x \) on the interval \( [s, \bar{s}) \), hence \( S(s) = s \) if \( s \ge \bar{s} \), \( S(s) > s \) if \( s < \bar{s} \).

It follows also that \( H'_s(S(s)) = 0 \) for \( s < \bar{s} \). Therefore

\(\frac{dH_s(S(s))}{ds} = \frac{\partial}{\partial s} H_s(x)_{x=S(s)}, \text{ if } s < \bar{s}.\)

So

(9.2.18)
\(\frac{dH_s(S(s))}{ds} = -\mu(s)\Gamma(S(s) - s) > 0, \text{ if } s < \bar{s}.\)

Clearly \( H_s(S(s)) = 0 \) for \( s \ge \bar{s} \). The property (9.2.16) has been proven.

Consider now \( S_0 = S(0) \). We have

\( H_0(x) = \int_0^x \Gamma(\xi)\mu(x - \xi)d\xi. \)

So

\( H'_0(x) = \mu(0)\Gamma(x) + \int_0^x \mu'(x - \xi)\Gamma(\xi) d\xi \)
\( = (c - p)\Gamma(x) + (p - \alpha(c - h)) \int_0^x f(x - \xi)\Gamma(\xi) d\xi. \)

However it is easy to check that \( \Gamma(x) \) satisfies the renewal equation

(9.2.19)
\( \Gamma(x) = 1 + \alpha \int_0^x f(x - \xi)\Gamma(\xi) d\xi. \)

Therefore

\( H'_0(x) = \frac{1}{\alpha}[(p - \alpha(p - h))\Gamma(x) - (p - \alpha(c - h))]. \)

Therefore \( S_0 \) is given by

(9.2.20)
\( \Gamma(S_0) = \frac{p - \alpha(c - h)}{p - \alpha(p - h)}. \)

We shall need the assumption

(9.2.21)
\( H_0(S_0) = \int_0^{S_0} \Gamma(\xi)\mu(S_0 - \xi)d\xi < -K. \)

We can then state the following

### Theorem 9.4.
Under the assumptions of Theorem 9.3 and (9.2.12), (9.2.21), the optimal feedback \( \psi(x) \) of the functional equation (9.2.5) is given by an \( s, S \) policy. The value of \( s \) is the unique value such that

(9.2.22)
\( K + \inf_{\eta \ge s} H_s(\eta) = 0, \)

and \( S(s) = s \). Moreover the function \( u(x) \) is continuous

Proof. Consider the function \( \inf_{\eta \ge s} H_s(\eta) = H_s(S(s)) \).

We have \( H_s(S(s)) = 0 \) for \( s \ge \bar{s} \). From the assumption we have \( H_0(S(0)) < -K \). From (9.2.18) we know that \( H_s(S(s)) \) is strictly increasing in \( s \), for \( s < \bar{s} \). So there will be one and only one \( s \), for which (9.2.22) is verified. So the pair \( s, S \) is well identified. We are going to construct a solution of (9.2.11), for which the optimal feedback is defined by an \( s, S \) policy, with the values \( s, S \) just defined. To simplify notation we drop the indices s,S. We use the notation H(x) for H_s(x), with the particular s. Consider the function

(9.2.23)
\( u(x) = H(x) + (h - c)x + \frac{g(s)}{1 - \alpha} \).

Since H(x) is continuous, the function u(x) is continuous. Then u(x) satisfies

(9.2.24)
\( u(x) = \begin{cases} (h - c)x + \frac{g(s)}{1 - \alpha}, & x \le s \\ hx + pE(x - D)^- + \alpha Eu(x - D)^+, & x \ge s \end{cases} \)

and also, from the choice of s

(9.2.25)
\( K + \inf_{\eta \ge s} [u(\eta) + (c - h)\eta] = \frac{g(s)}{1 - \alpha}, \)

hence also

(9.2.26)
\(\begin{aligned} u(s) + (c - h)s &= K + \inf_{\eta \ge s} [u(\eta) + (c - h)\eta] \\ &= K + u(S) + (c - h)S \end{aligned}\)

Since

\( u(x) = -(c - h)x + \frac{g(s)}{1 - \alpha}, \quad x \le s, \)

the function u(x) + (c - h)x is constant on $[0, s]$. Therefore

\(\inf_{\eta \ge x} [(c - h)\eta + u(\eta)] = \inf_{\eta \ge s} [(c - h)\eta + u(\eta)], \quad \forall x \le s.\)

Hence the function u satisfies

\(\begin{aligned} u(x) &= M(u)(x), \forall x \le s \\ u(x) &= T(u)(x), \forall x \ge s \end{aligned}\)

So it remains to prove that

\(\begin{aligned} u(x) \le T(u)(x), \forall x \le s \\ u(x) \le M(u)(x), \forall x \ge s \end{aligned}\)

In terms of H the first inequality amounts to $g_s(x) \ge 0, \forall x \le s$. This is true since $\mu(\xi) < 0, \forall x \le \xi < s < S$. The second inequality is more involved. In terms of H it amounts to

(9.2.27)
\( H(x) \le K + \inf_{\eta \ge x} H(\eta), \forall x \ge s. \)

To prove (9.2.27) we first notice that for x \ge s we have \inf_{\eta \ge x} H(\eta) \ge \inf_{\eta \ge s} H(\eta) \ge -K. So the inequality is certainly true whenever H(x) \le 0. Consider then the smallest number called x_0 for which H becomes positive. We have then

\( H(x_0) = 0, H(x) < 0 \quad \forall x, s < x < x_0. \)

We can claim that $g_s(x_0) > 0$. This follows from the relation $g_s(x_0) = -\alpha E H(x_0 - D)$ and the properties of x_0 resulting from its definition. To proceed we note that the relation (9.2.15) implies

\( H(x) = g_s(x) + \alpha E H(x - D), \)

which holds for any x, provided that we extend by 0 the definition of H whenever x \le 0.
