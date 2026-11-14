Consider two sets $F_k$ and $F_{k'n'}$. We define a function $g_{k,k:n'}$ from $U$ to $[0, 1]$, which is continuous (hence uniformly continuous, since $U$ is compact) and satisfies:
if $F_k \cap F_{k'n'} \neq \emptyset$ then $g_{k,k:n'} = 1$
if $F_k \cap F_{k'n'} = \emptyset$ then $g_{k,k:n'}(F_k) = 0, g_{k,k:n'}(F_{k'n'}) = 1$

The set of functions $g_{k,k:n'}$ is a separating sequence. Indeed if $u \neq v$ there exists $F_{k,n}$ and $F_{k'n'}$ such that $u \in F_{k,n}, v \in F_{k'n'}.$

To the function $g_n$ we associate $g^*_n$ as in Lemma A.2 and $G^*_n$ as in Lemma A.4.

Next define the sequence $H_n : \mathcal{F}(U) - \emptyset \to \mathcal{F}(U) - \emptyset$ by the formula
$H_n(A) = G^*_n[H_{n-1}(A)]; H_0(A) = A$

Since $A \neq \emptyset$, one has
$A = H_0(A) \supset H_1(A) \cdots \supset H_n(A)$.

Since
$H_n(A) = \left\{ u \in H_{n-1}(A) \mid g_n(u) = \min_{a \in H_{n-1}(A)} g_n(a) \right\},$

the sets $H_n(A)$ are not empty and compacts. We can assert that
\(\cap^\infty_{n=0} H_n(A) \neq \emptyset.\)

Indeed, there exists a sequence $a_n \in H_n(A)$. We can extract a subsequence $a_{n_k} \to a$. Necessarily $a \in \cap^\infty_{n=0} H_{n_k}(A) = \cap^\infty_{n=0} H_n(A)$.

If $u, u' \in \cap^\infty_{n=0} H_n(A)$, then by construction
$g_n(u) = g_n(u') = g^*_n(H_{n-1}(A)),$

and since the functions $g_n$ separate the points of $U$, we have $u = u'$. Therefore $\cap^\infty_{n=0} H_n(A)$ contains a single point, which is denoted by $\sigma(A)$. Let us check that

(A.2.5) \(H_n(A) \to \{\sigma(A)\}.\)

Indeed, the sequence $H_n(A)$ being decreasing, we can assert that
\(u \in \cap^\infty_{n=0} H_n(A) \implies d(u, H_n(A)) = 0, \forall n\)

therefore

(A.2.6) \(\cap^\infty_{n=0} H_n(A) \subset \liminf_n H_n(A) \subset \limsup_n H_n(A).\)

On the other hand, if we consider an element \(u \in \limsup_n H_n(A)\), there exists a sequence \(u_{n_k} \in H_{n_k}(A)\) such that \(d(u, u_{n_k}) \to 0\). We have \(n_k \le n_{k+1}\), hence for fixed \(k, u_{n_k} \in H_{n_k}\). This implies \(u \in H_{n_k}\), therefore \(u \in \cap^\infty_{n=0} H_n(A)\), which with (A.2.6) implies the result (A.2.5).

Now the functions \(G^*_n\) being Borel, the functions \(H_n\) are also Borel, \(\forall n\). Therefore the function \(\nu : \mathcal{F}(U) - \emptyset \to \mathcal{F}(U) - \emptyset\) defined by \(\nu(A) = \{\sigma(A)\}\) is Borel. To conclude that \(\sigma\) is Borel, we note that \(\sigma = \tau^{-1} \circ \nu\), where \(\tau : U \to \mathcal{F}(U) - \emptyset\) is defined simply by \(\tau(u) = \{u\}\). The map \(\tau\) is point to point and continuous. Since \(U\) is compact, \(\tau(U)\) is also compact, hence closed in \(\mathcal{F}(U) - \emptyset\). The inverse is Borel, and therefore \(\sigma\) is Borel, which concludes the proof.

We now prove Theorem 4.1: