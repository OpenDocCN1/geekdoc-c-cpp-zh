and

$$g'_s(x-0) = \begin{cases} h, & \text{if } x > 0 \\ -p, & \text{if } x \le 0 \end{cases}$$

The first condition implies

$$[S] + 1 \ge -\frac{ps}{h}.$$

The equality is not possible, because of the assumption hence

$$[S] + 1 > -\frac{ps}{h}.$$

For the second condition we have to consider the case $S - s$ integer or not integer. If it is not an integer then $S$ cannot be integer, but then $H'_s(S-0) = H'_s(S+0) = 0$ which is not possible. If $S$ is integer then the second condition amounts to

$$hS + ps \le 0,$$

hence the result.

We can then compute $H'_s(S)$ by the formula

$$H'_s(S) = \frac{1}{\lambda} \left[ -p \frac{s^2}{2} + p \frac{s}{p} + S \left( ps + h \frac{S+1}{2} \right) \right].$$

To define the optimum $s$ we must write the equation

$$K \lambda = p \frac{s^2}{2} - p \frac{s}{p} - S \left( ps + h \frac{S+1}{2} \right).$$

If we approximate $S$ by $-p \frac{s}{h}$ we deduce easily that $s$ is defined by

(14.7.2) $$s = - \sqrt{\frac{2hK\lambda}{p(h+p)}},$$

and the quantity ordered $S - s$ is given by

(14.7.3) $$S - s = \sqrt{\frac{2K\lambda(p+h)}{ph}}.$$

We see that as $p \to \infty$ we obtain exactly the EOQ formulas.

# LITTLE'S LAW:

Since we have Backlog and waiting time, a natural question is whether Little's Law applies to this model. Waiting starts between the moment the stock is zero till the time it becomes $s < 0$. If $\tau$ denotes this random time we have

$$\tau = \inf \{ t | D(t) = -s \}.$$

To simplify we assume $s$ integer. Then

$$D(\tau) = -s.$$

Since on $0, \tau$ we have

$$x(t) = -D(t),$$

the average backlog is

$$\frac{1}{\tau} \int_0^\tau D(t) dt,$$