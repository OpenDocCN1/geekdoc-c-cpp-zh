Define

$$B(x) = H(x) - \inf_{\eta \ge x} H(\eta).$$

So we want to prove

$$B(x) \le K.$$

For $x \le s$ we have

$$B(x) = - \inf_{\eta \ge x} H(\eta) = - \inf_{\eta \ge x} H(\eta) = K.$$

Consider the first point $x_0$ such that $x_0 > s$ and $H(x_0) = 0$, $H(x) \le 0, \forall x \le x_0$. For $s \le x \le x_0$ we have

$$B(x) \le - \inf_{\eta \ge x} H(\eta) \le - \inf_{\eta \ge x} H(\eta) = K.$$

It remains to consider the case $x > x_0$. Assume that there exists a point $x' > x_0$ such that $B(x') \ge K$. Then there will exist a point $x'$ s.t. that

$$\bar{s} < x_0 \le x', B(x') = 0, B(x) < K, x < x'.$$

Define the point $x_3$ such that

$$H(x_3) = \inf_{\eta \ge x'} H(\eta).$$

The point $x_3$ is uniquely defined as the smallest infimum beyond $x'$. Moreover $x_3 \neq x'$ since

$$B(x') = H(x') - H(x_3) = K.$$

Next define $x_2$ such that

$$H(x_2) = \max_{\eta \le x_3} H(\eta) = \max_{s \le \eta \le x_3} H(\eta).$$

We take $x_2$ the smallest maximum. Then we can assert that $x_2 \ge x'$. Indeed if $x_2 < x'$ then

$$\inf_{\eta \ge x_2} H(\eta) \le \inf_{\eta \ge x'} H(\eta),$$

and

$$H(x_2) - \inf_{\eta \ge x_2} H(\eta) \ge H(x') - \inf_{\eta \ge x'} H(\eta) = K,$$

which will contradict the definition of $x'$. Hence $x' \le x_2 \le x_3$. Moreover $x_2 \neq x_3$ since

$$H(x_2) - H(x_3) \ge H(x') - H(x_3) = B(x') = K.$$

Let us check now that

(9.3.23) $$H(x) - H(y) \le H(x_2) - H(x_3), \forall x \le y \le x_3.$$

Indeed if $x < x'$ then

$$H(x) - H(y) \le H(x) - \inf_{\eta \ge x} H(\eta) < K \le H(x_2) - H(x_3).$$

Next if $x' \le x \le y \le x_3$ then

$$H(x) - H(y) \le H(x_2) - H(x_3).$$

Collecting results we note

$$s < \bar{s} < x_0 \le x' \le x_2 < x_3.$$