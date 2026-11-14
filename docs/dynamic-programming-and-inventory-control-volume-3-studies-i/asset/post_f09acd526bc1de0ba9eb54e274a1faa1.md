
define in a unique way this point. This point is strictly positive, since \(G'_n(x, Q) \le c(1-\alpha) - \alpha p < 0, \forall x \le S\). It follows that we can write \(u_{n+1}(x, Q)\) as follows

```
\(\begin{align*} u_{n+1}(x, Q) = \begin{cases} hx^+ + px^- - cx + G_n(x+Q, Q), & \text{if } x < S_n(Q) - Q \\ hx^+ + px^- - cx + G_n(S_n(Q), Q), & \text{if } S_n(Q) - Q < x < S_n(Q) \\ hx^+ + px^- - cx + G_n(x, Q) & \text{if } x > S_n(Q) \end{cases} \end{align*}\)
```

We then check that \(u_{n+1}(x, Q)\) has the same properties as \(u_n(x, Q)\). Note that \(S_n(Q)\) is decreasing in \(Q\).

From the convexity of \(u_n(x, Q)\) we deduce that the limit \(u(x, Q)\) is convex.

Since \(u(x, Q) \ge u_n(x, Q)\), we obtain that \(u(x, Q) \to +\infty\) as \(|x| \to +\infty\). Also \(G(x, Q)\) defined by (11.1.5) is convex, continuous and \(\to +\infty\) as \(|x| \to +\infty\). The function \(G(x, Q)\) attains its minimum in a point \(S(Q)\) and by taking the smallest minimum, we can define \(S(Q)\) in a unique way. The formulas (11.1.6) define an optimal feedback. Let us now prove that \(u(x, Q)\) is \(C^1\), except in 0. We first notice the estimate

```
\(|u'_n(x, Q)| \le \frac{\max(h, p) + c}{1 - \alpha}.\)
```

Therefore, the limit \(u(x, Q)\) is Lipschitz continuous. But then \(G(x, Q)\) is \(C^1\), since

```
\(G'(x, Q) = c + \alpha \int_{-\infty}^x u'(z, Q) f(x-z) dz,\)
```

and \(G'(S(Q), Q) = 0\). The function

```
\(g(x, Q) = \inf_{x \le z \le x+Q} G(z, Q),\)
```

is also \(C^1\). Therefore

```
\(u(x, Q) = hx^+ + px^- - cx + g(x, Q),\)
```

is also \(C^1\), except at 0. Since \(G'(0, Q) \le c(1-\alpha) - \alpha p < 0, S(Q) > 0\). We can also check that \(S(Q)\) is decreasing and that \(u'(x, Q)\) is monotone increasing in \(Q\).

The proof has been completed.

### Remark 11.1.

There is no explicit formula for \(S(Q)\). It satisfies

```
\(c + \alpha Eu'(S(Q) - D) = 0.\)
```

However, unlike the case \(Q = +\infty\), one cannot express explicitly \(Eu'(S(Q) - D)\). Define

```
\(\begin{align*} z(x) &= u'(x) - h \mathbb{1}_{x > 0} + p \mathbb{1}_{x < 0} + c \\ g(x) &= c(1-\alpha) + \alpha h - \alpha (p+h) \bar{F}(x), \end{align*}\)
```

then the condition becomes

```
(11.1.10) \(g(S(Q)) + \alpha Ez(S(Q) - D) = 0.\)
```

When \(Q = +\infty, z(x) = 0, \forall x \le S\), but it is not true when \(Q\) is finite. The function \(z(x)\) is the solution of the problem

```
(11.1.11) \(z(x) = \begin{cases} g(x+Q) + \alpha Ez(x+Q-D), & \text{if } x < S(Q) - Q \\ 0 & \text{if } S(Q) - Q < x < S(Q) \end{cases}\)
```

It suffices to define \(z(x)\) for \(x \le S(Q) - Q\). We get the problem

```
\(z(x) = g(x+Q) + \alpha Ez(x+Q-D) \mathbb{1}_{D > (x+2Q-S(Q))^+},\)
```

which is equivalent to the integral equation

(11.1.12) 
\( z(x) = g(x+Q) + \alpha \int_{-\infty}^{\min\{x+Q, S\}} z(\eta) f(x+Q-\eta) d\eta. \)

For each \( S > 0 \), we solve the integral equation (11.1.12). We then define \( S(Q) \) by the algebraic equation (11.1.10).

The case of a set-up cost is open. It is unlikely that the optimal feedback is given by a \( s(Q), S(Q) \) policy.

## 11.2. MULTI SUPPLIER PROBLEM

### 11.2.1. DESCRIPTION OF THE PROBLEM.

We present here a problem considered by E. Porteus, [33]. It generalizes the problem of inventory control with set-up cost developed in Chapter 9. For ordering, one supposes now that there are multiple supplier sources. More precisely the ordering cost function is given by

(11.2.1) 
\( C(z) = \begin{cases} 0, & \text{if } z=0 \\ \min_i(K_i + c_i z) & \text{if } z>0 \end{cases} \, \)

with

(11.2.2) 
\( c_1 > c_2 > \cdots > c_M > 0, \quad 0 < K_1 < K_2 < \cdots < K_M. \)

The variable costs and the fixed costs vary in the opposite way. So there is not a single supplier which combines the cheapest variable and fixed costs. A trade off is possible. This is, of course, the source of the difficulty.

### Exercise 11.1.

Show that a function \( C(z) \) is a concave function on \( z \ge 0 \) and \( C(0) = 0 \). Show that a function \( C(z) \), which is concave on \( R^+ \) and vanishes at 0, verifies the sub additivity property

(11.2.3) 
\( C(z_1 + z_2) \le C(z_1) + C(z_2). \)

### Exercise 11.2.

Show the following property

\( C(z) = \left\{ \begin{array}{l} \min_{v_1 + \cdots + v_M = z \\ v_i \ge 0} \sum_{i=1}^M (K_i \mathbb{1}_{v_i > 0} + c_i v_i). \end{array} \right. \)

This is proven by recurrence on \( M \). It can be interpreted as the fact that there is no point splitting the order among the suppliers. One needs to select a single supplier.

We consider the dynamic inventory control problem with backlog. We can easily write the DP equation.

(11.2.4) 
\( u(x) = hx^+ + px^- + \inf_{i=1,\dots,M \\ \eta \ge x} [K_i \mathbb{1}_{\eta > x} + c_i(\eta - x) + \alpha E u(\eta - D)]. \)

If we set

(11.2.5) 
\( w(x) = u(x) - hx^+ - px^- , \)

the D.P. equation is equivalent to

(11.2.6) 
\( w(x) = \inf_{\eta \ge x} [C(\eta - x) + \alpha E(h(\eta - D)^+ + p(\eta - D)^- + w(\eta - D))]. \)

It is convenient to introduce the following notation. Define

$$g_i(x) = c_i(x + \overline{D}) + \alpha(w(x) + hx^+ + px^-),$$

and

$$G_i(x) = E g_i(x - D).$$

Let also

$$G_i^*(x) = \min \left[ G_i(x), \inf_{y \ge x} (K_i + G_i(y)) \right] = \inf_{y \ge x} (K_i \mathbb{1}_{y > x} + G_i(y)),$$

and

$$w_i(x) = -c_i x + G_i^*(x).$$

Finally the DP equation (11.2.6) becomes

$$w(x) = \min_{1 \le i \le M} w_i(x).$$

The objective is to prove the following result

### Theorem 11.3.

Assume (11.11), (11.2) and

$$(11.2.7) \quad c_1 - \alpha c_M - \alpha p < 0,$$

and a restriction on the probability density of the demand, namely property $\mathcal{P}$, below ($f$ is Poisson or a convolution of Poisson). Then the feedback $\delta(x)$ in the right hand side of (11.2.4), is given by a generalized s,S policy. This means that there exists a double sequence

$$(11.2.8) \quad s_m^* < s_{m-1}^* < \cdots < s_1^* < S_1 < S_2 \cdots < S_m, \quad 1 \le m \le M,$$

with the feedback

$$(11.2.9) \quad \delta(x) = \begin{cases} S_m & \text{if } x \le s_m^* \\ S_i & \text{if } s_{i+1}^* < x \le s_i^*, i=1, \cdots, m-1 \\ x & \text{if } x > s_1^* \end{cases}$$

## 11.2.2. AUXILIARY RESULTS

We will need some extension of the K convexity theory. We start with functions $G_i(x)$, satisfying algebraic properties. Later on, we will show that the functions, with the same notation, defined in the previous section satisfy these properties.

Consider functions $G_i(x)$, $i = 1, \cdots, M$, which are continuous, $G_i(x) \to \infty$ as $|x| \to +\infty$. We assume that there exists $a_i$ such that $G_i(x)$ is decreasing on $(-\infty, a_i]$, and verifies

$$G_i(x) < K_i + G_i(y), \forall a_i < x < y.$$

We say that $G_i(x)$ is $K_i$ nondecreasing on $[a_i, +\infty)$. We also assume the relations

$$G_{i+1}(x) - G_i(x) = (c_{i+1} - c_i)x.$$

We set

$$G_i^*(x) = \inf_{y \ge x} (K_i \mathbb{1}_{y > x} + G_i(y)),$$

and

$$w_i(x) = -c_i x + G_i^*(x).$$

Finally, we are interested in computing

$$(11.2.10) \quad w(x) = \min_{1 \le i \le M} w_i(x).$$

The optimization problem is in two steps. For each $i$ find the optimal

$\bar{y}_i = \delta_i(x)$,

which achieves the minimum in $y$ in the definition of $G_i^*(x)$. Then find the right index $i(x)$ in the definition of $w(x)$. The feedback function, which expresses the order as a function of the inventory is given by

$\bar{y} = \delta(x) = \delta_{(i(x))}(x)$.

Beyond the indexing, the framework is reminiscent of $K$ convexity. However, the functions $G_i(x)$ are not $K_i$ convex, but they enjoy a close property, the quasi $K_i$ convexity. Dropping the index, we define the $K$ quasi convexity by

$G(\theta x + (1-\theta)y) \le \max[G(x), K + G(y)], \forall x \le y$

### Exercise 11.3.

Show the $K$ quasi convexity property of the functions $G_i(x)$. Show also that a $K$ convex function is $K$ quasi-convex.

### Exercise 11.4.

Give an example of a function which is decreasing in $(-\infty, a]$, $K$ nondecreasing in $[a, \infty)$, and which is not $K$ convex.

The first easy thing is to check that the $\delta_i(x)$ are given by a $s_i, S_i$ policy. Indeed there exist

$s_i \le a_i \le S_i$,

such that

$G_i(S_i) = \min_y G_i(y)$,

and

$G_i(s_i) = K_i + G_i(S_i)$.

Then clearly

$\delta_i(x) = \begin{cases} S_i, & \text{if } x \le s_i \\ x, & \text{if } x > s_i \end{cases}$

Note also the property

$G_i(x) \le G_i(s_i), \text{ for } s_i \le x \le S_i$

### Remark 11.2.

If the function $G_i(x)$ is $K_i$ convex, then we can associate to it, $s_i, S_i$ satisfying the properties above. By taking $a_i = s_i$, we see that the properties of decreasing on $(-\infty, a_i]$ and $K_i$ nondecreasing on $[a_i, \infty)$ are satisfied.

We note that

$G'_i(x) = \begin{cases} G_i(s_i), & \text{if } x \le s_i \\ G_i(x), & \text{if } x \ge s_i \end{cases}$

So it is a continuous function and $w_i(x)$ is also continuous.

### Exercise 11.5.

Show that $w(x)$ is also continuous.

One has the property

### Lemma 11.1.

$a_1 \le S_1 \le S_2 \le \cdots \le S_M$.
