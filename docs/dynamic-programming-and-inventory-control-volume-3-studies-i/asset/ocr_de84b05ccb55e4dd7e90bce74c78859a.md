Consider now $x \ge 0$ with $[s] < s$. Consider $n - 1 < x < n$, then $[x] = n - 1$ and

$$H'_s(n-1+0) = \frac{h + \alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^n \right) - \frac{p - \alpha c}{\alpha} \left( \frac{\lambda}{\lambda + \alpha} \right)^n \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^{-[s]} \right),$$

$$H'_s(n-1-0) = \frac{h + \alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^{n-1} \right) - \frac{p - \alpha c}{\alpha} \left( \frac{\lambda}{\lambda + \alpha} \right)^{n-1} \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^{-[s]+1} \right).$$

Then for $n - 1 < x < n + [-s] + s$ we have

$[x - s] = n - 1 + [-s], \quad H'_s(x) = H'_s(n - 1 + 0),$

and for $n + [-s] + s < x < n$ we have

$[x - s] = n + [-s], \quad [x - s] - [x] = [-s] + 1$

and

$$H'_s(x) = \frac{h + \alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^n \right) - \frac{p - \alpha c}{\alpha} \left( \frac{\lambda}{\lambda + \alpha} \right)^n \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^{-[s]+1} \right) = H'_s(n - 0).$$

We have a discontinuity at $n + [-s] + s$ given by

$$H'_s(n + [-s] + s + 0) - H'_s(n + [-s] + s - 0) = H'_s(n - 0) - H'_s(n - 1 + 0) = - \frac{p - \alpha c}{\alpha + \lambda} \left( \frac{\lambda}{\lambda + \alpha} \right)^{n - [s]}. $$

So for $x \ge 0, [s] < s H'_s(x)$ has discontinuity points at $x = n$ and $x = n + [-s] + s, n > 0$. It is piecewise constant, but not increasing. It increases at $n$ and decreases at $n + [-s] + s$. However

$$H'_s(n+1+0) - H'_s(n+0) = \frac{1}{\lambda + \alpha} \left( \frac{\lambda}{\lambda + \alpha} \right)^{n+1} \left[ h + \alpha c + (p - \alpha c) \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^{-[s]} \right) \right]$$

The minimum $S(s)$ must satisfy $H'_s(S + 0) \ge 0$. Therefore $S$ is necessarily an integer. If $s$ is an integer, we deduce

$H'_s(x + 0) \ge 0, \forall x > S.$

Hence

$H_s(x) = \inf_{y > x} H_s(y), \forall x \ge S.$

Now for $s \le x \le S$ we have

$H_s(x) \le 0,$

and

$\inf_{\eta > s} H_s(\eta) = H_s(S) = -K$

If $s$ is not an integer, we can only deduce

$H'_s(n + 1 + 0) \ge H'_s(n + 0) \ge 0, \forall n > S.$

We may have some negative values of the derivative. This can occur at intervals $(n + [-s] + s, n)$. However, we know that for $x \ge s$

$H_s(x) \le K + H_s(x + \xi), \forall \xi \ge 0$