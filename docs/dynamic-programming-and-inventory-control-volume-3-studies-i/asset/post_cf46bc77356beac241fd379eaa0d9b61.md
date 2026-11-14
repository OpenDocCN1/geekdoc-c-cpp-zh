

PROOF. Note that, by the definition of the $S_i$, one has

$$G_{i+1}(S_i) - G_i(S_i) \ge G_{i+1}(S_{i+1}) - G_i(S_{i+1}),$$

hence

$$(c_{i+1} - c_i)S_i \ge (c_{i+1} - c_i)S_{i+1},$$

and thus

$$S_i \le S_{i+1}.$$

One has also the property

### Lemma 11.2.

If $s_i \le s_j$, for $i \le j$ then $w_i(x) \ge w_j(x) \forall x$

**Proof.** If $x \le s_i$ then

$$\begin{aligned} w_i(x) &= -c_i x + G_i(s_i) \\ &= -c_i x + (c_i - c_j)s_i + G_j(s_i) \\ \ge -c_i x + (c_i - c_j)s_i + G_j(s_i) \\ &= -c_i x + (c_i - c_j)s_i + w_j(x) + c_j x \\ \ge w_j(x) \end{aligned}$$

If $s_i \le x \le s_j$, then

$$\begin{aligned} w_i(x) &= -c_i x + G_i(x) \\ &= -c_i x + G_j(x) \\ \ge -c_i x + G_j(s_i) \\ &= w_j(x) \end{aligned}$$

Finally, if $x \ge s_j, w_i(x) = w_j(x)$

This concludes the proof.

It follows that the supplier $i$ can be discarded. So there remains a number $m \le M$ of suppliers with the following configuration

$$s_m < s_{m-1} < \cdots < s_1 \le S_1 \le \cdots \le S_m.$$

We now define the concept of generalized $s, S$ policy (see statement of Theorem. It consists in a double sequence

$$s_m^* < s_{m-1}^* < \cdots < s_i^* < S_i < S_2 \cdots < S_m,$$

with the feedback

$$\delta(x) = \begin{cases} S_m, & \text{if } x \le s_m^* \\ S_i, & \text{if } s_{i+1}^* < x \le s_i^*, i = 1, \cdots, m-1 \\ x, & \text{if } x > s_1^* \end{cases}$$

Recalling that $\delta(x) = \delta_{i(x)}(x)$, we see that a generalized $s, S$ policy is possible only if

$$s_i^* \le s_i, s_1^* = s_1.$$

We can formulate the main result of the optimization problem as follows

### Theorem 11.4.

The function \( w(x) \) in (11.2.10) is obtained through a generalized \( s,S \) policy. Namely, there exists \( m \le M \), and a subset of \( [1, \cdots, M] \), which we can renumber in increasing order as \( [1, \cdots, m] \), and an associated sequence \( s_i^* \), with \( s_i^* > s_{i+1}^*, s_i^* \le s_i, s_1^* = s_1 \), such that

$$w(x) = \begin{cases} -c_m x + G_m(s_m), & \text{if } x \le s_m^*, i(x) = m \\ -c_i x + G_i(s_i), & \text{if } s_{i+1}^* < x \le s_i^*, i=1, \cdots, m-1, i(x)=i \\ -c_1 x + G_1(x), & \text{if } x > s_1^* = s_1, \text{no order} \end{cases}$$

**Proof.** Define

$$s_{ij} = \frac{G_i(s_i) - G_j(s_j)}{c_i - c_j};$$

$$s_j^* = \min \left( s_{j1}, \min_{i=1,\cdots,j-1} s_{ij} \right).$$

We shall prove that

$$i(x) \text{ may be chosen } \ge j \text{ if } x \le s_j^*$$
$$i(x) \text{ may be chosen } \le j - 1 \text{ if } x > s_j^*$$

Indeed, if \( x \le s_j^* \), then

$$w_j(x) = -c_j x + G_j(s_j),$$

and for \( i \le j-1, x \le s_{ij} \) implies

$$x \le \frac{G_i(s_i) - G_j(s_j)}{c_i - c_j}.$$

Therefore

$$w_j(x) \le -c_i x + G_i(s_i), \forall i \le j-1.$$

However

$$w_i(x) = \begin{cases} -c_i x + G_i(s_i), & \text{if } x \le s_i \\ -c_{i+1} x + G_i(x), & \text{if } x > s_i \end{cases}$$

Note also

$$w_i(x) \le -c_i x + G_i(x), \forall x.$$

Hence if \( x \le s_i \), we can assert that \( w_i(x) \ge w_j(x) \). On the other hand, if \( x > s_i \), then \( w_i(x) = -c_{i+1}x + G_i(x) \ge w_j(x) \). So the first part is proven.

Suppose now that \( x > s_j^* \), we show that there is some \( i \le j-1 \), such that \( w_i(x) \le w_j(x) \). There are several cases. If \( s_j^* = s_i \), then \( w_j(x) = -c_j x + G_j(x) \), hence

$$w_j(x) = -c_i x + G_i(x) \ge w_i(x) \forall i \neq j.$$

Suppose \( s_j^* = \min_{i=1,\cdots,j-1} s_i < s_j \), then if \( x \ge s_j \) we have the same situation as before. There remains the case when \( s_j^* < x < s_j \). In that case, \( w_j(x) = -c_j x + G_i(s_i) \), and there exists \( i \le j-1 \), such that \( s_{ij} = s_j^* < x \), which implies \( w_j(x) > -c_{i+1}x + G_i(s_i) \). Moreover \( s_i > s_j \), since \( i \le j-1 \). Hence \( x < s_i \), and \( w_i(x) = -c_{i+1}x + G_i(s_i) \). We get immediately \( w_i(x) < w_j(x) \). So we have proven that there exists \( i \le j-1 \), better or equivalent to \( j \).

It follows that

$$s_i^* \le s_j^*$$

then the supplier \( i \) can never be chosen. Indeed, we know that if \( x \le s_j^* \), we can chose among the suppliers \( j, \cdots, M \), hence index i may be out. On the other hand if \( x > s_j^* \ge s_i^* \), then i as well as j may be excluded. So we eliminate all the indices i, such that there exists \( j > i \), with \( s_i^* \le s_j^* \). There remains m indices, with decreasing $s_i^*$. We may renumber them and define in this way the sequence $s_1^* > s_2^* > \dots > s_m^*$. It follows that if $s_{i+1}^* < x \le s_i^*$, then $i(x)$ can be chosen among the indices larger or equal to $i$, but we may exclude $i+1, \dots, m$, hence $i$ is optimal. If $x > s_1^* = s_1$, we may eliminate all indices, hence it is optimal not to order.

The proof has been completed.

We now prove some properties of the function $w$

### Corollary 11.1.

The function $w(x)$ is decreasing on $(-\infty, a_1]$, and $w(x) + c_1 x$ is $K_1$ nondecreasing on $[a_1, +\infty)$.

**Proof.** Recall that $w(x)$ is continuous. From the formula proved in Lemma 11.4 it follows that $w(x)$ decreases on $(-\infty, s_1]$ and from the properties of $G_1$ also decreasing on $(s_1, a_1)$. The second part is obvious.

Let us check additional properties of $w$.

### Corollary 11.2.

$w(x) + c_i x$ is $K_i$ nondecreasing on the whole line $R$. Assume $a_m \ge 0$, then $w(x) + c_m x$ is decreasing on $(-\infty, 0]$.

**Proof.** Noting that $G_i(x) = G_1(x) + (c_i - c_1)x$.

We can write $G_i^*(x) = \inf_{y \ge x} \{ K_i \mathbb{I}_{y > x} + G_1(y) - c_1 y + c_i y \}$.

Since $w_i(x) = -c_i x + G_i^*(x)$.

it follows that $w_i(x) = \inf_{y \ge x} \{ K_i \mathbb{I}_{y > x} + c_i(y - x) + G_1(y) - c_1 y \}$.

It follows that $w(x) = \inf_{z \ge x} \{ C(z - x) + G_1(z) - c_1 z \}$.

where $C(z) = \min_{i=1}^m \{ K_i \mathbb{I}_{z > 0} + c_i z \}$.

Take $y \ge x$, then $w(x) \le \inf_{z \ge y} \{ C(z - x) + G_1(z) - c_1 z \}$.

and from the subadditivity of $C(z)$, and $z \ge y \ge x$, it follows $w(x) \le w(y) + C(y - x)$.

from which we deduce $w(x) \le w(y) + K_i + c_i(y - x), \forall i$.

Hence $w(x) + c_i x$ is $K_i$ nondecreasing on the whole line $R$. Next

$$w(x) + c_m x = \begin{cases} G_m(s_m), & \text{if } x \le s_m^* \\ (c_m - c_i)x + G_i(s_i), & \text{if } s_{i+1}^* < x \le s_i^* \\ (c_m - c_1)x + G_1(x), & \text{if } x > s_1^* \end{cases}$$

In fact, one observes that $w(x) + c_m x = G_m(x), \text{ if } x > s_1^*$.

From the above expression, using $c_m \le c_i, \forall i$, and the fact that $a_m \ge 0$, hence $G_m(x)$ is decreasing on $(-\infty, 0]$, the second part of Corollary 11.2 follows.

## 11.2.3. APPLICATION TO THE MULTI-SUPPLIER PROBLEM.

To apply the preceding results to the multi-supplier problem, we need an additional intermediary result. Consider a function $\psi(x)$, piecewise continuous, which tends to $+\infty$ as $|x| \to +\infty$, hence attains its minimum. Let $D$ be a positive random variable, with density $f$. The quantity $\chi(x) = E\psi(x - D)$, is a continuous function, which also tends to $+\infty$ as $x \to +\infty$.

Exercise 11.6. Prove the preceding property. Use the fact that $\psi(x)$ reaches its minimum.

However, if $\psi$ decreases on $(-\infty, a]$, and is non $K$ decreasing, on $[a, +\infty)$, then this property does not carry over to $\chi$. The same bad situation occurs whenever $\psi$ is quasi $K$ convex. In the case of $K$ convexity, the property carries over. Note however, that $\chi(x)$ decreases on $(-\infty, a]$, and since it goes to $+\infty$ as $x \to +\infty$, there is necessarily some $b \ge a$, such that $\chi(x)$ decreases on $(-\infty, b]$, and may increase after. So $b$ is a local minimum. We want to restrict ourselves to distributions $f$ such that the following property $\mathcal{P}$ holds: The function $\chi$ is non $K$ decreasing on $[b, +\infty)$.

Let us show that the property $\mathcal{P}$ holds, whenever the distribution $f$ is Poisson, or a convolution of Poisson distributions. Suppose $f$ is a Poisson distribution, with parameter $\lambda$, then $f(x) = \lambda \exp -\lambda x$.

Exercise 11.7. Check that $\chi'(x) = \lambda(\psi(x) - \chi(x))$.

Let $S$ be the minimum of $\chi$. Since $\chi'(b) = \chi'(S) = 0$, we have $\chi(S) = \psi(S)$ and $\chi(b) = \psi(b)$. Let $h > 0$. Consider the function $z(x) = \chi(x) - \chi(x + h) - K$, then we have $z(b) \le \chi(b) - \chi(S) - K = \psi(b) - \psi(S) - K \le 0$, since $a \le b \le S$.

Exercise 11.8. Check that $z'(x) \le -\lambda z(x)$.

Therefore $\frac{dz}{dx} \exp \lambda x \le 0$,

and it follows that $z(x) \exp \lambda x \le z(b) \exp \lambda b, \forall x \ge b$, hence $z(x) \le 0, \forall x \ge b$. This implies that $\chi$ is $K$ nondecreasing for $x \ge b$. The property $\mathcal{P}$ carries over to convolutions of Poisson distributions. Indeed, if $D = \sum_{j=1}^J D_j$,

