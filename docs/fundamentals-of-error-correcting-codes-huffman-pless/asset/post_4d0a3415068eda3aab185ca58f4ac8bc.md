
$C(\mathcal{X}, \mathcal{P}, D)$ over $\mathbb{F}_8$ with $5 \le k \le 21$, apply Theorem 13.4.3 to find the dimension of the code and a lower bound on its minimum distance. Give an upper bound on the minimum distance from the Singleton Bound. Finally, find a generator matrix for the code when $k=21$.

### Exercise 796 Prove that if $D \ge 0$, then $C(\mathcal{X}, \mathcal{P}, D)$ contains the all-one codeword.

Recall that the dual of a generalized Reed-Solomon code is also a generalized Reed-Solomon code by Theorem 5.3.3. Since generalized Reed-Solomon codes are algebraic geometry codes by Exercise 790, it is natural to ask if duals of algebraic geometry codes are also algebraic geometry codes. The answer is yes. It can be shown (see [135, Theorem 2.72] or [320, Theorem II.2.10]) that $C(\mathcal{X}, \mathcal{P}, D)^\perp = C(\mathcal{X}, \mathcal{P}, E)$, where $E = P_1 + \cdots + P_n - D + (\eta)$ for a certain Weil differential $\eta$ determined by $\mathcal{P}$; this differential is related to residues of functions mentioned at the conclusion of Section 13.2.2 and in Exercise 771.

## 13.5 The Gilbert-Varshamov Bound revisited

In Section 2.10 we derived upper and lower bounds on the largest possible rate
$$
\alpha_q(\delta) = \limsup_{n \to \infty} n^{-1} \log_q A_q(n, \delta n)
$$
for a family of codes over $\mathbb{F}_q$ of lengths going to infinity with relative distances approaching $\delta$. The Asymptotic Gilbert–Varshamov Bound is the lower bound $\alpha_q(\delta) \ge 1 - H_q(\delta)$ guaranteeing that there exists a family of codes with relative distances approaching $\delta$ and rates approaching or exceeding $1 - H_q(\delta)$, where $H_q$ is the Hilbert entropy function defined on $0 \le x \le r = 1 - q^{-1}$ by
$$
H_q(x) = \begin{cases} 
0 & \text{if } x = 0, \\ 
x \log_q(q-1) - x \log_q x - (1-x) \log_q(1-x) & \text{if } 0 < x \le r,
\end{cases}
$$
as we first described in Section 2.10.3. For 30 years after the publication of the Gilbert-Varshamov Bound, no family of codes had been demonstrated to exceed this bound until such a family of algebraic geometry codes was shown to exist in 1982. In this section we discuss this result; but before doing so we show that there is a family of Goppa codes that meet this bound.

### 13.5.1 Goppa codes meet the Gilbert-Varshamov Bound

Theorem 5.1.10 states that primitive BCH codes over $\mathbb{F}_q$ are asymptotically bad, where we recall that a set of codes of lengths going to infinity is asymptotically bad if either the rates go to 0 or the relative distances go to 0. This is true of other families of codes such as the family of cyclic codes whose extended codes are affine-invariant [161]. The family of binary codes obtained from Reed-Solomon codes over $\mathbb{F}_{2^m}$ by concatenation with the $\{m, m, 1\}$ binary code consisting of all binary $m$-tuples is also asymptotically bad [218, Chapter 10]. Recall that a set of codes of lengths approaching infinity is asymptotically good if both the rates and relative distances are bounded away from 0. Certainly, codes that meet the Asymptotic Gilbert–Varshamov Bound are asymptotically good. For most families of codes, such as cyclic codes, it is not known if the family is asymptotically bad or if it contains a subset of asymptotically good codes. The first explicit construction of asymptotically good codes was due to Justesen [160] in 1972; his codes are a modification of the concatenated Reed–Solomon codes mentioned above. While the Justesen codes are asymptotically good, they do not meet the Asymptotic Gilbert–Varshamov Bound. However, Goppa codes include a set of codes that meet the Asymptotic Gilbert–Varshamov Bound. We prove this here. However, the reader will note that the construction of this set of Goppa codes is not explicit; that is, one cannot write down the family of specific codes that meet the bound.

In our construction we will need a lower bound on the number $I_q(e)$ of irreducible monic polynomials of degree $e$ in $\mathbb{F}_q[x]$. The exact value of $I_q(e)$, computed in [18], is
$$
I_q(e) = \frac{1}{e} \sum_{d|e} \mu(d)q^{e/d},
$$
where $\mu$ is the Möbius function given by $\mu(d) = 1$ if $d = 1$, $\mu(d) = (-1)^r$ if $d$ is a product of $r$ distinct primes, and $\mu(d) = 0$ otherwise. The lower bound we will need is
$$
I_q(e) \ge \frac{q^e}{e} (1 - q^{-e/2+1}); \tag{13.12}
$$
the proof of this can also be found in [18].

### Theorem 13.5.1 There is a family of Goppa codes over $\mathbb{F}_q$ that meets the Asymptotic Gilbert–Varshamov Bound.

Proof: Let $t$ and $d$ be positive integers. Consider the Goppa code $\Gamma(L, G)$ over $\mathbb{F}_q$ of length $n = q^t$ with $L = \{y_0, y_1, \dots, y_{n-1}\} = \mathbb{F}_{q^t}$ and $G \in \mathbb{F}_q[x]$. The polynomial $G$ must not have roots in $L$, a requirement that is certainly satisfied if we choose $G$ to be irreducible of degree $e > 1$ over $\mathbb{F}_{q^t}$. We need to decide what condition must be satisfied for the existence of such a $G$ so that $\Gamma(L, G)$ has minimum distance at least $d$. To that end, let $\mathbf{c} = c_0 c_1 \cdots c_{n-1} \in \mathbb{F}_q^n$ where $0 < w(\mathbf{c}) = w$. If $\mathbf{c} \in \Gamma(L, G)$, then $\sum_{i=0}^{n-1} c_i / (x - \gamma_i) = a(x)/b(x)$ where $b(x)$ is a product of $w$ of the factors $(x - \gamma_j)$ and $\deg(a(x)) \le w - 1$. Furthermore, $a(x)$ is a multiple of $G(x)$; in particular, $G(x)$ must be one of the irreducible factors of $a(x)$ of degree $e$. There are at most $(w - 1)/e$ such factors. So if we want to make sure that $\mathbf{c} \notin \Gamma(L, G)$, which we do when $w < d$, we must eliminate at most $\lfloor (w - 1)/e \rfloor$ choices for $G$ from among all the $I_q(e)$ irreducible polynomials of degree $e$ in $\mathbb{F}_q[x]$. For each $1 \le w < d$ there are $\binom{n}{w}(q - 1)^w$ vectors $\mathbf{c}$ that are not to be in $\Gamma(L, G)$. Thus there are at most
$$
\sum_{w=1}^{d-1} \left\lfloor \frac{w-1}{e} \right\rfloor \binom{n}{w} (q-1)^w < \frac{d}{e} V_q(n, d)
$$
irreducible polynomials that cannot be our choice for $G$ where $V_q(n, d) = \sum_{i=0}^{d} \binom{n}{i} (q-1)^i$. Hence, we can find an irreducible $G$ so that $\Gamma(L, G)$ has minimum distance at least $d$ provided
$$
\frac{d}{e} V_q(n, d) < \frac{q^{te}}{e} (1 - q^{-te/2+1}), \tag{13.13}
$$
by (13.12). If $\delta = d/n$, taking logarithms base $q$ and dividing by $n$, we obtain
$$
n^{-1}[\log_q(\delta n) + \log_q V_q(n, \delta n)] < \frac{te}{n} + n^{-1}[\log_q(1 - q^{-te/2+1})].
$$
Taking limits as $n$ approaches infinity, Lemma 2.10.3 yields $H_q(\delta) \le \lim_{n \to \infty} te/n$ or $1 - H_q(\delta) \ge 1 - \lim_{n \to \infty} te/n$. Since $t = \log_q n$, we can choose an increasing sequence of $e$s growing fast enough so that both the inequality in (13.13) is maintained (guaranteeing the existence of a sequence of Goppa codes of increasing lengths $n = q^t$ with relative minimum distances at least $\delta n$) and $1 - H_q(\delta) = 1 - \lim_{n \to \infty} te/n$. Theorem 13.2.1 implies that the codes in our sequence have rate at least $1 - te/n$; therefore this sequence meets the Asymptotic Gilbert–Varshamov Bound.

### 13.5.2 Algebraic geometry codes exceed the Gilbert–Varshamov Bound

The 1982 result of Tsfasman, Vlăduţ, and Zink [333] showed for the first time that there exists a sequence of codes whose relative distances approach $\delta$ with rates exceeding $1 - H_q(\delta)$ as their lengths go to infinity. We will only outline this result as the mathematics involved is beyond the scope of this book.

Let $\mathcal{X}$ be a curve of genus $g$ over $\mathbb{F}_q$, $\mathcal{P}$ a set of size $n$ consisting of $\mathbb{F}_q$-rational points on $\mathcal{X}$, and $D$ a divisor on $\mathcal{X}$ with $\mathcal{P} \cap \text{supp}(D) = \emptyset$ where $2g - 2 < \deg(D) < n$. By Theorem 13.4.3, $\mathcal{C}(\mathcal{X}, \mathcal{P}, D)$ is an $[n, k, d]$ code over $\mathbb{F}_q$ with rate $R = k/n = (\deg(D) + 1 - g)/n$ and relative distance $d/n \ge (n - \deg(D))/n$. Thus
$$
R + \delta \ge \frac{\deg(D) + 1 - g}{n} + \frac{n - \deg(D)}{n} = 1 + \frac{1}{n} - \frac{g}{n}.
$$
In particular,
$$
R \ge -\delta + 1 + \frac{1}{n} - \frac{g}{n}. \tag{13.14}
$$
Thus we wish to show that there exists a sequence of codes, defined from curves, of increasing length $n$ with relative distances tending toward $\delta$ such that $g/n$ tends to a number as close to 0 as possible. Such a construction is not possible using only curves in the projective plane $\mathbb{P}^2(\mathbb{F}_q)$ as the number of points on the curve is finite (at most $q^2 + q + 1$), implying that the length of a code defined on the curve cannot approach infinity since the length is bounded by $q^2 + q$. This limitation is overcome by allowing the curves we examine to come from higher dimensional projective space. Although individual curves still have only a finite number of points, that number can grow as the genus grows. Fortunately, (13.14) applies for curves in higher dimensional space, as does Theorem 13.4.3.

Since we wish $g/n$ to be close to 0, we want $n/g$ to be as large as possible. To explore the size of this quantity, define $N_q(g)$ to be the maximum number of $\mathbb{F}_q$-rational points on a nonsingular absolutely irreducible curve $\mathcal{X}$ in $\mathbb{P}^m(\mathbb{F}_q)$ of genus $g$, and let
$$
A(q) = \limsup_{g \to \infty} \frac{N_q(g)}{g}.
$$
