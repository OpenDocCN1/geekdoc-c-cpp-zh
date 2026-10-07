$\theta = -ln\frac{\lambda_T(e)}{\lambda_C(e)}$

is constant for all values of $	heta$. If we let $D(c_j) = \sum_{i=1}^j d(e_i, c_j)$ be the total number of events observed at calendar time $c_j$ and $r$ be the fraction of patients randomized to treatment $	au$, then $L(c_j)$ is asymptotically normal with the following mean and variance

$E[L(c_j)] = \theta D(c_j)r(1-r)$.

$Var[L(c_j)] = D(c_j)r(1-r)$.

It can be shown that the sequential log-rank score statistics, $L(c_1), L(c_2), \dots, L(c_j)$ have independent increments, that is, if $j_1 < j_2$, $L(c_{j_1})$ and $L(c_{j_2})-L(c_{j_1})$ are independent [20].

Similarly, if we define the treatment effect to be the log of ratio of hazard functions above, then the null hypothesis is

$H_0 \quad \theta = 0$

and the alternative hypothesis is

$H_1 \quad \theta = \theta_1$

Instead of defining the information fraction on sample sizes as before, we define it as the ratio of the total number of events at $c_j$ to that at $c_J$

$t_j = \frac{D(c_j)}{D(c_j)}$

In addition, we have the stochastic increment statistic as

$S(t_j) = \frac{L(c_j)}{\sqrt{D(c_j)r(1-r)}}$

and

$D(c_j) = \frac{l_j}{r(1-r)}$