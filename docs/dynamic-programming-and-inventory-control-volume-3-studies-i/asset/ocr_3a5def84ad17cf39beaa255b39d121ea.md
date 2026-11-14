We can claim that \(x_3 \neq x'\) since

\(B_s(x') = G_s(x') - G_s(x_3) = K,\)

therefore \(x_3\) is a local minimum, which implies

(15.4.5) \(G'_s(x_3) = 0, \quad G''_s(x_3) > 0\)

Define next \(x_2\) to be the smallest maximum of \(G_s(\eta), \eta \le x_3\)

(15.4.6) \(G_s(x_2) = \sup_{\eta \le x_3} G_s(\eta)\)

The maximum is attained since

\(\sup_{\eta \le x_3} G_s(\eta) = \sup_{s \le \eta \le x_3} G_s(\eta),\)

and the function \(G_s(x)\) is continuous. Let us check that \(x_2 \ge x'\). Indeed suppose that \(x_2 < x'\). Then

\(\inf_{\eta \ge x_2} G_s(\eta) \le \inf_{\eta \ge x'} G_s(\eta),\)

and

\(G_s(x_2) - \inf_{\eta \ge x_2} G_s(\eta) \ge G_s(x') - \inf_{\eta \ge x'} G_s(\eta) = K\)

which contradicts the definition of \(x'\). Moreover \(x_2 \neq x_3\) since

\(G_s(x_2) - G_s(x_3) \ge G_s(x') - G_s(x_3) = K.\)

Therefore \(x_2\) is also a local maximum and we have

(15.4.7) \(G'_s(x_2) = 0 \quad G''_s(x_2) < 0.\)

So we have \(x' \le x_2 < x_3\). Let us prove the property

(15.4.8) \(G_s(x) - G_s(y) \le G_s(x_2) - G_s(x_3), \quad \forall x \le y \le x_3.\)

Indeed, if \(x < x'\) then

\(G_s(x) - G_s(y) \le G_s(x) - \inf_{\eta \ge x} G_s(\eta) < K \le G_s(x_2) - G_s(x_3),\)

and if \(x \ge x'\) then \(x' \le x \le y \le x_3\) and

\(G_s(x) - G_s(y) \le G_s(x_2) - G_s(x_3),\)

from the definition of \(x_2\) and \(x_3\).

Finally, let us define \(x_1\) such that

(15.4.9) \(G_s(x_1) = \inf_{\eta \le x'} G_s(\eta).\)

For the same reasons as in the definition of \(x_2\) the point \(x_1\) is well defined as the smallest minimum. Moreover \(x_1 \neq x'\). Indeed

\(G_s(x') = K + \inf_{\eta \ge x'} G_s(\eta),\)

and recalling that \(x' > x_0 > s\) and \(G_s(x)\) decreases on \((s, x_0)\)

\(G_s(x') \ge K + \inf_{\eta \ge x_2} G_s(\eta) = G_s(s) > G_s(x_0) \ge \inf_{\eta \le x'} G_s(\eta) = G_s(x_1),\)

consequently \(x_1\) is a local minimum and thus

(15.4.10) \(G'_s(x_1) = 0, \quad G''_s(x_1) > 0.\)

Note the sequence

(15.4.11) \(s < x_0 \le x_1 < x' \le x_2 < x_3.\)