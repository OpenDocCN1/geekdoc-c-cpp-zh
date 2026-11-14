By the Recursion Theorem, there is a constant \(c\) such that \(\Phi_{h(c)} = \Phi_c\). Set \(g = \Phi_c\) to be a partial recursive function. Hence

```
\(g((m, n)) = \begin{cases} 1 & m = 1 \wedge n = 2, \\ 1 & (\exists k)(g((m, k)) = 1 \wedge (g(k, n) = 1), \\ 1 & (\exists k)(g((k, m)) = 1 \wedge n = 2^n), \\ 1 & m = 1 \wedge n = 3 \cdot 5^d \wedge (\exists k)((\exists j)(g((j, m)) = 1 \wedge m = O_d(k)), \\ \uparrow & \text{Otherwise.} \end{cases}\)
```

Define \(m <_x n\) if and only if \(g(m, n)) = 1\). Set \(X = \{m \mid (\exists n)(m <_x n)\}\). It is straightforward to verify that the field of \(<_x\) satisfies (i)-(iv).

Note that given \(n \in \mathbb{N}\), \(<_x\) restricted to the set \(\{m \mid m <_x n\}\) is not necessarily linear. We introduce the following modification. Define \(z \le x\) to be such that \(i \in z\) if and only if \(i \in x\) and \(<_x\) restricted to \(\{m \mid m <_x i\}\) is linear. Then \(z\) is an arithmetical set. It is obvious that \(<_x\) restricted to \(z\) is a partial ordering, \(\emptyset \subset z\) and the conditions (i)-(iv) hold for \(<_x\) restricted to \(z\).

Now for any \(n \in \mathbb{O}\), let \(z_n\) be a hyperarithmetic set such that \(i \in z_n\) if and only if \(i \in \mathbb{O}_{2^{n*}}\) or there exists \(j \in \mathbb{O}_{2^{n*}}\) satisfying \(j <_l i\) and \(i \in z\). In other words, \(z_n\) is obtained by "cutting off" those nodes in \(z\) not above \(\mathbb{O}_{2^{n*}}\). Hence \(z_n\) has \(\mathbb{O}_{2^{n*}}\) as an "initial segment". Note that \(<_x\) restricted to \(z_n\) also satisfies conditions (i)-(iv).

# **Definition 2.6.2.** Let \(\Theta^* = \bigwedge A\) where

```
\(A = \{y \mid y \in x \text{ is hyperarithmetic} \wedge \text{Conditions (i)-(iv) in §1.2.1 hold for } <_x \text{ restricted to } y\}.\)
```

Denote by \(<_{\Theta^*}\) the ordering \(<_x\) restricted to \(\Theta^*\). Note that \(z_n \in A\) for all \(n \in \mathbb{O}\). Moreover \(\emptyset \subset \Theta^*\) by the definition of \(\emptyset\). Since conditions (i)-(iv) in §1.2.1 are arithmetical statements, by Corollary 2.2.2 it follows that \(\Theta^*\) is \(\Sigma^1_1\).

# **2.6.2 A** \(\Pi^1_1\)**-path through** \(\Theta\)

Since \(\Theta^*\) is \(\Sigma^1_1\), there must be an \(i \in \Theta^* \setminus \mathbb{O}\). Note that for every \(n \in \mathbb{O}\), \(i \in z_n \setminus \mathbb{O}_n\). Hence for every \(n \in \mathbb{O}\), there is an \(i_n \in \mathbb{O}_{2^{n*}} \setminus \mathbb{O}_{2^n}\) such that \(i_n <_x i\) and thus \(i_n <_{\Theta^*} i\). Let \(\Theta^*_i = \{j \mid j <_{\Theta^*} i \wedge j \in \mathbb{O}\}\). Then \(j \in \Theta^*_i\) if and only if \(j \in \Theta \wedge j <_l i\). Hence \(\Theta^*_i \subseteq \mathbb{O}\) is a \(\Pi^1_1\)-set.

# **Lemma 2.6.3.** \(<_{\Theta}\) restricted to \(\Theta^*_i\) is a well-ordering of order type \(\omega^{CK}_1\).

Proof. Obviously \(<_{\Theta}\) restricted to \(\Theta^*_i\) is a well-ordering. Suppose that the order type of \(<_{\Theta}\) restricted to \(\Theta^*_i\) is less than \(\omega^{CK}_1\). Then there is an \(n \in \mathbb{O}\) such that \(\Theta^*_i \subseteq \mathbb{O}_n\). Then for any \(k \in \mathbb{O}_{2^{n*}} \setminus \mathbb{O}_{2^n}\), \(k <_{\Theta^*} j\). Hence \(j \notin z_n\), a contradiction.