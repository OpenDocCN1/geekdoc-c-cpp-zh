We must complete the conditions by considerations on the boundary and about smoothness. The boundary is \(x=0\) We clearly must order at the boundary, otherwise the inventory remains at 0, since it cannot become negative. Eventually we order and we can consider that the problem starts at this time. Therefore, we can write

(14.1.4)
\(u(0) = K + \inf_{v>0} (cv + u(v)).\)

Concerning smoothness, equation (14.1.3) is written without ambiguity if

(14.1.5)
\(u \in C^1(0, \infty).\)

The set of inequalities and complementarity slackness equation (14.1.1), (14.1.2), (14.1.3) and associated boundary and smoothness conditions is called a *Quasi-Variational Inequality*.

**Remark 14.1.** The smoothness is not guaranteed by the definition of the value function \(u(x)\). It is a desirable property, which is far from automatic, in particular at switching points.

Let us now write conditions satisfied by a value function defined by an \(s, S\) policy. Note that

\(0 \le s \le S.\)

We first have

(14.1.6)
\(u_{s,S}(x) = K + c(S - x) + u_{s,S}(S), \forall x \le s.\)

Next

(14.1.7)
\(\alpha u_{s,S} + \lambda u'_{s,S} - hx = 0, \forall x > s.\)

These relations express the decision making under an \(s, S\) policy.

Comparison with the relations defining the value function \(u\) imply a natural way to obtain \(S\) from \(s\). Let us choose first a single positive number \(s\) and define \(u_s(x)\) by

(14.1.8)
\(u_s(x) + cx = K + \inf_{y>s} (cy + u_y(y)), x \le s\)

(14.1.9)
\(\alpha u_s + \lambda u'_s - hx = 0, \forall x > s.\)

Then \(S(s)\) is obtained simply by

(14.1.10)
\(\inf_{y>s} (cy + u_y(y)) = cS + u_s(S)\)

# 14.1.4. DEFINITION of \(u_s\). For any fixed \(s\), we can write the solution of the differential equation (14.1.9) as follows

\(u_s(x) = u_s(s) \exp -\frac{\alpha}{\lambda}(x-s) + \frac{h}{\lambda} \int_s^x y \exp -\frac{\alpha}{\lambda}(x-y) dy,\)

hence

(14.1.11)
\(u_s(x) = \frac{h}{\alpha} \left( x - \frac{\lambda}{\alpha} \right) + \left( u_s(s) - \frac{h}{\alpha} s + \frac{\lambda h}{\alpha^2} \right) \exp -\frac{\alpha}{\lambda}(x-s).\)

To define \(S = S(s)\) we write

\(u'_s(S) = -c,\)

therefore

\(\alpha u_s(S) = hS + \lambda c.\)