**10.3.4. PARTICULAR CASE.** We consider the particular case of an exponential distribution $f(x) = \beta \exp -\beta x$. We recall that $\Gamma(x) = 1 + \beta x$.

Next we have

(10.3.41) 
\(\mu(x) = h - (p + h) \exp -\beta x^+,\)

and

(10.3.42) 
\(g(x) = hx^+ + px^- + (c + p)D - \frac{p+h}{\beta}(1 - \exp -\beta x^+).\)

We next compute the function $H(x)$, for $x > s$. We use the formulas

\(H'(x) = \begin{cases} -p\Gamma(x - s), & \text{if } x < 0 \\ -p\Gamma(x - s) + (p + h)(\Gamma(x) - 1), & \text{if } s < 0 < x \\ h\Gamma(x - s) - (p + h)F(x) - (p + h) \int_s^x \Gamma'(x - \xi)F(\xi)d\xi & \text{if } 0 < s < x \end{cases}\)

hence

\(H'(x) = \begin{cases} -p(1 + \beta(x - s)), & \text{if } x < 0 \\ -p(1 + \beta(x - s)) + (p + h)\beta x, & \text{if } s < 0 < x \\ h(1 + \beta(x - s)) - (p + h) \exp -\beta s & \text{if } 0 < s < x \end{cases}\)

We then obtain, for $x > s$

(10.3.43) 
\(H(x) = -p \left( x - s + \frac{\beta}{2}(x - s)^2 \right) + (h + p) \left[ (x - s^+)^+ (1 - \exp -\beta s^+) + \frac{\beta}{2}(x^+ - s^+)^2 \right].\)

The number $\bar{s}$ satisfies $\mu(\bar{s})=0$, hence

(10.3.44) 
\(\exp -\beta \bar{s} = \frac{h}{p + h}.\)

We thus consider $s \le \bar{s}$. We define $S(s)$ by $H'(S) = 0$, hence

(10.3.45) 
\(S(s) = \frac{p\beta s^- - h(1 - \beta s^+) + (h + p) \exp -\beta s^+}{h\beta}.\)

We can see that $S(\bar{s}) = \bar{s}$, and $S(s)$ is decreasing for $s \le \bar{s}$. Moreover $S(-\infty) = +\infty$.

We next define the value of s. We first obtain the formula

(10.3.46) 
\(H_s(S(s)) = - \frac{1}{2h\beta} [ (h + p) \exp -\beta s^+ - h ]^2 - \frac{\beta p}{2h} (p + h)(s^-)^2 - \frac{p(p + h)}{h} s^-.\)

We can check directly on this formula that $H_s(S(s))$ increases from $-\infty$ to 0, as s grows from $-\infty$ to $\bar{s}$. So there exists a unique s such that $H_s(S(s)) = -K$.

# **Exercise 10.1.** Check that

(10.3.47) 
\(K < \frac{p^2}{2h\beta} \implies (p + h) \exp -\beta s = h + \sqrt{2h\beta K}, s > 0,\)

and for $K > \frac{p^2}{2h\beta}$ then s is the negative root of

(10.3.48) 
\(\frac{s^2\beta(p + h)}{2h} - \frac{sp(p + h)}{h} + \frac{p^2}{2h\beta} - K = 0.\)