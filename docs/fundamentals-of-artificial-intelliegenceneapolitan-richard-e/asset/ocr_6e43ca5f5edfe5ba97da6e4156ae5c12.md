# Example 13.7 For the Markov chain determined by the urns in Figure 13.3 the transition matrix is

```
\(\mathbf{P} = \begin{pmatrix} 1/6 & 1/2 & 1/3 \\ 2/9 & 4/9 & 1/3 \\ 1/2 & 1/3 & 1/6 \end{pmatrix}\)
```

A Markov chain is called **finite** if it has a finite number of states. Clearly the chain represented by the urns in Figure 13.3 is finite. We denote by \(p_{ij}^{(n)}\) the probability of a transition from \(e_i\) to \(e_j\) in exactly \(n\) trials. That is, \(p_{ij}^{(n)}\) is the conditional probability of entering \(e_j\) at the \(n\)th trial given that the initial state is \(e_i\). We say \(e_j\) is **reachable** from \(e_i\) if there exists an \(n \ge 0\) such that \(p_{ij}^{(n)} > 0\). A Markov chain is called **irreducible** if every state is reachable from every other state.

# Example 13.8 Clearly, if \(p_{ij} > 0\) for every \(i\) and \(j\), the chain is irreducible.

The state \(e_i\) has **period** \(t > 1\) if \(p_{ii}^{(n)} = 0\) unless \(n = mt\) for some integer \(m\), and \(t\) is the largest integer with this property. Such a state is called **periodic**. A state is **aperiodic** if no such \(t > 1\) exists.

# Example 13.9 Clearly, if \(p_{ii} > 0\), \(e_i\) is aperiodic.

We denote by \(f_{ij}^{(n)}\) the probability that starting from \(e_i\) the first entry to \(e_j\) occurs at the \(n\)th trial. Furthermore, we let

```
\(f_{ij} = \sum_{n=1}^{\infty} f_{ij}^{(n)}.\)
```

Clearly, \(f_{ij} \le 1\). When \(f_{ij} = 1\), we call \(P_{ij}(n) \equiv f_{ij}^{(n)}\) the **distribution of the first passage** for \(e_j\) starting at \(e_i\). In particular, when \(f_{ii} = 1\), we call \(P_i(n) \equiv f_{ii}^{(n)}\) the **distribution of the recurrence times** for \(e_i\), and we define the **mean recurrence time** for \(e_i\) to be

```
\(\mu_i = \sum_{n=1}^{\infty} n f_{ii}^{(n)}.\)
```

The state \(e_i\) is called **persistent** if \(f_{ii} = 1\) and **transient** if \(f_{ii} < 1\). A persistent state \(e_i\) is called **null** if its mean recurrence time \(\mu_i = \infty\) and otherwise it is called **non-null**.

# Example 13.10 It can be shown that every state in a finite irreducible chain is persistent (see [Ash, 1970]), and that every persistent state in a finite chain is non-null (see [Feller, 1968]). Therefore every state in a finite irreducible chain is persistent and non-null.

An aperiodic persistent non-null state is called **ergodic**. A Markov chain is called **ergodic** if all its states are ergodic.