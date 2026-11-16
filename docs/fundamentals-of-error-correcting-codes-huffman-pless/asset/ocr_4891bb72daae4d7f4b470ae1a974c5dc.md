need a preliminary definition and lemma. A subset of an abelian group G is normalized provided its entries sum to 0.

Lemma 8.7.13 Let $D$ be a $(v, k, \lambda)$ difference set in an abelian group $G$ with $\gcd(v, k) = 1$. Then the development $D$ of $D$ contains a unique normalized block.

Proof: Suppose that the elements of $D$ sum to $d$. Let $D_t = \{i + \delta \mid \delta \in D\}$ be an arbitrary block of $D$. Then the entries in $D_t$ sum to $d + ki$. As $\gcd(v, k) = 1$, there is a unique solution $i \in G$ of $d + ki = 0$.

Corollary 8.7.14 ([204]) Let $\mathcal{D} = (\mathbb{Z}_v, \mathcal{B})$ be a cyclic symmetric $2-(v, k, \lambda)$ design of order $\mu = k - \lambda$ with $\gcd(v, k) = 1$. Then the normalized block in $\mathcal{B}$ is a union of $p$-cyclotomic cosets modulo $v$ for any prime $p \mid \mu$ with $p > \lambda$ and $p \nmid v$.

Proof: If $D$ is any block in $\mathcal{B}$, it is a cyclic difference set in $\mathbb{Z}_v$, and $\mathcal{D}$ is the development of $D$ by Theorem 8.7.5. By Lemma 8.7.13, we may assume $D$ is normalized. By Theorem 8.7.12, $D\mu_p$ is a block in $\mathcal{B}$ for any prime $p \mid \mu$ with $p > \lambda$ and $p \nmid v$. Clearly, $D\mu_p$ is normalized; by uniqueness in Lemma 8.7.13, $D\mu_p = D$. Thus if $i$ is in $D$, then $ip$ modulo $v$ is also in $D$ implying that $D$ is the union of $p$-cyclotomic cosets modulo $v$.

Example 8.7.15 Let $D = (\mathbb{Z}_{13}, \mathcal{B})$ be a cyclic projective plane of order $\mu = 3$. Then $D$ is a symmetric $2-(13, 4, 1)$ design, and its normalized block $D$ is a union of $3$-cyclotomic cosets modulo $13$. These cosets are $C_0 = \{0\}$, $C_1 = \{1, 3, 9\}$, $C_2 = \{2, 5, 6\}$, $C_4 = \{4, 10, 12\}$, and $C_7 = \{7, 8, 11\}$. As blocks have size $4$, $D$ must be equal to one of $C_0 \cup C_i$ for some $i \in \{1, 2, 4, 7\}$. Note that each of $C_0 \cup C_i$ is indeed a cyclic difference set; this same fact is explored in Exercise 359 via cyclic codes. By Exercise 469, $D\mu_a$ for $a$ relatively prime to $v$ is also a $(13, 4, 1)$ difference set and $D\mu_a$ is the development of $D\mu_a$. Hence as $C_1 \cup \mu_2 = C_2$, $C_1 \cup \mu_4 = C_4$, and $C_1 \cup \mu_7 = C_7$, the four possibilities for $D$ all produce equivalent cyclic designs. Thus to equivalence there is only one cyclic projective plane of order $3$.

Exercise 469 Let $a$ be relatively prime to $v$. Let $D$ be a $(v, k, \lambda)$ cyclic difference set in $\mathbb{Z}_v$.

+   (a) Prove that $D\mu_a$ is also a cyclic difference set in $\mathbb{Z}_v$.

+   (b) Prove that if $D$ is the development of $D$, then $D\mu_a$ is the development of $D\mu_a$.

Exercise 470 Prove that up to equivalence there is a unique cyclic projective plane of order $4$. Also give a $(21, 5, 1)$ difference set for this plane.

Exercise 471 Prove that up to equivalence there is a unique cyclic symmetric $2-(11, 5, 2)$ design. Give an $(11, 5, 2)$ difference set for this design.

Exercise 472 Prove that up to equivalence there is a unique cyclic projective plane of order $5$. Also give a $(31, 6, 1)$ difference set for this plane.

Example 8.7.16 Using Corollary 8.7.14 we can show that there is no $(\mu^2 + \mu + 1, \mu + 1, 1)$ cyclic difference set and hence no cyclic projective plane of order $\mu$ with $10 \mid \mu$. Suppose $D$ is such a difference set. By Corollary 8.7.14, we may assume that $D$ is normalized with multipliers $\mu_2$ and $\mu_5$, since $\lambda = 1$ and neither $2$ nor $5$ divide $\mu^2 + \mu + 1$. Let $x \in D$