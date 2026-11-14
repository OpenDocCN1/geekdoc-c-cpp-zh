
We now use the particular case, in which the invariant measure is given by (10.2.51) and \(\bar{D} = \frac{1}{\beta}\). After some lengthy but easy calculations we get the formula

\[
J_{s,S} = \frac{c - \frac{h}{2}}{\beta} + \frac{K + \frac{p - c + h}{\beta} \exp -\beta s - \frac{h}{2\beta}}{1 + \beta(S - s)} + h\left(\frac{1}{2}(S - s) + s\right).
\]

We can try now to minimize this expression in the two arguments \(s, S - s\). We first consider \(s\) fixed and minimize in \(S - s\). We obtain the condition

\[
\frac{K + \frac{p - c + h}{\beta} \exp -\beta s - \frac{h}{2\beta}}{(1 + \beta(S - s))^2} = \frac{h}{2\beta^2},
\]

which defines \(S(s)\). We can then compute \(J_s = J_{s,S(s)}\). We obtain the simple expression

\[
J_s = \frac{c}{\beta} + hS(s).
\]

Since we want to minimize \(J_s\), we find \(s\) such that \(S'(s) = 0\). Now writing (10.2.56) as

\[
(1 + \beta(S - s))^2 = \frac{2\beta}{h} K + 2 \frac{p - c + h}{h} \exp -\beta s - 1.
\]

We differentiate this expression in \(s\), and we take into account that \(S'(s) = 0\). We check easily that this implies

\[
1 + \beta(S - s) = \frac{p - c + h}{h} \exp -\beta s,
\]

which is exactly (10.2.46). Using this relation in (10.2.56) and rearranging we obtain

\[
K = \frac{h\beta}{2}(S - s)^2,
\]

which is (10.2.49). So the number \(\rho\) is the minimum of the ergodic cost, over all possible \(s, S\) policies.

## 10.3. ERGODIC INVENTORY CONTROL WITH FIXED COST AND BACKLOG

### 10.3.1. STATEMENT OF THE PROBLEM.

We consider the Bellman equation

\[
u_\alpha(x) = -cx + hx^+ + px^- + \inf_{\eta \ge x} \{ K \mathbf{1}_{\eta > x} + c\eta + \alpha E u_\alpha(\eta - D) \},
\]

studied in section 9.3. Define

\[
g_\alpha(x) = c(1 - \alpha) + \alpha cD + \alpha h E(x - D)^+ + \alpha p E(x - D)^-,
\]

and

\[
\mu_\alpha(x) = g'_\alpha(x) = c(1 - \alpha) + \alpha h - \alpha(h + p)\bar{F}(x).
\]

Then

\[
H_{\alpha,s}(x) = \int_s^x \Gamma_\alpha(x - \xi) \mu_\alpha(\xi) \,d\xi,
\]

where \(\Gamma_\alpha(x)\) is the solution of the renewal equation

(10.3.5)
\[
\Gamma_\alpha(x) = 1 + \alpha \int_0^x f(x-\xi)\Gamma_\alpha(\xi)\,d\xi.
\]

We define the function \(S_\alpha(s)\) such that

(10.3.6)
\[
\inf_{\eta \ge s} H_{\alpha,s}(\eta) = H_{\alpha,s}(S_\alpha(s)),
\]

and the pair \(s_\alpha, S_\alpha\) is defined by the relations

(10.3.7)
\[
\inf_{\eta \ge s_\alpha} H_{\alpha,s_\alpha}(\eta) + K = 0, \quad S_\alpha = S_\alpha(s_\alpha).
\]

We know that

(10.3.8)
\[
s_\alpha \le \bar{s}_\alpha,
\]

with

(10.3.9)
\[
c(1-\alpha) + ch - \alpha(p+h)\bar{F}(\bar{s}_\alpha) = 0.
\]

Then

(10.3.10)
\[
u_\alpha(x) = H_{\alpha,s_\alpha}(x) - cx + hx^+ + px^- + \frac{g_\alpha(s_\alpha)}{1-\alpha}.
\]

We want to study the behavior of \(u_\alpha(x)\) as \(\alpha \uparrow 1\).

### 10.3.2. CONVERGENCE.

We shall make the assumption

(10.3.11)
\[
f(x) \text{ is continuous, } f(x) > 0, \forall x.
\]

We recall that \(D = \int_0^{+\infty} x f(x) \,dx < \infty\). Also \(F(x) < 1, \forall x.\)

The function \(\Gamma_\alpha(x)\) converges to \(\Gamma(x)\) where

(10.3.12)
\[
\Gamma(x) = 1 + \int_0^x f(x-\xi)\Gamma(\xi)\,d\xi.
\]

We have next

(10.3.13)
\[
\mu_\alpha(x) \to \mu(x) = h - (p+h)F(x).
\]

Similarly

(10.3.14)
\[
g_\alpha(x) \to g(x) = cD + hE(x-D)^+ + pE(x-D)^-.
\]

The function

(10.3.15)
\[
H_{\alpha,s}(x) \to H_s(x) = \int_s^x \Gamma(x-\xi)\mu(\xi)\,d\xi.
\]

We can define \(\bar{s} > 0\) such that \(\mu(\bar{s}) = 0\) and \(\mu(x) < 0, \forall x < \bar{s}\) and \(\mu(x) > 0, \forall x > \bar{s}\). Since \(\Gamma\) is an increasing function, the function \(H_s(x)\) is increasing in \(x\), whenever \(s \ge \bar{s}\). Therefore we can assert

\[
S(s) = s, \quad \inf_{\eta \ge s} H_s(\eta) = 0, \text{ if } s \ge \bar{s}.
\]

So we limit the set of possible \(s\) to satisfy \(s < \bar{s}\).

### Lemma 10.3.

For \(s < \bar{s}\), the infimum of \(H_s(x)\) for \(x \ge s\) is attained in points strictly larger than \(\bar{s}\). Moreover \(\inf_{x \ge s} H_s(x) < 0\).

Proof. We cannot argue as in Lemma 10.1. The reason is that we do not have anymore the a priori bound provided by \(S_\alpha(0)\). The equivalent would be \(S_\alpha(-\infty)\). However, from formula (9.3.24) we see that \(S_\alpha(-\infty)\) is not bounded as \(\alpha \uparrow 1\). We shall instead rely on the estimates

(10.3.16)
\[
1 + B_1 x \le \Gamma(x) \le 1 + B_2 x, \quad B_2 = \sup_{x \ge 0} \frac{F(x)}{\int_0^x F(\xi) \,d\xi}, \quad B_1 = \inf_{x \ge 0} \frac{F(x)}{\int_0^x F(\xi) \,d\xi}.
\]

Note that the numbers \(B_1, B_2\) are well defined. Indeed the function \(G(x) = \frac{F(x)}{\int_0^x F(\xi) \,d\xi}\) converges to \(f(0) > 0\) as \(x \to 0\) and to \(\frac{1}{D}\) as \(x \to \infty\). Moreover it is continuous. Call

\[
z(x) = \Gamma(x) - 1 - Bx,
\]

then \(z\) is the solution of

\[
z(x) = F(x) - B \int_0^x F(\xi) \,d\xi + \int_0^x z(x - \xi) f(\xi) \,d\xi.
\]

If \(F(x) - B \int_0^x F(\xi) \,d\xi \le 0\), the function \(z(x)\) is also negative. Similarly, if \(F(x) - B \int_0^x F(\xi) \,d\xi \ge 0\), it is positive. The estimates (10.3.16) follow easily. We next express

\[
\begin{aligned}
H_s(x) &= \int_s^x \Gamma(x - \xi) \mu(\xi) \,d\xi \\
&= h \int_s^x \Gamma(x - \xi) \,d\xi - (p + h) \int_s^x \Gamma(x - \xi) \bar{F}(\xi) \,d\xi.
\end{aligned}
\]

If \(s > 0\), we get

\[
H_s(x) \ge h \int_s^x \Gamma(x - \xi) \,d\xi - (p + h) \int_0^x \Gamma(x - \xi) \bar{F}(\xi) \,d\xi.
\]

However

(10.3.17)
\[
\int_0^x \Gamma(x - \xi) \bar{F}(\xi) \,d\xi = x,
\]

which can be seen simply by differentiating the left hand side and showing that the derivative is 1. So, we have, from (10.3.16) and (10.3.17),

\[
\begin{aligned}
H_s(x) &\ge h(x - s) + \frac{h B_1}{2} (x - s)^2 - (p + h) x \\
&= \frac{h B_1}{2} (x - s)^2 - p x - h s, \quad x > s > 0.
\end{aligned}
\]

(10.3.18)

Now if \(s < 0\), we have

\[
H_s(x) = -p \int_0^x \Gamma(x - \xi) \,d\xi + h \int_0^x \Gamma(x - \xi) \,d\xi - (p + h) x,
\]

and using (10.3.16) we get easily

(10.3.19)
\[
H_s(x) \ge p s + \frac{B_2}{2} (-s^2 + 2sx) - p x + h \frac{B_1}{2} x^2, \quad s < 0 < x.
\]

Therefore, in both cases, \(H_s(x) \to \infty\) as \(x \uparrow \infty\). Also \(H'_s(s+) = \mu(s) < 0\). Hence the function \(H_s(x)\) attains a negative minimum on \((s, \infty)\). We call \(S(s)\) the smallest minimum if there are many.

We have

\[
H'_s(S(s)) = 0.
\]

We have next

\[
\frac{d}{ds}H_s(S(s)) = \frac{\partial}{\partial s}H_s(s)\big|_{S(s)} = -\Gamma(S(s) - s)\mu(s) > 0.
\]

Moreover \( S(s) > s > 0 \). For \( s < 0, x > 0 \) we have

(10.3.20)
\[
H_s(x) = -p \int_0^x \Gamma(x - \xi) \,d\xi + h \int_0^x \Gamma(\xi) \,d\xi - (p + h)x, \quad \forall s < 0 < x.
\]

It follows that

\[
H'_s(x) = (p + h)\Gamma(x) - p\Gamma(x - s) - (p + h),
\]

therefore \( S(s) \) is solution of the equation

(10.3.21)
\[
(p + h)\Gamma(S) - p\Gamma(S - s) - (p + h) = 0.
\]

It follows that as \( s \to -\infty, S(s) \to +\infty \). Otherwise, there will be a contradiction with (10.3.21). Furthermore, for \( s > 0 \) one has

\[
H_s(S(s)) \le H_s(0) = -p \int_0^\infty \Gamma(\xi) \,d\xi \le ps,
\]

from which it follows that \( H_s(S(s)) \to -\infty \) as \( s \to -\infty \).

Hence the function \( \inf_{y \ge s} H_s(y) \) increases from \( -\infty \) to 0, as \( s \) increases from \( -\infty \) to \( \bar{s} \). Therefore there exists a unique \( s \) for which it is equal to \( -K \). We can find the pair \( s, S \) by solving the algebraic system

(10.3.22)
\[
\begin{aligned}
\Gamma(S - s)\mu(s) + \int_s^S \Gamma(S - \xi)\mu'(d\xi) &= 0 \\
\int_s^S \Gamma(S - \xi)\mu(d\xi) &= -K
\end{aligned}
\]

### Theorem 10.5.

We assume \( h < c \) and (10.3.11), then we have

(10.3.23)
\[
s_\alpha \to s, \quad S_\alpha \to S,
\]

where the pair \( s, S \) is solution of (10.3.22). Let \( H(x) = H_s(x) \). Then

(10.3.24)
\[
u_\alpha(x) - \frac{g_\alpha(s_\alpha)}{1 - \alpha} \to u(x) = H(x) - cx + hx^+ + px^-.
\]

Set \( \rho = g(s) \), then \( \rho > 0 \) and one has

(10.3.25)
\[
u(x) + \rho = -cx + hx^+ + px^- + \inf_{\eta \ge x} \{K \mathbf{1}_{\eta > x} + c\eta + Eu(\eta - D)\}.
\]

Proof. Let us check that \( s_\alpha \) is bounded. Since \( s_\alpha < \bar{s} \), it is sufficient to assume \( s_\alpha < 0 \). We have \( S_\alpha > 0 \). We can write

\[
-K = H_{\alpha, s_\alpha}(S_\alpha) \le H_{\alpha, s_\alpha}(0)
\]
\[
= (c(1 - \alpha) - \alpha p) \int_{s_\alpha}^0 \Gamma_\alpha(-\xi) \,d\xi \le -s_\alpha(c(1 - \alpha) - \alpha p)
\]

which implies

\[
s_\alpha^- \le \frac{K}{\alpha p - c(1 - \alpha)},
\]

and thus \( s_\alpha \) remains bounded. But then, using estimates (10.3.18), (10.3.19) we get immediately that \( S_\alpha \) remains also bounded. So we can extract a subsequence
