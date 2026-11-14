**Proposition 12.1.5** (Martin-Löf [96]). *There exists a universal Martin-Löf test. Namely, there is a Martin-Löf test* \(\{U_n\}_{n<\omega}\) *such that* \(\bigcap_{n<\omega} V_n \subseteq \bigcap_{n<\omega} U_n\) *for every Martin-Löf test* \(\{V_n\}_{n<\omega}\).

# 12.1.3 Strong Martin-Löf randomness

**Definition 12.1.6** (Kurtz [79]).
(i) A sequence of open sets \(\{U_n\}_{n<\omega}\) is a generalized Martin-Löf test if \(\{(\sigma, \sigma) \mid \sigma \in U_n\}\) is r.e. and \(\lim_{n \to \infty} \mu(U_n) = 0\);
(ii) a real x is strongly Martin-Löf random if \(x \notin \bigcap_{n<\omega} U_n\) for any generalized Martin-Löf test \(\{U_n\}_{n<\omega}\).

Strong Martin-Löf randomness has a number of regularity properties not shared by Martin-Löf randomness.

# 12.1.4 Relativized randomness

Each of the notions above may be relativized to an arbitrary real x. For example, an x-Martin-Löf test is a sequence of open sets \(\{U_n\}_{n<\omega}\) such that \(\{(n, \sigma) \mid \sigma \in U_n\}\) is x-r.e. and \(\mu(U_n) < 2^{-n}\) for every \(n \in \omega\). Then z is x-Martin-Löf random if \(z \notin \bigcap_{n<\omega} U_n\) for any x-Martin-Löf test \(\{U_n\}_{n<\omega}\). In particular, z is n-random if z is \(0^{(n-1)}\)-Martin-Löf random.

The following is known as van Lambalgen's Theorem.

**Theorem 12.1.7** (van Lambalgen [165]). \(x \oplus y\) is Martin-Löf random if and only if x is Martin-Löf random and y is x-Martin-Löf random, and also if and only if y is Martin-Löf random and x is y-Martin-Löf random.

Martin-Löf randomness seems to be the only randomness notion for which van Lambalgen's Theorem holds.

# 12.1.5 Relative strengths of randomness notions

The relative strengths of the notions of randomness introduced above may be summarized as follows. Note that the implications do not reverse:

+   Strong Martin-Löf randomness \(\Rightarrow\) Martin-Löf randomness
+   \(\Rightarrow\) Schnorr randomness
+   \(\Rightarrow\) Kurtz randomness