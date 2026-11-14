# 14.6.4 Lowness for \(\Pi^1_1\)-randomness and strong \(\Pi^1_1\)-ML randomness

Theorem 14.6.9 raises the natural question of characterizing reals that are low for \(\Pi^1_1\)-randomness – in particular whether there is one that is not hyperarithmetic. The answer to the latter is in the negative. Proposition 14.6.10 gives a characterization of such reals. We say that x is non-\(\Pi^1_1\)-random cupable if x \(\oplus\) y \(\ge_h\) 0 for all \(\Pi^1_1\)-random y. It is immediate that if x is low for \(\Pi^1_1\)-randomness then \(\omega_1^{CK} = \omega_1^x\).

# Proposition 14.6.10 (Harrington, Nies and Slaman [12]). A real x is low for \(\Pi^1_1\)-randomness if and only if x is low for \(\Delta^1_1\)-randomness and non-\(\Pi^1_1\)-random cupable.

Proof. If x is low for \(\Pi^1_1\)-randomness, then every \(\Pi^1_1\)-random real is \(\Pi^1_1(x)\)-random. Note that by relativizing Theorem 13.14, the \(\Pi^1_1(x)\)-set \(\{y \mid y \oplus x \ge_h 0\}\) is null since \(x \ge_h 0\). Thus x is non-\(\Pi^1_1\)-random cupable.

Suppose y is \(\Delta^1_1\)-random. If x is not \(\Delta^1_1(x)\)-random, then there is a \(\Delta^1_1(x)\)-nullset A containing y. By Proposition 14.2.3, the set \(B = \bigcup C \ge 2^n \mid \mu(C) = 0 \land C \text{ is } \Delta^1_1\) is a \(\Pi^1_1\)-nullset. Now \(y \in A \land B\). Hence \(A \land B\) is a nonempty \(\Sigma^1_1(x)\)-set. By the Gandy Basis Theorem (2.5.3), there is \(z \in A \land B\) such that \(\omega_1^x = \omega_1^z = \omega_1^{CK}\). By Corollary 14.3.2, z is \(\Pi^1_1\)-random but not \(\Pi^1_1(x)\)-random, a contradiction.

Conversely, suppose x is low for \(\Delta^1_1\)-randomness and non-\(\Pi^1_1\)-random cupable. Then \(x \ge_h 0\). Let z be a \(\Pi^1_1\) random real. Relativizing the proof of Theorem 14.3.1, the largest \(\Pi^1_1(x)\)-nullset \(\mathcal{O}(x)\) is a union of countably many \(\Delta^1_1(x)\)-null sets \(\mathcal{O}_n(x)\) and the \(\Pi^1_1(x)\)-nullset \(\{y \mid y \oplus x \ge_h 0\}\). Since x is low for \(\Delta^1_1\)-randomness, \(z \notin \bigcup_n \mathcal{O}_n(x)\). Since x is non-\(\Pi^1_1\)-random cupable, \(z \oplus x \ge_h 0\). Hence z is \(\Pi^1_1(x)\)-random. We conclude that x is low for \(\Pi^1_1\)-randomness.

# Proposition 14.6.11. There is a \(\Delta^1_1\)-traceable x which is \(\Pi^1_1\)-random cupable.

Proof. By Corollary 13.33.8, there is an uncountable \(\Sigma^1_1\)-set A containing only nonhyperarithmetic \(\Delta^1_1\)-traceable reals. Let \(\mathcal{O}\) be the largest \(\Pi^1_1\)-nullset. By Theorem 13.2.1, there exist \(x \in A\) and \(y \notin \mathcal{O}\) such that \(x \oplus y \ge_h 0\).

# Corollary 14.6.12.

+   (i) Lowness for \(\Pi^1_1\)-Kurtz randomness is different from \(\Delta^1_1\)-Kurtz randomness;
+   (ii) Lowness for \(\Pi^1_1\)-randomness is different from \(\Delta^1_1\)-randomness.

Proof. To prove (i), note that by Theorem 14.6.8 and 14.6.6, every \(\Delta^1_1\)-traceable real is low for \(\Delta^1_1\)-Kurtz randomness. By Proposition 14.6.11, there is an x which is low for \(\Delta^1_1\)-Kurtz randomness for which there is a \(\Pi^1_1\)-random y satisfying \(x \oplus y \equiv_h 0\). We claim that x is not low for \(\Pi^1_1\)-Kurtz randomness. Let \(e < \omega\) and \(e \in \mathcal{O}^\emptyset\) such that \(y = \Phi_e^{H_e^\emptyset}\). Then
\(z \in \{y\} \Leftrightarrow (\exists r \le_h x \land z(r) \in \{e\} \emptyset) \land z = \Phi_e^{H_e^\emptyset}\).

Hence y is a \(\Pi^1_1(x)\)-singleton and so non-\(\Pi^1_1(x)\)-random. Note that (ii) follows immediately from Proposition 14.6.10 and 14.6.11.