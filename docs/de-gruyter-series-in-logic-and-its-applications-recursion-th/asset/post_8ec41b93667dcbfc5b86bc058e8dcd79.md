
Theorem 2.5.5 (Spector [155]). There exist reals $x$ and $y$ such that $x \not\le_h y$ and $y \not\le_h x$. In fact, there is a real $x \not\le_h 0$ with $\omega_1^x = \omega_1^{CK}$.

Proof. Let $A = \{x | x \notin \xi_0\}$ be a nonempty $\Sigma^1_1$-set. By Theorem 2.5.3 and Corollary 2.4.11, the set $B = \{x \in A | \omega_1^x = \omega_1^{CK}\}$ is a nonempty $\Sigma^1_1$-set. By Lemma 2.5.4, $B$ is uncountable. Since there are at most countably many reals hyperarithmetically reducible to 0, there is a real $x \in B$ such that $x \not\le_h 0$. Furthermore, $x \not\le_h 0$ since $\omega_1^x = \omega_1^{CK}$. $\square$

It should be pointed out that Spector's original proof of Theorem 2.5.5 was quite different from the one given above. His proof involved a measure-theoretic argument and was nonconstructive. That idea will be explored in Chapter 14 on higher randomness.

## 2.5.3 Kreisel's Basis Theorem

**Theorem 2.5.6** (Kreisel [35]). If $x$ is nonhyperarithmetic and $A \subseteq \omega^\omega$ is a nonempty $\Sigma^1_1$-set, then there is a $y \in A$ such that $x \not\le_h y$.

Proof. Suppose that $x$ is nonhyperarithmetic and $A \subseteq \omega^\omega$ is a nonempty $\Sigma^1_1$-set. By Gandy's Basis Theorem 2.5.3, the set $B = \{z | \omega_1^z = \omega_1^{CK} \land z \in A\}$ is a nonempty $\Sigma^1_1$-set. For each pair $(e, n)$ with $n \in \omega$, let

$P_{(e,n)} = \{z | (\exists i)(\Phi_e^{\tilde{H}_i}(i) \downarrow \lor \Phi_e^{\tilde{H}_i}(i) \downarrow \neq x(i))\}.$

We claim that for any nonempty $\Sigma^1_1$-set $C$, there is a nonempty $\Sigma^1_1$-set $Q_{(e,n)} \subseteq C \cap P_{(e,n)}$. There are three cases to consider.

- (1) There exist $z \in C$ and $i \in \omega$ such that $\Phi_e^{\tilde{H}_i}(i) \uparrow$. Then let $Q_{(e,n)} = \{z | (\Phi_e^{\tilde{H}_i}(i) \uparrow \land z \in C)\}$.
- (2) Not Case (1) but there exist $z_0, z_1 \in C$ and $i \in \omega$ such that $\Phi_e^{\tilde{H}_{z_0}}(i) \uparrow \neq \Phi_e^{\tilde{H}_{z_1}}(i)$. Then there is a $k \le 1$ such that $\Phi_e^{\tilde{H}_k}(i) \neq x(i)$. Let $Q_{(e,n)} = \{z | (\Phi_e^{\tilde{H}_z}(i) = \Phi_e^{\tilde{H}_k}(i) \land z \in C)\}$.
- (3) Neither (1) nor (2). Then the $\Sigma^1_1$-set $\{u | (\exists 2i)(\forall z \in C \land u(i) = \Phi_e^{\tilde{H}_z}(i))\}$ contains exactly one real which must be hyperarithmetic. Let $Q_{(e,n)} = C$.

By Proposition 1.1.12, there is a $y \in B \cap \bigcap_{n < \omega} P_{(e,n)}$. By the definition of $P_{(e,n)}$, $x \neq \Phi_e^{\tilde{H}_y}$. Note that $\omega_1^y = \omega_1^{CK}$. Hence by Theorem 2.3.3, we conclude $x \not\le_h y$. $\square$

Theorem 2.5.6 says that the cone of sets hyperarithmetically above one that is non-hyperarithmetic does not contain a nonempty $\Sigma^1_1$-subset. In particular, no cone above a nonhyperarithmetic set is $\Sigma^1_1$. From the model-theoretic point of view, the argument used in the proof of the theorem is a type-omitting argument. This will be used again later to construct nonstandard models for characterizing hyperarithmetic sets via the constructible hierarchy $L$.

## 2.5.4 Exercises

**Exercise 2.5.1.** Prove that for any real $z$, the set $\{(x, 0^x) \mid x \in 2^{\omega}\}$ is not $\Sigma_1^1(z)$.

**Exercise 2.5.2.** Prove that there exist $x, y \le_h \mathbf{0}$ such that $x \not\le_h y$ and $y \not\le_h x$.

**Exercise 2.5.3.** Prove that there is a sequence of reals $(x_i)_{i < \omega}$ such that $x_i <_h x_{i+1} <_h \mathbf{0}$.

**Exercise 2.5.4** (Slaman [140]). Prove that there is no $\Sigma_1^1$-set $A \subseteq \omega^\omega$ such that every $\Sigma_1^1$-set is a continuous injective image of $A$.

**Exercise 2.5.5** (Hjorth [49]). Prove that every $\Sigma_1^1$-set is a continuous injective image of the $\Pi_1^1$-set $\{x \in \omega^\omega \mid x \in \omega^\omega\}$.

**Exercise 2.5.6.** Prove that any nonempty $\Sigma_1^1$-set $A$ contains an element $x$ such that $0^x \le_T \mathbf{0}$.

**Exercise 2.5.7** (Solovay [152]). Given functions $f, g: \omega \to \omega$, we say that $g$ dominates $f$ if $g(i) \ge f(i)$ for $i < \omega$. Prove that a real $x$ is hyperarithmetic if and only if there is a function $f \ge_T x$ such that $g \ge_T f$ whenever $g$ dominates $f$.

## 2.6 More on $\mathbf{O}$

### 2.6.1 A nonstandard $\mathbf{O}$

We construct a nonstandard $\mathbf{O}$ which shares many properties with $\mathbf{O}$. The following lemma says that there is an r.e. set whose field is an end extension of $\mathbf{O}$.

**Lemma 2.6.1.** There is an r.e. set $x$ and an r.e. partial ordering relation $<_x$ defined on $x$ such that

- (i) The conditions (i)-(iv) in §1.2.1 hold for $<_x$;
- (ii) $\mathbf{O} <_x$;
- (iii) $<_0$ is the restriction of $<_x$ to $\mathbf{O}$; and
- (iv) If $m <_x n$ and $n \in \mathbf{O}$, then $m \in \mathbf{O}$.

Proof. We build $<_x$ by effective transfinite induction. Define a recursive function $h$ as follows:

```
\(\Phi_{h(e)}((m, n)) = \left\{ \begin{array}{ll} 1 & m = 1 \wedge n = 2, \ 1 & (\exists k)(\Phi_e((m, k)) = 1 \wedge \Phi_e((k, n)) = 1), \ 1 & (\exists k)(\Phi_e((k, m)) = 1 \wedge n = 2^m), \ 1 & m \neq 1 \wedge n = 3 \cdot 5^d \wedge (\exists k)(\exists j)(\Phi_e((j, m)) = 1 \wedge m = \Phi_d(k)), \ \uparrow & \text{Otherwise.} \end{array} \right.\)
```

By the Recursion Theorem, there is a constant \(c\) such that \(\Phi_{h(c)} = \Phi_c\). Set \(g = \Phi_c\) to be a partial recursive function. Hence

```
\(g((m, n)) = \begin{cases} 1 & m = 1 \wedge n = 2, \\ 1 & (\exists k)(g((m, k)) = 1 \wedge g(k, n) = 1), \\ 1 & (\exists k)(g((k, m)) = 1 \wedge n = 2^m), \\ 1 & m \neq 1 \wedge n = 3 \cdot 5^d \wedge (\exists k)(\exists j)(g((j, m)) = 1 \wedge m = \Phi_d(k)), \\ \uparrow & \text{Otherwise.} \end{cases}\)
```

Define \(m <_x n\) if and only if \(g(m, n) = 1\). Set \(X = \{m \mid (\exists n)(m <_x n)\}\). It is straightforward to verify that the field of \(<_x\) satisfies (i)-(iv).

Note that given \(n \in \mathbb{N}\), \(<_x\) restricted to the set \(\{m \mid m <_x n\}\) is not necessarily linear. We introduce the following modification. Define \(z \subseteq x\) to be such that \(i \in z\) if and only if \(i \in x\) and \(<_x\) restricted to \(\{m \mid m <_x i\}\) is linear. Then \(z\) is an arithmetical set. It is obvious that \(<_x\) restricted to \(z\) is a partial ordering, \(\emptyset \subset z\) and the conditions (i)-(iv) hold for \(<_x\) restricted to \(z\).

Now for any \(n \in \mathbb{O}\), let \(z_n\) be a hyperarithmetic set such that \(i \in z_n\) if and only if \(i \in \mathbb{O}_{2^{n*}}\) or there exists \(j \in \mathbb{O}_{2^{n*}}\) satisfying \(j <_l i\) and \(i \in z\). In other words, \(z_n\) is obtained by "cutting off" those nodes in \(z\) not above \(\mathbb{O}_{2^{n*}}\). Hence \(z_n\) has \(\mathbb{O}_{2^{n*}}\) as an "initial segment". Note that \(<_x\) restricted to \(z_n\) also satisfies conditions (i)-(iv).

### Definition 2.6.2

Let \(\Theta^* = \bigwedge A\) where

```
\(A = \{y \mid y \in x \text{ is hyperarithmetic} \wedge \text{Conditions (i)-(iv) in §1.2.1 hold for } <_x \text{ restricted to } y\}.\)
```

Denote by \(<_{\Theta^*}\) the ordering \(<_x\) restricted to \(\Theta^*\). Note that \(z_n \in A\) for all \(n \in \mathbb{O}\). Moreover \(\emptyset \subset \Theta^*\) by the definition of \(\emptyset\). Since conditions (i)-(iv) in §1.2.1 are arithmetical statements, by Corollary 2.2.2 it follows that \(\Theta^*\) is \(\Sigma^1_1\).

### 2.6.2 A \(\Pi^1_1\)-path through \(\Theta\)

Since \(\Theta^*\) is \(\Sigma^1_1\), there must be an \(i \in \Theta^* \setminus \mathbb{O}\). Note that for every \(n \in \mathbb{O}\), \(i \in z_n \setminus \mathbb{O}_n\). Hence for every \(n \in \mathbb{O}\), there is an \(i_n \in \mathbb{O}_{2^{n*}} \setminus \mathbb{O}_{2^n}\) such that \(i_n <_x i\) and thus \(i_n <_{\Theta^*} i\). Let \(\Theta^*_i = \{j \mid j <_{\Theta^*} i \wedge j \in \mathbb{O}\}\). Then \(j \in \Theta^*_i\) if and only if \(j \in \Theta \wedge j <_l i\). Hence \(\Theta^*_i \subseteq \mathbb{O}\) is a \(\Pi^1_1\)-set.

### Lemma 2.6.3

\(<_{\Theta}\) restricted to \(\Theta^*_i\) is a well-ordering of order type \(\omega^{CK}_1\).

Proof. Obviously \(<_{\Theta}\) restricted to \(\Theta^*_i\) is a well-ordering. Suppose that the order type of \(<_{\Theta}\) restricted to \(\Theta^*_i\) is less than \(\omega^{CK}_1\). Then there is an \(n \in \mathbb{O}\) such that \(\Theta^*_i \subseteq \mathbb{O}_n\). Then for any \(k \in \mathbb{O}_{2^{n*}} \setminus \mathbb{O}_{2^n}\), \(k <_{\Theta^*} j\). Hence \(j \notin z_n\), a contradiction.
