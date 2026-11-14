of them, we define uniquely the number \( S(s) \). Note also, that if \( s \ge \bar{s} H_s(x) \) is increasing in \( x \), and for \( s < \bar{s} H_s(x) \) is decreasing in \( x \) on the interval \( [s, \bar{s}) \), hence \( S(s) = s \) if \( s \ge \bar{s} \), \( S(s) > s \) if \( s < \bar{s} \).

It follows also that \( H'_s(S(s)) = 0 \) for \( s < \bar{s} \). Therefore

\(\frac{dH_s(S(s))}{ds} = \frac{\partial}{\partial s} H_s(x)_{x=S(s)}, \text{ if } s < \bar{s}.\)

So

(9.2.18) \(\frac{dH_s(S(s))}{ds} = -\mu(s)\Gamma(S(s) - s) > 0, \text{ if } s < \bar{s}.\)

Clearly \( H_s(S(s)) = 0 \) for \( s \ge \bar{s} \). The property (9.2.16) has been proven.

Consider now \( S_0 = S(0) \). We have

\( H_0(x) = \int_0^x \Gamma(\xi)\mu(x - \xi)d\xi. \)

So

\( H'_0(x) = \mu(0)\Gamma(x) + \int_0^x \mu'(x - \xi)\Gamma(\xi) d\xi \)
\( = (c - p)\Gamma(x) + (p - \alpha(c - h)) \int_0^x f(x - \xi)\Gamma(\xi) d\xi. \)

However it is easy to check that \( \Gamma(x) \) satisfies the renewal equation

(9.2.19) \( \Gamma(x) = 1 + \alpha \int_0^x f(x - \xi)\Gamma(\xi) d\xi. \)

Therefore

\( H'_0(x) = \frac{1}{\alpha}[(p - \alpha(p - h))\Gamma(x) - (p - \alpha(c - h))]. \)

Therefore \( S_0 \) is given by

(9.2.20) \( \Gamma(S_0) = \frac{p - \alpha(c - h)}{p - \alpha(p - h)}. \)

We shall need the assumption

(9.2.21) \( H_0(S_0) = \int_0^{S_0} \Gamma(\xi)\mu(S_0 - \xi)d\xi < -K. \)

We can then state the following

**Theorem 9.4.** Under the assumptions of Theorem 9.3 and (9.2.12), (9.2.21), the optimal feedback \( \psi(x) \) of the functional equation (9.2.5) is given by an \( s, S \) policy. The value of \( s \) is the unique value such that

(9.2.22) \( K + \inf_{n \ge s} H_n(\eta) = 0, \)

and \( S(s) = s \). Moreover the function \( u(x) \) is continuous

PROOF. Consider the function \( \inf_{n \ge s} H_n(s) = H_s(S(s)) \).

We have \( H_s(S(s)) = 0 \) for \( s \ge \bar{s} \). From the assumption we have \( H_0(S(0)) < -K \). From (9.2.18) we know that \( H_s(S(s)) \) is strictly increasing in \( s \), for \( s < \bar{s} \). So there will be one and only one \( s \), for which (9.2.22) is verified. So the pair \( s, S \) is well identified. We are going to construct a solution of (9.2.11), for which the optimal feedback is defined by an \( s, S \) policy, with the values \( s, S \) just defined. To