to stating that for any hyperarithmetic Martin-Löf random z, x is Martin-Löf random relativized to z. By van Lambalgen's Theorem 12.17, this is in turn equivalent to saying that for every hyperarithmetic Martin-Löf random z, x \(\oplus\) z is Martin-Löf random which, by Theorem 12.2.11, is equivalent to “for any hyperarithmetic Martin-Löf random z, \((\exists c)(\forall n)(K(x \upharpoonright n) \ge 2n - C(z \upharpoonright n) - c)\)”.

One proves similarly that (i) <=> (iii).

# Corollary 14.5.2.

\(\Delta^1_1\)-randomness is upward closed for both K- and C-degrees.

# 14.5.2 The Kolmogorov complexity of \(\Pi^1_1\)-random reals

# Proposition 14.5.3.

For any \(\Pi^1_1\)-random x, if either x \(\le_K\) y or x \(\le_C\) y, then y is \(\Pi^1_1\)-random.

# Proof.

Suppose that x is \(\Pi^1_1\)-random and x \(\le_K\) y (resp. x \(\le_C\) y). By Corollary 14.5.2, y is \(\Delta^1_1\)-random. Note that {z | x \(\le_K\) z} (resp. {z | x \(\le_C\) z}) is \(\Delta^1_1(x)\). By Theorem 12.2.14 and Lemma 2.5.4 relativized to x, y \(\le_h\) x and so \(\omega_1^x = \omega_1^{CK}\). Then by Corollary 14.3.2, y is \(\Pi^1_1\)-random.

One may also show that \(\Delta^1_1\)-randomness is both K- and C-upward closed. By Theorem 14.4.7, if \((\omega_1^x)^L < \omega_1\), then \(\Sigma^1_1\)-randomness is upward closed for both \(\le_K\) and \(\le_C\). It is not known if \(\Pi^1_1\)-ML randomness is upward closed for either of these reducibilities.

# 14.5.3 Exercise

# Exercise 14.5.1.

Prove that there is no function f such that x is \(\Delta^1_1\)-random if and only if \((\exists c)(\forall n)(K(x \upharpoonright n) \ge n + f(n) - c)\).

# 14.6 Lowness for randomness

Lowness notions for higher randomness generally parallel those for randomness over the natural numbers. In this section, we omit proofs about lowness properties which are minor modifications of those for the latter. The reader is referred to the relevant books or papers for details.

# 14.6.1 Lowness for higher Kurtz randomness

# Lemma 14.6.1.

If x is \(\Delta^1_1\)-dominated and \(\Delta^1_1\)-semitraceable, then x is low for \(\Delta^1_1\)-Kurtz tests.