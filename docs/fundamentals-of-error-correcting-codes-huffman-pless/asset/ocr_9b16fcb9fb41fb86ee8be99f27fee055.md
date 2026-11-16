# 6 Duadic codes

In Chapter 5 we described the family of cyclic codes called BCH codes and its subfamily of RS codes. In this chapter we define and study another family of cyclic codes called duadic codes. They are generalizations of quadratic residue codes, which we discuss in Section 6.6. Binary duadic codes were initially defined in [190] and were later generalized to arbitrary finite fields in [266, 270, 301, 315].

# 6.1 Definition and basic properties

We will define duadic codes in two different ways and show that the definitions are equivalent. We need some preliminary notation and results before we begin. Throughout this chapter $\mathbb{Z}_n$ will denote the ring of integers modulo $n$. We will also let $\mathcal{E}_n$ denote the sub-code of even-like vectors in $\mathcal{R}_n = \mathbb{F}_q[x]/(x^n - 1)$. The code $\mathcal{E}_n$ is an $[n, n-1]$ cyclic code whose dual code $\mathcal{E}_n^\perp$ is the repetition code of length $n$. By Exercise 221 the repetition code has generating idempotent

$\overline{j}(x) = \frac{1}{n}(1+x+x^2+\cdots+x^{n-1})$.

So by Theorem 4.4.9, $\mathcal{E}_n$ has generating idempotent $1-\overline{j}(x)\mu_{-1} = 1-\overline{j}(x)$. We summarize this information in the following lemma.

Lemma 6.1.1. The code $\mathcal{E}_n$ has the following properties:

+   (i) $\mathcal{E}_n$ is an $(n, n-1)$ cyclic code.
+   (ii) $\overline{\mathcal{E}}_n$ is the repetition code with generating idempotent $\overline{j}(x) = (1/n)(1+x+x^2+\cdots+x^{n-1})$.
+   (iii) $\mathcal{E}_n$ has generating idempotent $1-\overline{j}(x)$.

In defining the duadic codes, we will obtain two pairs of codes; one pair will be two even-like codes, which are thus subcodes of $\mathcal{E}_n$, and the other pair will be odd-like codes. It will be important to be able to tell when either a vector or a cyclic code in $\mathcal{R}_n$ is even-like or odd-like.

Lemma 6.1.2. Let $a(x) = \sum_{i=0}^{n-1} a_i x^i \in \mathcal{R}_n$. Also let $\mathcal{C}$ be a cyclic code in $\mathcal{R}_n$ with generator polynomial $g(x)$. Then:

+   (i) $a(x)$ is even-like if and only if $a(1) = 0$ if and only if $a(x)\overline{j}(x) = 0$,
+   (ii) $a(x)$ is odd-like if and only if $a(1) \neq 0$ if and only if $a(x)\overline{j}(x) = \alpha \overline{j}(x)$ for some nonzero $\alpha \in \mathbb{F}_q$.