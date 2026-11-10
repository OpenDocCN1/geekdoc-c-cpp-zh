
**Standard Fuzzy Complement:** defined as a fuzzy set \(\bar A\) on \(U\) for which \(\bar A(x) = 1 - A(x)\) for every \(x \in U\).

**Standard Fuzzy Intersection:** defined as a fuzzy set on \(U\) for which \((A \cap B)(x) = \min[A(x), B(x)]\) for every \(x \in U\).

**Standard Fuzzy Union:** defined as a fuzzy set on \(U\) for which \((A \cup B)(x) = \max[A(x), B(x)]\) for every \(x \in U\).

Functions that meet the criteria of fuzzy intersections are known as t-norms and those that meet the criteria of fuzzy unions are known as t-conorms. A largest fuzzy set is obtained by performing the standard fuzzy intersection, while a smallest fuzzy set is formed by performing the standard fuzzy union operation.

Points \(x \in X\) for which \(A(x) = \bar A(x)\) are called “equilibrium points” of \(A\).

Functions that qualify as fuzzy intersections and fuzzy unions are usually referred to in literature as “t-norms” and “t-conorms”, respectively.

The standard fuzzy intersection is the weakest fuzzy intersection (the largest fuzzy set is produced), while the standard fuzzy union is the strongest fuzzy union (the smallest fuzzy set is produced).

Fuzzy intersections and fuzzy unions do not cover all operations that aggregate fuzzy sets, but they are the only ones that are associative. The remaining aggregating operations must be defined as functions of \(n\) arguments for each \(n > 2\). Aggregation operations that, for any given membership grades \(a_1, a_2, \ldots, a_n\), produce a membership grade that lies between \(\min(a_1, a_2, \ldots, a_n)\) and \(\max(a_1, a_2, \ldots, a_n)\) are called “averaging operations”. For given fuzzy sets, each of the averaging operations produces a fuzzy set that is larger than any fuzzy intersection and smaller than any fuzzy union.

If each \(x \in X\) has to be a member of \(A\), \(B\), and/or \(C\), we have

$$
B = \bar A \cap \bar C
$$

which means that if a person is not young and they are not old, they must be middle aged.

Similarly,

$$
A \cup (A \cap B) = A
$$

Proof:

$$
\max[A, \min(A,B)] = \max[A,A] = A \quad \text{if } A(x) \leq B(x)
$$

$$
\max[A, \min(A,B)] = \max[A,B] = A \quad \text{if } A(x) > B(x)
$$

so it is true for all \(x\).

For any fuzzy set \(A\) defined on a finite universal set \(X\), we define its “scalar cardinality”, \(|A|\), by the formula

$$
|A| = \sum_{x \in X} A(x)
$$

Some authors refer to \(|A|\) as the “sigma count” of \(A\).

For any pair of fuzzy sets defined on a finite universal set \(X\), the “degree of subsethood”, \(S(A,B)\), of \(A\) in \(B\) is defined by

$$
S(A,B) = \frac{|A| - \sum_{x \in X} \max[0, A(x) - B(x)]}{|A|}
= \frac{|A \cap B|}{|A|}
$$

Properties: \(A\) and \(B\) are fuzzy sets. The following properties hold for \(a,b\) in the range \([0,1]\).

- (i) \(a^+ A \subseteq aA\)
- (ii) if \(a \le b\), then \(bA \subseteq aA\) and \(b^+A \subseteq a^+A\)
- (iii) \(a(A \cap B) = aA \cap aB\) and \(a(A \cup B) = aA \cup aB\)
- (iv) \(a^+(A \cap B) = a^+A \cap a^+B\) and \(a^+(A \cup B) = a^+A \cup a^+B\)
- (v) \(a(\bar A) = \overline{(1-a)^+ A}\)

This means that the alpha-cut of the complement of \(A\) is the \((1-a)\) strong alpha-cut of \(A\) complemented.

$$
a(\bar A) \neq \overline{aA}
$$

$$
a^+(\bar A) \neq \overline{a^+A}
$$

## 6.9.1 Fuzzy Complements

\(A(x)\) defines the degree to which \(x\) belongs to \(A\). Let \(cA\) denote a fuzzy complement of \(A\) of type \(c\). \(cA(x)\) is the degree to which \(x\) belongs to \(cA\). (\(A(x)\) is therefore the degree to which \(x\) does not belong to \(cA\).)

$$
c(A(x)) = cA(x)
$$

### Axioms for Fuzzy Complements

- **Axiom c1.** \(c(0)=1\) and \(c(1)=0\) (boundary conditions)
- **Axiom c2.** for all \(a,b \in [0,1]\), if \(a \le b\) then \(c(a) \ge c(b)\) (monotonicity)
- **Axiom c3.** \(c\) is a continuous function (continuity)
- **Axiom c4.** \(c\) is “involutive,” which means that \(c(c(a))=a\) for all \(a \in [0,1]\) (involution)

These axioms are not independent, since it can be shown that if a complement function \(c\) obeys Axioms c2 and c4, then it also must obey c1 and c3. In addition, it must be a one-to-one function, which means that the function is also “bijective”. It therefore follows that all involutive complements form a special subclass of all continuous complements, which in turn forms a special subclass of all fuzzy complements. The Standard Fuzzy Complement is one type of involutive fuzzy complement.

### Classes of Fuzzy Complements

1. “Sugeno class” defined by

$$
c_\lambda(a) = \frac{1-a}{1+\lambda a}
$$

where \(\lambda\) is in the range \((-1, \infty)\). When \(\lambda=0\), this becomes the Standard Fuzzy Complement.

2. “Yager class” defined by

$$
c_w(a) = (1-a^w)^{1/w}
$$

where \(w\) is in the range \((0, \infty)\). When \(w=1\), we again have the Standard Fuzzy Complement.

### Theorems of Fuzzy Complements

**Theorem 6.2:** Every fuzzy complement has at most one equilibrium. This means that \(c(a)-a=0\) for at most one \(a \in [0,1]\). (The fuzzy complements are assumed to obey all 4 axioms throughout.)

**Theorem 6.3:** Assume that a given fuzzy complement \(c\) has an equilibrium \(e\), which by Theorem 6.2 is unique. Then

$$
a \le c(a) \quad \text{if } a \le e
$$

$$
a \ge c(a) \quad \text{if } a \ge e
$$

**Theorem 6.4:** If \(c\) is a continuous fuzzy complement, then \(c\) has a unique equilibrium. A dual point, \(d_a\), with respect to \(e\) is defined by

$$
c(d_a) - d_a = a - c(a)
$$

**Theorem 6.5:** If a complement \(c\) has an equilibrium \(e\), then the equilibrium is its own dual point:

$$
d_e = e
$$

**Theorem 6.6:** For each \(a \in [0,1]\), \(d_a = c(a)\) if \(c(c(a)) = a\), that is, when the complement is involutive.

This means that if the complement is not involutive, either the dual point does not exist, or it does not coincide with the complement point.

**Theorem 6.7 (First Characterization Theorem of Fuzzy Complements):**
Let \(c\) be a function from \([0,1]\) to \([0,1]\). Then, \(c\) is an involutive fuzzy complement if and only if there exists a continuous function \(g\) from \([0,1]\) to \(\mathbb{R}\) such that \(g(0)=0\), \(g\) is strictly increasing, and

$$
c(a) = g^{-1}(g(1)-g(a))
$$

where \(g^{-1}\) is the inverse of \(g\), for all \(a \in [0,1]\).

Functions \(g\) are usually called increasing generators. Each function that qualifies as an increasing generator determines an involutive fuzzy complement by the equation above.

For the Standard Fuzzy Complement, \(g(a)=a\).

For the Sugeno class of complements,

$$
g_\lambda(a) = \frac{\ln(1+\lambda a)}{\lambda}, \quad \lambda > -1
$$

For the Yager class of complements,

$$
g_w(a) = a^w, \quad w > 0
$$

Combining to give

$$
g_{\lambda,w}(a) = \frac{\ln(1+\lambda a^w)}{\lambda}, \quad \lambda > -1,\; w > 0
$$

which yields

$$
c_{\lambda,w}(a) = \left(\frac{1-a^w}{1+\lambda a^w}\right)^{1/w}
$$

which contains the Sugeno class and the Yager class as special subclasses.

As one more example,

$$
g_\gamma(a) = \frac{a}{\gamma + (1-\gamma)a}, \quad \gamma > 0
$$

produces the class of involutive fuzzy complements

$$
c_\gamma(a) = \frac{\gamma^2(1-a)}{a + \gamma^2(1-a)}, \quad \gamma > 0
$$

Involutive fuzzy complements can also be produced by “decreasing generators”.

**Theorem 6.8 (Second Characterization Theorem of Fuzzy Complements):**
Let \(c\) be a function from \([0,1]\) to \([0,1]\). Then, \(c\) is an involutive fuzzy complement if and only if there exists a continuous function \(f\) from \([0,1]\) to \(\mathbb{R}\) such that \(f(1)=0\), \(f\) is strictly decreasing, and

$$
c(a) = f^{-1}(f(0)-f(a))
$$

where \(f^{-1}\) is the inverse of \(f\), for all \(a \in [0,1]\).

For the Standard Fuzzy Complement, \(f(a) = -ka + k\) for all \(k > 0\).

For the Yager class of complements, \(f_w(a) = 1 - a^w\) (\(w > 0\)).

## 6.9.2 Fuzzy Intersections: t-norms

The intersection of two fuzzy sets, \(A\) and \(B\), is specified by a binary operation on the unit interval; that is, a function of the form

$$
i : [0,1] \times [0,1] \longrightarrow [0,1]
$$

For every element \(x\) in the universal set, this function takes the membership grades of \(x\) in the fuzzy sets \(A\) and \(B\) and yields the membership grade of \(x\) in the set constituting the intersection of \(A\) and \(B\):

$$
(A \cap B)(x) = i[A(x), B(x)]
$$

The operator \(i\) in the above equation obeys a few specific properties in order to ensure that fuzzy sets produced by \(i\) are intuitively acceptable as meaningful fuzzy intersections of a given pair of fuzzy sets. The class of t-norms is now generally accepted as equivalent to the class of fuzzy intersections. Therefore, “t-norms” and “fuzzy intersections” may be used interchangeably.

Note that the function \(i\) is independent of \(x\); it depends only upon the values of \(A(x)\) and \(B(x)\) (or \(a\) and \(b\), which are in \([0,1]\), respectively).

A “fuzzy intersection/t-norm” is a binary operation on the unit interval that satisfies at least the following axioms for all \(a\), \(b\), and \(d\) in the range \([0,1]\).

### Axioms for Fuzzy Intersections

- **Axiom i1:** \(i(a,1) = a\) (boundary condition)
- **Axiom i2:** \(b \le d\) implies \(i(a,b) \le i(a,d)\) (monotonicity)
- **Axiom i3:** \(i(a,b) = i(b,a)\) (commutativity)
- **Axiom i4:** \(i(i(a,b),d) = i(a,i(b,d))\) (associativity)

The above four axioms are called the “axiomatic skeleton for fuzzy intersections/t-norms”.

It is often desired to restrict the class of fuzzy intersections (t-norms) by considering additional requirements. Three of the most important are:

- **Axiom i5:** \(i\) is a continuous function (continuity)
- **Axiom i6:** \(i(a,a) \le a\) (subidempotency)
- **Axiom i7:** \(a_1 < a_2\) and \(b_1 < b_2\) imply \(i(a_1,b_1) < i(a_2,b_2)\) (strict monotonicity)

Since the requirement in Axiom i6 is weaker than “idempotency” — the requirement that \(i(a,a)=a\) — it is called “subidempotency”.
