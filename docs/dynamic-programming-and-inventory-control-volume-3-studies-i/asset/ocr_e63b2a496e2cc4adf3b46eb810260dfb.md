where \(c\) is the variable cost per unit of order, \(h\) is the holding per unit cost and \(p\) is the shortage per unit cost. We next define the control pay-off

```
(5.2.4) 
\( J_z(V) = \sum_{n=1}^{\infty} \alpha^{n-1} E l(y_n, v_n) \).
```

The value function \( u(x) = \inf J_z(V) \) is solution of Bellman equation

```
(5.2.5) 
\( u(x) = \inf_{v \ge 0} [(x, v) + \alpha E u(x + v - D)] \).
```

# 5.2.2. BELLMAN EQUATION.

Consider the ceiling function

```
(5.2.6) 
\( w_0(x) = \sum_{n=1}^{\infty} \alpha^{n-1} (\Phi^0)^{n-1} (hx^+ + px^-)(x) \).
```

It is easy to check that this series is well defined and

```
(5.2.7) 
\( w_0(x) \le \max(h, p) \left[ \frac{|x|}{1-\alpha} + \frac{\bar{D}}{(1-\alpha)^2} \right] \).
```

Assumptions (4.3.1), (4.3.2), (4.3.6) are satisfied. So results of Theorems 4.3, 4.4, 4.5 are applicable. We can then state

> **Theorem 5.4.** Under the assumptions (5.2.2), (5.2.3) the set of solutions of the functional equation (5.2.5), in the interval \( 0 \le u \le w_0 \) is not empty and has a minimum and a maximum solution \(\underline{u}\) and \(\bar{u}\). The minimum solution is l.s.c. It coincides with the value function. There exists an optimal control policy, obtained through a feedback \(\tilde{v}(x)\).

We turn now to the question of uniqueness. We can check that the properties (4.5.1), (4.5.2) are satisfied. However, only the first part of property (4.5.4) is satisfied. Therefore we cannot directly apply Theorem 4.8. Hence the situation is not similar to that of Theorem 5.1. The key issue is to obtain estimates on the feedback \(\tilde{v}(x)\). The feedback will not be bounded, in the case of high negative inventories. We can state the following important result

> **Proposition 5.1.** The optimal feedback satisfies

```
(5.2.8) 
\( \tilde{v}(x) \le x^- + \frac{\alpha D}{c(1-\alpha)^2} [h + (p+c)(1-\alpha)] \).
```

Proof. We begin by getting an estimate from below of the value function. We shall check that

```
(5.2.9) 
\( u(x) \ge \frac{hx^+}{1-\alpha} + px^- - \frac{h\alpha \bar{D}}{(1-\alpha)^2} \).
```

This estimate is proved by induction. We begin with

```
\( u(x) \ge hx^+ + px^- \),
```

then, using \( u(x) \ge hx^+ \) in the right hand side of equation (5.2.5), we get

```
\(\begin{aligned} u(x) \ge & hx^+ + px^- + \alpha h E(x - D)^+ \\ \ge & hx^+ + px^- + \alpha h(x^+ - \bar{D}) \\ = & hx^+ (1 + \alpha) + px^- - \alpha h \bar{D}. \end\}\)
```

Iterating again we get

```
\( u(x) \ge hx^+ (1 + \alpha + \alpha^2) + px^- - (\alpha + 2\alpha^2)h \bar{D} \).
```