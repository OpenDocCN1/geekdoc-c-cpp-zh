exactly half its entries equal to 0 and half equal to 1, implying that

$$\sum_{u \in v+C} wt(u) = \frac{nM}{2}$$

or equivalently,

$$\sum_{i=0}^n i A_i(v) = \frac{nM}{2}.$$ (11.2)

where $\{A_i(v) \mid 0 \le i \le n\}$ is the weight distribution of $\mathbf{v} + \mathcal{C}$. Equation (11.2) implies that the average distance between $\mathbf{v}$ and the codewords of $\mathcal{C}$ is $n/2$. Therefore the distance between $\mathbf{v}$ and some codeword $c \in \mathcal{C}$ is at most $n/2$. By Theorem 11.1.2(i) we have part (i).

Now assume that $\mathcal{C}$, and hence $\mathbf{v} + \mathcal{C}$, has strength 2. In each row of $M_t$ corresponding to the vector $\mathbf{u} \in \mathbf{v} + \mathcal{C}$, there are $\binom{n}{2}$ ordered pairs of bits. Each block of $\binom{n}{2}$ pairs of distinct columns of $M_t$ contains the binary 2-tuple $(1, 1)$ exactly $M/4$ times. Therefore

$$\sum_{u \in v+C} \binom{wt(u)}{2} = \sum_{u \in v+C} \frac{wt(u)(wt(u)-1)}{2} = \binom{n}{2} \frac{M}{4} = \frac{n}{2} \frac{n-1}{2} \frac{M}{4}.$$

Using (11.2) we obtain

$$\sum_{i=0}^n i^2 A_i(v) = \frac{n(n+1)M}{4}.$$ (11.3)

Combining (11.2) and (11.3) produces

$$\sum_{i=0}^n (2i-n)^2 A_i(v) = nM.$$ (11.4)

This implies that there is an $i$ with $A_i(v) \neq 0$ such that $(2i-n)^2 \ge n$. Taking the square root of both sides of this inequality shows that either $i \le \frac{n-\sqrt{n}}{2}$ or $i \ge \frac{n+\sqrt{n}}{2}$.

Suppose now that $\mathcal{C}$ is self-complementary. By Exercise 629, $\mathbf{v} + \mathcal{C}$ is also self-complementary. Then there is an $i$ satisfying the first of the above two inequalities with $A_i(v) \neq 0$. Thus there is a vector $\mathbf{u} \in \mathbf{v} + \mathcal{C}$ with $wt(u) \le (n-\sqrt{n})/2$. Hence (ii) holds.

In the case of binary linear codes, the Norse Bounds can be restated as follows.

**Corollary 11.2.2** Let $\mathcal{C}$ be a binary linear code of length $n$.

+   (i) If $C^\perp$ has minimum distance at least 2, then $\rho(C) \le \lfloor n/2 \rfloor$.

+   (ii) If $C^\perp$ has minimum distance at least 4 and the all-one vector $\mathbf{1}$ is in $C$, then $\rho(C) \le \lfloor (n-\sqrt{n})/2 \rfloor$.

**Exercise 630** Prove Corollary 11.2.2.

**Exercise 631** Let $\mathcal{C}$ be a self-complementary binary code of strength 2 with $\rho(C) = (n-\sqrt{n})/2$, and let $\mathbf{v} + \mathcal{C}$ have minimum weight $\rho(C)$. Show that half the vectors in $\mathbf{v} + \mathcal{C}$