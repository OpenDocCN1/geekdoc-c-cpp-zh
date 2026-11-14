Since Q(y, z) is \(\Sigma_1\), by Theorem 3.1.6, there is a \(v \in M\) such that

\(M \models (\forall y' \in y')(\exists f \in v)(\exists z'(f(y') = z \land P(f))).\)

Hence there is a \(w \in M\) such that \(w = \{f \mid f \in v \land P(f)\}\).

For any \(f_1, f_2 \in w\) and \(y' \in \text{Dom}(f_1) \cap \text{Dom}(f_2)\), we claim that \(f_1(y') = f_2(y')\). Suppose not. Then by the Axiom of Foundation again, there is a \(y'\) such that \(f_1(y') \neq f_2(y')\) but \(f_1(y'') = f_2(y'')\) for all \(y'' \in y'\). However,

\(f_1(y') = G(y', (\langle y'', f_1(y'') \rangle \mid y'' \in y')) = G(y', (\langle y'', f_2(y'') \rangle \mid y'' \in y')) = f_2(y')\),

a contradiction.

Now take \(f' = \bigcup_{f \in w} f\). By Theorem 3.1.7, \(f \in M\). Obviously, Dom(f) is transitive and so P(f). Define \(f' = f \cup \{\langle y, G(y, f \upharpoonright y) \rangle\}\). Then \(M \models f'(y) = G(y, f \upharpoonright y) \land P(f')\) and so \(M \models Q(y, G(y, f' \upharpoonright y))\). Hence \(M \models (\exists z)Q(y, z)\), a contradiction.

Thus KP + \((\forall y)(\exists z)Q(y, z)\).

# Remark 3.1.9.

Defining a function such as G in Theorem 3.1.8 quite often requires one to go through a series of straightforward, though tedious, steps of \(\Sigma_1\)-induction. Henceforth we will leave the details of these steps to the reader and refer to them simply as “applying Theorem 3.1.8 by \(\Sigma_1\)-induction”.

Theorem 3.1.8 is a central result in the theory of admissible sets. It plays the same role as that of effective transfinite induction in descriptive set theory. We illustrate this point with an application of the theorem. Define the transitive closure operator TC to be:

\(\text{TC}(\emptyset) = \emptyset\), and

\(\text{TC}(a) = a \cup \bigcup \{\text{TC}(x) \mid x \in a\}.\)

By induction on the relation \(\in\), one shows that for any set x, TC(x) is the smallest transitive set containing x. The question is whether this operator is well defined in KP.

Let G be a \(\Sigma\)-function such that \(G(\emptyset, y) = \emptyset\) and \(G(x, y) = x \cup \bigcup \{y_i \mid \langle y_0, y_1 \rangle \in y\}\). Then by Theorem 3.1.8 there is a \(\Sigma\)-function F such that \(F(x) = G(x, (\langle y, F(y) \rangle \mid y \in x))\). It is not difficult to verify that for each x, F(x) = TC(x). We have the following corollary.

# Corollary 3.1.10.

KP + TC(x) is a \(\Sigma\)-function.

By Corollary 3.1.10, together with the proof of Theorem 3.1.8, we have the following theorem.

# Theorem 3.1.11.

Let G be an n + 2-ary \(\Sigma\)-function. There is an n + 1-ary \(\Sigma\)-function F such that

\(\text{KP} \vdash F(y, x_1, \dots, x_n) = G(y, x_1, \dots, x_n, (\langle z, F(z, x_1, \dots, x_n) \rangle \mid z \in \text{TC}(y))).\)