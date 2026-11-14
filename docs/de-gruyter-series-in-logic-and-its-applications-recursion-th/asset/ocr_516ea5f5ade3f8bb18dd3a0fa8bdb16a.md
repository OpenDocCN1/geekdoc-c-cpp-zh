Suppose that $x$ is $\Pi^1_1$-semitraceable, $\omega_1^x = \omega_1^{ck,x}$, and $f \leq_h x$. Fix a $\Pi^1_1$-partial function $p$ for $f$ witnessing the semitraceability of $x$. Since $p$ is a $\Pi^1_1$-function, there is a recursive injection $h$ such that $p(m) = m \leftrightarrow h(m, m) \in O$.

Let $R(n, m)$ be a $\Pi^1_1(x)$-relation such that $R(n, m)$ if and only if there exists a $k$, where $m > k \geq n$, so that $f(k) = p(k)$. Then there is a total function $g$ uniformizing $R$ such that $g$ is $\Pi^1_1(x)$, and hence $\Delta^1_1(x)$. Thus for every $n$ there is an $m \in [g(n), g(g(n))$ such that $f(m) = p(m)$. Let $g'(0) = g(0)$, and $g'(n + 1) = g(g'(n))$ for all $n < \omega$. Define a $\Pi^1_1(x)$-relation $S(n, m)$ such that $S(n, m)$ if and only if $m \in [g'(n), g'(n + 1))$ and $p(m) = f(m)$. Uniformizing $S$, we obtain a $\Delta^1_1(x)$-function $g''$.

Let $H = \{h(m, k) \mid k \in (\exists n)(g''(n) = m \land f(m) = k)\}$. Then $H$ is $\Delta^1_1(x)$ and since $\omega_1^x = \omega_1^{ck,x}$, $H \subseteq O_n$ for some $n \in O$. Since $O_n$ is $\Delta^1_1$, we may define a $\Delta^1_1$-function $\bar{f}$ by setting $\bar{f}(i) = j$ if $h(i, j) \in O_n$ and $\bar{f}(i) = 1$ otherwise. Then there are infinitely many $i$ such that $f(i) = \bar{f}(i)$.

The following clarifies the relationship between traceability and semitraceability.

# Proposition 13.3.11 (Kjos-Hanssen, Nies, Stephan and Yu [68]). Every $\Delta^1_1$-traceable real is $\Delta^1_1$-dominated and $\Delta^1_1$-semidominated.

Proof. Clearly every $\Delta^1_1$-traceable real is $\Delta^1_1$-dominated. Let $x$ be a $\Delta^1_1$-traceable real and let $f$ be a $\Delta^1_1(x)$-function. Define $g(n) = \langle f(2^n), f(2^n + 2), \dots, f(2^{n+1} - 1) \rangle$. Then there is a $\Delta^1_1$ trace $T$ for $g$ such that $|T|_n \leq n$ for all $n$.

For $2^n + 1 \leq m \leq 2^{n+1}$, let $\bar{f}[m]$ be the $(m - 2^n)$-th entry of the tuple which is the $(m - 2^n)$-th element of $T_n$ if there exists such a tuple, and let $\bar{f}(m) = 1$ otherwise. It is not difficult to see that for every $n$ there is at least one $m \in [2^n, 2^{n+1})$ such that $f(m) = \bar{f}(m)$.

# Corollary 13.3.12. A real $x$ is $\Delta^1_1$-traceable if and only if for every $\bar{y}$ hyperarithmetic in $x$, there is a hyperarithmetic function $f$ such that

$(\forall n)(\exists m \in [2^n, 2^{n+1}))(f(m) = \bar{f}(m))$.

# Proposition 13.3.13. For any $x$, the following are equivalent.

+   (i) $x$ is $\Delta^1_1$-semidominated and $\Delta^1_1$-dominated;

+   (ii) For every function $g \leq_h x$, there exist an increasing $\Delta^1_1$-function $f$ and a $\Delta^1_1$-function $F : \omega \to \mathscr{P}_{<\omega}(\omega)$ with $|F(n)| \leq n$ such that

$(\forall n)(\exists m \in [f(n), f(n+1)))(g(m) \in F(m))$.

Proof. (i) $\Rightarrow$ (ii): Immediate because $1 \leq n$.

(ii) $\Rightarrow$ (i). Suppose $\bar{g} \leq_h x$. Without loss of generality, assume $\bar{g}$ is nondecreasing. Let $f$ and $F$ be the corresponding $\Delta^1_1$-functions. Let $u(n) = \sum_{k \in [f(n)+1)} k_{k \in F(k)}$ and note that $u$ is a $\Delta^1_1$-function dominating $\bar{g}$. Let

$h(n) = \langle \bar{g}(2^n + 1), \bar{g}(2^n + 2), \dots, \bar{g}(2^{n+1} - 1) \rangle$.