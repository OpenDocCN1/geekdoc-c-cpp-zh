This defines a Markov chain to which is associated the operator

(12.3.4) 
 \(\Phi^v \varphi(x, z) = \int_0^\infty \varphi(x + v - \zeta, c) f(\zeta | z) d\zeta,\)

hence the transition probability is given by

(12.3.5) 
 \(\pi(x, z, v; d\xi, d\zeta) = \delta(\xi - (x + v - \zeta)) \otimes f(\zeta | z) d\zeta.\)

We next define the function

(12.3.6) 
 \(l(x, v) = cv + hx^+ + px^-,\)

which will model the one period cost. The cost function is then

(12.3.7) 
 \(J_{x,z}(V) = E \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n).\)

We are interested in the value function

(12.3.8) 
 \(u(x, z) = \inf_V J_{x,z}(V).\)

We notice again that the properties (4.31), (4.32) are satisfied. To proceed, we need to specify a ceiling function. It corresponds to a control identically 0. Set \(l_v(x) = l(x, v)\). Note the inequalities

\(\Phi^{x+} u^+(x, z) \le x^+, \quad \Phi^{x-} u^-(x, z) \le x^- + c_0 z + c_1.\)

It is easy to check that

(12.3.9) 
 \((\Phi^0)^n x^+(x, z) \le x^+,\)

(12.3.10) 
 \((\Phi^0)^n x^-(x, z) \le x^- + c_0 z \frac{1-c_0^n}{1-c_0} + (n - c_0(n+1) + c_0^{n+1}) \frac{c_1}{(1-c_0)^2}.\)

Consider then the function

(12.3.11) 
 \(w_0(x, z) = \sum_{n=1}^\infty \alpha^{n-1} (\Phi^0)^{n-1} l_0(x)\)

# **Lemma 12.2.** We assume that

(12.3.12) 
 \(\alpha c_0 < 1,\)

then the series \(w_0(x, z) < \infty\), and more precisely

(12.3.13) 
 \(u_0(x, z) \le \frac{hx^+ + px^-}{1 - \alpha} + \frac{p c_0 z \alpha}{(1 - c_0 \alpha)(1 - \alpha)} + \frac{p c_1}{(1 - c_0)^2} \left( \frac{\alpha - c_0}{(1 - \alpha)^2} + \frac{c_0}{1 - \alpha c_0} \right).\)

PROOF. It is an immediate consequence of formulas (13.2.10) and (12.3.9). \(\square\)

We next write the Bellman equation

(12.3.14) 
 \(u(x, z) = \inf_{v \ge 0} [l(x, v) + \alpha \Phi^v u(x, z)].\)

We state the following

# **Theorem 12.4.** We assume (13.2.1), (12.3.2), (12.3.6), (13.2.11). Then there exists one and only one solution of equation (13.2.15), such that \(0 \le u \le w_0\). It is continuous and coincides with the value function (12.3.8). There exists an optimal feedback \(v(x, z)\) and an optimal control policy \(\bar{V}\).