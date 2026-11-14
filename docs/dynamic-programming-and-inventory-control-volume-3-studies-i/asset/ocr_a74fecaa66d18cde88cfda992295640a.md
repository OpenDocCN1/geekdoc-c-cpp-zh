and the impulse times \(\theta_n\) verify \(\theta_{n+1} > \theta_n + L\).

The cost function is given by \(J_s(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) \exp -\alpha \theta_n + \int_0^\infty f(y_x(t; V)) \exp -\alpha t dt \right]\).

At time 0 we assume that there is no delivery in the pipe line.

# 14.8.2. INEQUALITIES FOR THE VALUE FUNCTION.

The value function \(u(x) = \inf_V J_s(V)\),

satisfies the following set of inequalities and complementarity slackness conditions (Variational Inequality)

(14.8.1) 
\(u(x) \le K + E \int_0^L f(x - D(t)) \exp -\rho t dt + \inf_{v \ge 0} [cv + Eu(x + v - D(L)) \exp -\alpha L] = M(u)(x)\),

and

(14.8.2) \(-\lambda(u(x-1) - u(x)) + \alpha u(x) \le f(x)\).

The complementarity slackness condition expresses

(14.8.3) \([((\alpha + \lambda)u(x) - \lambda u(x-1)) - f(x)][u(x) - M(u)(x)] = 0\)

# 14.8.3. OPTIMAL s, S POLICY.

The concept of s, S policy extends easily. It is convenient to introduce the function

\(g(x) = f(x) + \alpha c x + \lambda E \int_0^L (f(x - 1 - D(t)) - f(x - D(t))) \exp -\alpha t dt - \alpha E \int_0^L f(x - D(t)) \exp -\alpha t dt\)

and we set

\(g_s(x) = (g(x) - g(s)) \mathbb{I}_{x > s}\).

We solve as before, for a given s

(14.8.4) \((\alpha + \lambda)H_s(x) - \lambda H_s(x-1) = g_s(x), \forall x \ge s; H_s(x) = 0, \forall x \le s\)

We define next the value function corresponding to s

\(u_s(x) = H_s(x) - cx + E \int_0^L f(x - D(t)) \exp -\alpha t dt + C(s)\),

where \(C(s)\) depends only on s. We want

\((\alpha + \lambda)u_s(x) - \lambda u_s(x-1) = f(x), \forall x \ge s\).

We check easily that the constant \(C(s)\) must satisfy

\(\alpha C(s) = g(s) + \lambda c\).

On the other hand

\(C(s) = K + \inf_{\eta \ge s} [c\eta + Eu_s(\eta - D(L)) \exp -\alpha L]\).