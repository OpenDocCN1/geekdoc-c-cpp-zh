
## 14.5. NEWSVENDOR PROBLEM

We consider here a period T. At the beginning of the period, the inventory is S, the quantity procured. The total demand in the period is D assumed to be random with a probability density function f(x). It materializes during the period at a uniform rate \(\frac{D}{T}\). So the inventory at time t is

\(S - \frac{D}{T}t.\)

This random variable can be positive or negative. When it is positive, it carries a holding cost. When it is negative it carries a shortage cost.

The average inventory surplus is

\(I_+(S) = E[\frac{\int_0^T (S - D\frac{t}{T})^+ dt}{T}] = E\left[ \mathbb{I}_{S>D}(S - \frac{D}{2}) + \mathbb{I}_{S \le D} \frac{S^2}{2D} \right]\)
\(= SF(S) - \frac{1}{2} \int_0^S x f(x) dx + \frac{S^2}{2} \int_S^{+\infty} \frac{f(x)}{x} dx.\)

For the shortage inventory, we have

\(I_-(S) = E[\frac{\int_0^T (S - D\frac{t}{T})^- dt}{T}] = E[\frac{((S - D)^-)^2}{2D}],\)

which is

\(I_-(S) = I_+(S) - S + \frac{1}{2} \int_0^{+\infty} x f(x) dx.\)

We denote by h the holding cost per unit of time and by p the shortage cost per unit of time, so the total cost is

\(C(S) = hI_+(S) + pI_-(S),\)

or

\(C(S) = (h+p) \left[ SF(S) - \frac{1}{2} \int_0^S x f(x) dx + \frac{S^2}{2} \int_S^{+\infty} \frac{f(x)}{x} dx \right]\)
\(+ p \left( -S + \frac{1}{2} \int_0^{+\infty} x f(x) dx \right).\)

We can then compute the optimal \(S = \hat{S}\). We have

\(C'(S) = (h+p) \left( F(S) + S \int_S^{+\infty} \frac{f(x)}{x} dx \right) - p,\)

and

\(C''(S) = (h+p) \int_S^{+\infty} \frac{f(x)}{x} dx > 0.\)

Therefore the unique \(\hat{S}\) is given by

\(F(\hat{S}) + \hat{S} \int_{\hat{S}}^{+\infty} \frac{f(x)}{x} dx = \frac{p}{h+p}\)

### Remark 14.2. Usually the solution of the Newsvendor problem is given as

\(F(\hat{S}) = \frac{p}{h+p}.\)

This is because one assumes that the demand materializes in one shot.

## 14.6. POISSON DEMAND

### 14.6.1. POISSON PROCESS. Instead of modeling the randomness of the demand through a random rate \(\lambda\), we shall consider the demand \(D(t)\) to be a Markov process. In the deterministic case it is simply \(\lambda t\). The most natural stochastic process is the Poisson process with parameter \(\lambda\). We recall the definition of the Poisson process. We have

\(D(0) = 0; D(t_2) - D(t_1) \text{ and } D(s_2) - D(s_1) \text{ are independent } \forall s_1 \le s_2 \le t_1 \le t_2\)

\(D(t_2) - D(t_1) \text{ is integer valued; } P(D(t_2) - D(t_1) = k) = \exp(-\lambda(t_2 - t_1)) \frac{(\lambda(t_2 - t_1))^k}{k!}\)

The following formula expresses the Markov property

\(P(D(t + \epsilon) = D(t)|D(s), s \le t) \sim 1 - \lambda \epsilon \quad P(D(t + \epsilon) = D(t) + 1|D(s), s \le t) \sim \lambda \epsilon\)

The Poisson process models the arrivals of customers at a queue, with average arrival rate \(\lambda\). Note that

\(ED(t) = \lambda t.\)

This last property explains why the Poisson is a natural extension of the deterministic model with constant demand rate \(\lambda\).

The infinitesimal generator of the Markov process \(D(t)\) is the linear operator on smooth functions of the real variable \(x\) defined by

\(A\phi(x) = \lim_{\epsilon \to 0} \frac{\phi(x + D(\epsilon)) - \phi(x)}{\epsilon} = \lambda(\phi(x + 1) - \phi(x))\)

### 14.6.2. DESCRIPTION OF THE MODEL. An impulse control is a sequence

\(\theta_n, v_n,\)

where \(\theta_n\) is a stopping time with respect to the filtration

\(\mathcal{F}^t = \sigma(D(s), s \le t),\)

and \(v_n\) is a random variable \(\mathcal{F}^{\theta_n}\) measurable. Denoting by \(V\) an impulse control, the corresponding inventory is described by the formula

\(y_x(t; V) = x - D(t) + M(t; V),\)

with

\(M(t) = M(t; V) = \sum_{\{n|\theta_n < t\}} v_n\)

Note that the inventory can become negative. Let

\(f(x) = hx^+ + px^-,\)

the cost function to be minimized is given by

\(J_x(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) \exp(-\alpha \theta_n) \right.\)

\(\left. + \int_0^\infty f(y(t)) \exp(-\alpha t) \, dt \right]\)

### 14.6.3. INEQUALITIES FOR THE VALUE FUNCTION.

Considering the value function
\( u(x) = \inf_V J_V(V). \)

We can derive inequalities and complementarity slackness conditions for the function \( u(x) \), which will be referred again as the *Quasi-Variational Inequality*. We first have

(14.6.1) \( u(x) \le K \inf_{v>0} (cv + u(x+v)), \)

then

(14.6.2) \( -\lambda(u(x-1) - u(x)) + \alpha u(x) \le f(x). \)

The complementarity slackness condition expresses

(14.6.3) \( [((\alpha + \lambda)u(x) - \lambda u(x-1)) - f(x)](u(x) - K \inf_{v>0} (cv + u(x+v))) = 0. \)

### 14.6.4. VALUE FUNCTION CORRESPONDING TO AN \( s, S \) POLICY.

Note that \( x \in R \). There is no explicit boundary condition. However \( u(x) \) should not have a growth faster than \( f(x) \) (namely linear growth). In a way similar to that discussed in the deterministic case, the value function corresponding to an \( s, S \) policy is defined as follows. We write

(14.6.4) \( u_s(x) + cx = u_s(s) + cs = K + \inf_{\eta > s} (c\eta + u(\eta)) = K + cS + u(S), \forall x \le s \)

(14.6.5) \( (\alpha + \lambda)u(x) - \lambda u(x-1) - f(x) = 0, \forall x \ge s \)

### Theorem 14.1. Assume

\( p > \alpha c. \)

There exists a unique pair \( s, S \) and a unique continuous function \( u_s(x) \) with linear growth such that equations (14.6.4), (14.6.5) are satisfied.

### PROOF. Noting that

\( u_s(s-1) + c(s-1) = u_s(s) + cs, \)

and

\( (\alpha + \lambda)u_s(s) - \lambda u_s(s-1) = f(s), \)

we get

\( u_s(x) + cx = cs + \frac{f(s) + \lambda c}{\alpha}, \forall x \le s. \)

Define

\( H_s(x) = u_s(x) + cx - cs - \frac{f(s) + \lambda c}{\alpha} \)

We get the following relations for \( H_s(x) \)

(14.6.6) \( (\alpha + \lambda)H_s(x) - \lambda H_s(x-1) = g(x) - g(s), \forall x \ge s; H_s(x) = 0, \forall x \le s, \)

where we have set

\( g(x) = f(x) + \alpha cx. \)

We have

\( g(x) - g(s) = \begin{cases} -(p - \alpha c)(x - s), & \forall x < 0 \\ (h + \alpha c)x + (p - \alpha c)s, & \forall x \ge 0 \end{cases} \)

When \( s < 0 \), we see in particular, thanks to the assumption, that

\( g(x) - g(s) \le 0, \forall s < x < 0. \)

In fact, noting that there exists a unique \( \nu > 0 \) such that \( g(\nu) = g(s) \). We have

\( s < x < \nu \Rightarrow g(x) - g(s) < 0. \)

Define

\( g_s(x) = (g(x) - g(s)) \mathbf{1}_{x > s}. \)

We obtain

(14.6.7) \( H_s(x) = \sum_{j=0}^{\lfloor x-s \rfloor} \frac{g_s(x-j)\lambda^j}{(\alpha+\lambda)^{j+1}}, \forall x \ge s; H_s(x) = 0, \forall x \le s, \)

in which \( \lfloor x \rfloor \) is the integer part of x, the unique integer such that

\( \lfloor x \rfloor \le x < \lfloor x \rfloor + 1. \)

Thanks to the fact that \( g_s(s) = 0 \), we can check that \( H_s(x) \) is a continuous function. The quantity \( S = S(s) \) is obtained by

\( H_s(S) = \inf_{\eta > s} H_s(\eta). \)

Recalling the definition of \( f(x) \) we get at once

\( S(s) = s, \forall s \ge 0 \)

Consider next the case \( s < 0 \). From formula (14.6.7) it follows immediately that

\( s < x < \nu \Rightarrow H_s(x) < 0. \)

We can next write for \( x > \nu \)

\( H_s(x) = \sum_{j=0}^{\lfloor x-\nu \rfloor} \frac{g_s(x-j)\lambda^j}{(\alpha+\lambda)^{j+1}} + \sum_{j=\lfloor x-\nu \rfloor+1}^{\lfloor x-s \rfloor} \frac{g_s(x-j)\lambda^j}{(\alpha+\lambda)^{j+1}}. \)

The first sum is composed of positive terms, and the second of negative terms. We deduce easily the following estimate

\( H_s(x) \ge \frac{g_s(x)}{\alpha+\lambda} + \frac{g_s(0)}{\alpha} \left( \frac{\lambda}{\lambda+\alpha} \right)^{\lfloor x-s \rfloor}, \)

from which it follows that

\( H_s(x) \to +\infty \text{ as } x \to +\infty. \)

Recalling the continuity of \( H_s(x) \) it follows that it reaches its minimum on \( (s, \infty) \). Picking the smallest minimum \( S(s) \) we define the function \( S(s) \) for \( s < 0 \). Necessarily

\( S(s) \ge 0, \)

since \( H_s(x) \) decreases on \( s < x < 0 \). This follows from direct checking of formula (14.6.7).

There remains to find \( s \). It must satisfy the equation in \( s \)

\( \inf_{\eta > s} H_s(\eta) = -K. \)

We have

\( \inf_{\eta > s} H_s(\eta) = 0, \forall s \ge 0. \)
