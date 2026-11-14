and the control process \(v_n\) is adapted to the filtration \(\mathcal{F}^n\). We define the cost function for each period

(12.6.4) \( l(x, v) = hx^+ + px^- + cv. \)

Calling \(V = \{v_1, \cdots, v_n, \cdots\}\): a control policy, we define the cost functional

(12.6.5) \( J_{x, \lambda}(V) = E \left[ \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n) | y_1 = x, \lambda_1 = \lambda \right]. \)

We consider the value function

(12.6.6) \( u(x, \lambda) = \inf_V J_{x, \lambda}(V), \)

and the Bellman equation

(12.6.7) \( u(x, \lambda) = hx^+ + px^- - cx + \inf_{y \ge x} [\alpha y + \alpha \Phi^u(u, \eta, \lambda)]. \)

# **12.6.2. SCALABILITY.**

Bellman equation (12.6.7) is, as expected a 2 dimensional problem. We just describe here a case when the problem can be reduced to one dimension, by an interesting property, the *scalability*. We say that there is scalability with the function \(g(\lambda)\) if one has the relations

(12.6.8) \( f(x, \lambda) = \frac{f(x/q(\lambda))}{q(\lambda)}, \quad q(\rho(\lambda, x)) = q(\lambda) U\left(\frac{x}{q(\lambda)}\right). \)

Let us give examples. The first one is the function

(12.6.9) \( f(x, \lambda) = \frac{k \alpha x^{k-1}}{(\lambda + x^k)^{\alpha+1}}. \)

This probability density is called Weibull-Gamma. The reason is that it is obtained by combining a Weibull distribution with a Gamma distribution. Suppose we consider a Weibull distribution

\(\psi(y, x) = k y x^{k-1} \exp - y x^k,\)

depending on a parameter \(y\). However, the parameter \(y\) is not known. One considers that it is random with a density

\(g(y, \lambda) = \frac{\lambda^\alpha y^{\alpha-1} \exp - y \lambda}{\Gamma(a)},\)

where we recall that for \(a > 0\)

\(\Gamma(a) = \int_0^{+\infty} x^{a-1} \exp - x \, dx.\)

We see immediately that

\(f(x, \lambda) = \int_0^{+\infty} \psi(y, x) g(y, \lambda) \, dy.\)

The function \(f(x, \lambda)\) defined by (12.6.9) is scalable if \(\rho(\lambda, x) = \lambda + x^k\). The functions \(g(\lambda)\), \(f(x)\), \(U(x)\) are defined by

(12.6.10) \( q(\lambda) = \lambda \bar{k}, \quad f(x) = \frac{k \alpha x^{k-1}}{(1+x^k)^{\alpha+1}}, \quad U(x) = (1+x^k) \bar{k}. \)