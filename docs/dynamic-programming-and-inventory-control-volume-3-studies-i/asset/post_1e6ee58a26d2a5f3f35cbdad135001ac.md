
We now prove (16.3.37), (16.3.38), by studying $u$ more precisely. First, from the relation

$$\frac{\sigma^2}{2}\Phi'(0) - (\nu - k\gamma) + \alpha \int_0^{+\infty} \Phi(x) dx = 0$$

we deduce (recalling that $\Phi(0) = 1$)

$$u(0) > 0.$$

Moreover, one easily checks that $u(x)$ is the solution of the differential equation

$$(16.3.41) \quad u' = \frac{2u^2}{\sigma^2} - \frac{2u}{\sigma^2}(\nu + k(x - \gamma)) - \alpha, \quad u(0) > 0.$$

We first check that $u(x) > 0$ for $x < 0$. Indeed, we can write for $x < 0$

$$-\frac{\sigma^2}{2}\Phi'(0) + \frac{\sigma^2}{2}\Phi'(x) + \nu - k\gamma - (\nu + k(x - \gamma))\Phi(x) + \alpha \int_x^0 \Phi(y) dy = 0,$$

hence

$$\frac{-\frac{\sigma^2}{2}\Phi'(0) + (\nu - k\gamma)}{\Phi(x)} = u(x) + \alpha \int_x^0 \Phi(y) dy = 0,$$

which implies $u(x) > 0$, for $x < 0$. Next we write (16.3.41) as

$$(16.3.42) \quad u' = \frac{2}{\sigma^2}(u(x) - B(x))(u(x) + C(x)),$$

with

$$C(x) = B(x) - (\nu + k(x - \gamma)).$$

Note that

$$B(x)C(x) = \frac{\alpha \sigma^2}{2}.$$

Consider now

$$v(x) = \frac{u(x)}{B(x)} > 0,$$

it satisfies the differential equation

$$(16.3.43) \quad v' = \frac{2}{\sigma^2}(v - 1)\left(Bv + \frac{\alpha \sigma^2}{2B}\right) - v \frac{k}{\sqrt{(\nu + k(x - \gamma))^2 + 2\alpha \sigma^2}}, \quad x < 0.$$

We deduce

$$-\frac{1}{2} \frac{d}{dx} ((1 - v)^+)^2 = v'(1 - v)^+ < 0,$$

therefore the function $((1 - v)^+)^2$ increases on $(-\infty, 0)$. It follows that if there exists $\bar{x} < 0$ such that $(1 - v)^+(\bar{x}) = 0$, then necessarily

$$(1 - v)^+(x) = 0, \quad \forall x < \bar{x}$$

Hence if $v(\bar{x}) \ge 1$, necessarily $v(x) \ge 1, \forall x < \bar{x}$. Suppose now that $v(x) < 1, \forall x < 0$, then from the equation (16.3.43) it follows that $v'(x) < 0$. Therefore $v(x)$ increases as $x \to -\infty$. It necessarily converges to $v^* \le 1$. If $v^* < 1$, we see from the equation that $v'(x) \to -\infty$, as $x \to -\infty$. This is a contradiction. Summarizing we have the situation: either

$$v(x) \ge 1, \quad \forall x < \bar{x}$$

or

$$v(x) \uparrow 1, \quad \text{as } x \downarrow -\infty$$

Since \(u(x) = v(x)B(x)\) we have either

$$u(x) \ge B(x), \forall x < \bar{x}$$

or

$$u(x) - B(x) = (v(x) - 1)B(x) \to 0, \text{ as } x \to -\infty$$

So in both cases we can assert the property (16.3.38). Next, either

$$-\frac{\sigma^2}{2} \frac{\Phi'(x)}{\Phi(x)} \ge -(\nu + k(x - \gamma)) + B(x), \forall x \le \bar{x}$$

or

$$-\frac{\sigma^2}{2} \frac{\Phi'(x)}{\Phi(x)} = B(x) + u(x) - B(x) - (\nu + k(x - \gamma)) \to \infty, \text{ as } x \to -\infty.$$

In both cases we obtain property (16.3.37). So \(\tilde{Z}(x)\) given by (16.3.40) is the dominant term in the expression of \(Z(x)\). Now we can write

$$\tilde{Z}(x) = \frac{2}{\sigma^2} \frac{p - c(\alpha + k)}{\alpha(\alpha + k)} Bu(Bv - (\nu + k(x - \gamma)\nu)$$
$$= \frac{2}{\sigma^2} \frac{p - c(\alpha + k)}{\alpha(\alpha + k)} \left( B^2(x)v(x)(v(x) - 1) + v(x) \frac{\alpha a^2}{2} \right).$$

Now, since

$$\liminf_{x \to -\infty} v(x) \ge 1,$$

we can assert that

$$\liminf_{x \to -\infty} \tilde{Z}(x) = \frac{p - c(\alpha + k)}{\alpha + k},$$

hence also

$$\liminf_{x \to -\infty} Z(x) = \frac{p - c(\alpha + k)}{\alpha + k}$$

which proves (16.3.34), and concludes the proof.

## 16.4. SOLUTION OF THE Q.V.I

It remains to show that the function \(G_s(x)\) defined by (16.3.1), (16.3.2) is solution of the Q.V.I. (16.2.5). We can state the

### Theorem 16.3. The function \(G_s(x)\) defined by (16.3.1), (16.3.2) is solution of the Q.V.I. (16.2.5).

Proof. We first check the complementarity slackness condition (third condition (16.2.5)). For \(x \le s\), we have

$$G_s(x) = G_s(s)$$
$$= K + G_s(S(s))$$
$$= K + \inf_{\eta > s} G_s(\eta).$$

But

$$\inf_{\eta > s} G_s(\eta) = \inf_{\eta > x} G_s(\eta) \quad \forall x \le s.$$

Indeed, for \(x < \eta < s\), one has

$$G_s(\eta) = G_s(s) > \inf_{\eta > s} G_s(\eta).$$

Therefore, we can assert that

$$G_s(x) = K + \inf_{\eta > x} G_s(\eta) \quad \forall x \le s.$$

Clearly, the complementarity slackness condition is satisfied. It remains to show that

(16.4.1) $$ AG_s(x) + \alpha G_s(x) \le g(x) + c(\nu - k\tau), \quad x < s $$

(16.4.2) $$ G_s(x) \le K + \inf_{\eta > x} G_s(\eta) \quad \forall x \ge s. $$

But (16.4.1) means

$$ G_s(s) \le g(x) + c(\nu - k\tau), \quad x < s, $$

and from formula (16.3.30) we need to prove

$$ g(s) + \frac{\sigma^2}{2} Q(s) \le g(x), \quad x \le s, $$

which is true since \( Q(s) < 0 \) and \( x \le s \le 0 \).

The proof of (16.4.2) is identical to that of (15.3.20), Theorem 15.2, Chapter 15. This concludes the proof. \(\square\)

## TWO BAND IMPULSE CONTROL PROBLEMS

### 17.1. INTRODUCTION

In the inventory control problems considered in the previous chapters, the impulse control was a replenishment type ordering control. The inventory depleted by the demand had to be replenished from time to time (the impulse times). There are situations in which one may want to reduce the inventory. This will be the case when there is an additional source of supply (the mean reverting rule is one example). It may then not be optimal to accumulate inventory. A typical example is the cash management problem introduced by Constantinides and Richard [17]. For another application see Cadenillas and Zapatero [15]. This chapter is based on Bensoussan, Liu and Yuan [10].

### 17.2. THE PROBLEM

#### 17.2.1. THE MODEL

We consider a probability space \(\Omega, \mathcal{A}, P\) on which is defined a Wiener process \(w(t)\). Let \(\mathcal{F}^t = \sigma(w(s), s \le t)\) An impulse control is a sequence

$$
\theta_n, v_n,
$$

where \(\theta_n\) is a stopping time with respect to the filtration \(\mathcal{F}^t\) and \(v_n\) is a random variable \(\mathcal{F}^{\theta_n}\) measurable. Denoting by \(V\) an impulse control, the corresponding inventory is described by the formula

$$
(17.2.1) \quad y_t(t; V) = x + \mu t + \sigma w(t) + M(t; V),
$$

with

$$
M(t) = M(t; V) = \sum_{\{n|\theta_n < t\}} v_n
$$

In this model the drift term \(\mu t\) combines a mean demand and a fixed resupply policy. The number \(\mu\) is any real number.

Let

$$
f(x) = hx^+ + px^-.
$$

We define the cost functional by

$$
(17.2.2) \quad J_x(V) = E \left[ \sum_{k=0}^{\infty} C(v_k) \exp -a\theta_n + \int_0^{\infty} f(y_x(t; V)) \exp -adt \right],
$$

where

$$
(17.2.3) \quad C(v) = K^+ \mathbb{I}_{v>0} + K^- \mathbb{I}_{v<0} + c^+ v^+ + c^- v^-,
$$

in which \(v^+ = \max(v, 0)\), \(v^- = -\min(v, 0)\) and \(K^+, K^-, c^+, c^-\) are positive constants. Note that the upper symbols +, - have different meanings.

Conversely to the previous models, the impulses can be positive or negative, and they are subject to different fixed and variable costs.

The value function is defined by

$$
u(x) = \inf J_x(V).
$$

#### 17.2.2. Q.V.I.

We write the Q.V.I arising from Dynamic Programming. We consider the operator

$$
(17.2.4) \quad Au(x) = -\frac{1}{2}\sigma^2 u''(x) - \mu u'(x).
$$

The Q.V.I. is given by

$$
(17.2.5) \quad \begin{aligned} Au(x) + \alpha u(x) \le f(x); \\ u(x) \le M(u)(x); \\ (Au(x) + \alpha u(x) - f(x))(u(x) - M(u)(x)) = 0, \end{aligned}
$$

with

$$
M(u)(x) = \inf_{v \neq 0} [C(v) + u(x+v)].
$$

We look for a function which is $C^1$ with linear growth. Standard arguments show that the solution of the Q.V.I. is the value function.

#### 17.2.3. TRANSFORMATION

Define

$$
\begin{aligned}
M^+ u(x) &= \inf_{v \ge 0} (K^+ \mathbf{1}_{v>0} + c^+ v + u(x+v)); \\
M^- u(x) &= \inf_{v \le 0} (K^- \mathbf{1}_{v<0} - c^- v + u(x+v)),
\end{aligned}
$$

then

$$
Mu(x) = \min(M^+ u(x), M^- u(x)),
$$

and the Q.V.I. can be written as follows

$$
(17.2.6) \quad \begin{aligned} Au(x) + \alpha u(x) \le f(x); \\ u(x) \le M^+ u(x); \\ u(x) \le M^- u(x); \\ (Au(x) + \alpha u(x) - f(x))(u(x) - M^+ u(x))(u(x) - M^- u(x)) = 0. \end{aligned}
$$

Introduce the functions

$$
(17.2.7) \quad G^+(x) = u(x) + c^+ x;
$$

$$
(17.2.8) \quad G^-(x) = u(x) - c^- x;
$$

$$
(17.2.9) \quad g^+(x) = f(x) + \alpha c^+ x;
$$

$$
(17.2.10) \quad g^-(x) = f(x) - \alpha c^- x,
$$

then we can write the Q.V.I. in two parts

$$
(17.2.11) \quad \begin{aligned} AG^+ + \alpha G^+ \le g^+(x) - c^+ \mu \\ G^+(x) \le K^+ + \inf_{\eta > y} G^+(\eta) \\ (AG^+ + \alpha G^+ - g^+(x) + c^+ \mu)(G^+(x) - K^+ - \inf_{\eta > y} G^+(\eta)) = 0 \\ \text{if } G^-(x) < K^- + \inf_{\eta < y} G^-(\eta) \end{aligned}
$$
