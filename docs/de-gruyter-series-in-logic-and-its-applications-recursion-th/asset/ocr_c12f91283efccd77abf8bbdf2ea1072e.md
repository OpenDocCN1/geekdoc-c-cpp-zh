Then \((p_{a_{j-1}}^{j+1}, s_1) \le (r_1, s_1)\). Let \(q_{a_{j-1}}^{j+1} = s_1\). Now for \(j' \neq j\) and \(i < 2\), let \(v_{a_{j'-1}}^{j+1} = v_{a_{j'-1}}^j\), and

\(p_{a_{j-1}}^{j+1}(a) = \begin{cases} p_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^j(a) = p_{a_{j-1}}^{j+1}(a), \\ p_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^j(a) = p_{a_{j-1}}^{j+1}(a), \\ p_{a_{j-1}}^{j+1}(a) : \text{Otherwise.} \end{cases}\)

Let \(q_{a_{j-1}}^{j+1}\) be a name such that

\(q_{a_{j-1}}^{j+1}(a) = \begin{cases} q_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^{j+1} = p_{a_{j-1}}^{j+1} \wedge p_{a_{j-1}}^{j+1} \Vdash q_{a_{j-1}}^j(a) = q_{a_{j-1}}^j(a), \\ q_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^{j+1} = p_{a_{j-1}}^{j+1} \wedge p_{a_{j-1}}^{j+1} \Vdash q_{a_{j-1}}^j(a) = q_{a_{j-1}}^j(a), \\ q_{a_{j-1}}^{j+1}(a) : \text{Otherwise.} \end{cases}\)

This completes the construction at substage \(j + 1\).

For \(\sigma \in 2^n\) and \(i < 2\), let \((p_{a_\sigma}^{j+1}, q_{a_\sigma}^{j+1}) = (p_{a_\sigma}^{j+1}, q_{a_\sigma}^{j+1})\) and \(v_{a_\sigma} = v_{a_\sigma}^{j+1}\). Let \(\{\gamma_i\}_{i < \omega}\) be an enumeration of the countable set

\(\{\alpha < \omega \mid (\exists \sigma)(\sigma \in 2^{n+1} \wedge (p_\alpha(a) \text{ is defined} \vee p_\alpha \Vdash \neg \dot{q}_\alpha(a) \text{ is defined}'))\}\).

Let \(\beta_{n+1,i,j} = \gamma_i\) for \(i, j < \omega\). This ends the construction at stage \(n + 1\). Finally let \(a_n = \beta_{(n)}\) for each \(n\).

It is immediate that the sequences defined satisfy conditions (1)-(4) and hence the proof of Theorem 9.1.7 is complete. \(\square\)

# 9.1.3 Exercises

**Exercise 9.1.1.** Prove that there is a partial ordering \(\langle 2^{<\omega}, \le_P \rangle\) into which every locally countable partial ordering of size not greater than \(2^{\aleph_0}\) is embeddable.

**Exercise 9.1.2.** Prove Theorem 9.1.4.

**Exercise 9.1.3** (Sacks [107]). A partial ordering \(\langle \mathbf{P}, \le_P \rangle\) is locally finite if for any \(p \in \mathbf{P}\), \(|\{q \mid q \le_P p\}| < \aleph_0\). Prove that every locally finite partial ordering in \(\langle 2^\omega, \le_P \rangle\) is embeddable into \(\langle \mathscr{D}, \le \rangle\).

**Exercise 9.1.4.** Prove that there is an independent set \(X\) of Turing degrees of size \(2^{\aleph_0}\).

**Exercise 9.1.5.** Prove Theorem 9.1.6.

# 9.2 Embedding locally finite upper semilattices into \(\langle \mathscr{P}, \le \rangle\)

# 9.2.1 Embedding an upper semilattice

**Definition 9.2.1.** A partial ordering \(\langle P, \le \rangle\) is an *upper semilattice* if for any \(p, q \in P\), there is an \(r \in P\) such that \(r\) is the \(\le\)-least upper bound of \(p\) and \(q\).