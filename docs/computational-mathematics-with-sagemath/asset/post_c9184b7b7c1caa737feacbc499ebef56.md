
**Elimination.** The lexicographic monomial orders have the following fundamental property: *if $G$ is a Gröbner basis for the lexicographic order of $J \subset K[x_1, \ldots, x_n]$, then the $G \cap K[x_{k+1}, \ldots, x_n]$ are Gröbner bases for the elimination ideals*⁸ $J \cap K[x_{k+1}, \ldots, x_n]$. A lexicographic Gröbner basis splits into blocks, the last one of which depends only on $x_n$, the penultimate on $x_n$ and $x_{n-1}$, and so on⁹.

> \*For a given $k$, this is true more generally for any order such that $i \le k < j \Rightarrow x_i > x_j$. Such an order is called a “block order” (see also Table 9.5).

> ⁹ We thus get a “triangular form” of the system formed by the ideal generators, however in a weaker sense with respect to §2.5: we cannot say much a priori about the number of polynomials in each block or their leading terms.

```sage
sage: R.<t,x,y,z> = PolynomialRing(QQ, order='lex')
sage: J = R.ideal(t*x*y*z-t, t^2-x^2-y^2-z^2-1, t-x*y)
sage: [u.polynomial(u.variable(0)) for u in J.groebner_basis()]
[t + x + y + z - 1,
 (y + 1)*x + y + z - 1,
 (z - 2)*x + y*z - 2*y - 2*z + 1,
 (z - 2)*y^2 + (-2*z + 1)*y - z^2 + z - 1]
```

In this example, the last polynomial of the basis only depends on $y$ and $z$. It is preceded by a block of two polynomials in $x$, $y$ and $z$, and the first polynomial contains all variables. The successive elimination ideals can be seen immediately.

We have seen in §2.5 that the elimination ideals do not provide a perfect description of the ideal. Here, the block of polynomials in $z$ only is empty, thus any value of $z$, except maybe a finite number, appears as last coordinate of a solution. We are tempted to express the possible values of $y$ for each $z$ thanks to the last equation. We get two values, except for $z = 2$, for which only $y = -1$ works. Only when we get to the preceding equation do we notice that the choice $z = 2$ is contradictory. Inversely, again from the last equation, $y = -1$ implies $z = 2$, and is thus excluded. It finally occurs that none of the leading terms of the polynomials (written in their respective main variable, as in the above Sage output) vanishes for $z \neq 2$.

**Exercise 38** (Trigonometric relations). Write $\sin(\theta)^6$ as a polynomial in $u(\theta) = \sin \theta + \cos \theta$ and $v(\theta) = \sin(2\theta) + \cos(2\theta)$.

### 9.3.5 Computations

We refer the reader interested in algorithms computing Gröbner bases to the reference [CLO07] mentioned in the introduction. In addition, the module `sage.rings.polynomial.toy_buchberger` from Sage offers a “pedagogical” implementation of Buchberger’s algorithm and various related algorithms, which closely follows their theoretical description.

Let us however keep in mind that computing a Gröbner basis is expensive both in terms of time and memory, and even very expensive in some unlucky cases. Besides, the `groebner_basis` method has several options¹⁰ which allow the expert user to manually choose a Gröbner basis algorithm according to the characteristics of the problem to solve.

> ¹⁰ For more details, see the help page of this method, as well as those of internal methods of the ideal, whose name starts with `_groebner_basis`.

Let us consider the ideals C_n(K) ⊂ K[x_0, …, x_{n−1}] defined by:

C₂(K) = ⟨x₀ + x₁, x₀x₁ − 1⟩  
C₃(K) = ⟨x₀ + x₁ + x₂, x₀x₁ + x₀x₂ + x₁x₂, x₀x₁x₂ − 1⟩  
⋮  
C_n(K) = ⟨∑_{i∈ℤ/nℤ} ∏_{j=0}^{k} x_{i+j}⟩_{k=0}^{n−2} + ⟨x₀⋯x_{n−1} − 1⟩,    (9.11)

and accessible in Sage by commands like:

```sage
sage: from sage.rings.ideal import Cyclic
sage: Cyclic(QQ['x,y,z'])
Ideal (x + y + z, x*y + x*z + y*z, x*y*z - 1) of
Multivariate Polynomial Ring in x, y, z over Rational Field
```

They are classical test problems to evaluate the efficiency of tools for solving polynomial systems. On a computer where Sage computes the reduced Gröbner basis of C₆(ℚ) in less than a second:

```sage
sage: def C(R, n): return Cyclic(PolynomialRing(R, 'x', n))

sage: %time len(C(QQ, 6).groebner_basis())
CPU times: user 136 ms, sys: 0 ns, total: 136 ms
Wall time: 147 ms
45
```

The computation of that of $C_7(\mathbb{Q})$ does not terminate after a dozen hours, and uses more than 3 Gb of memory.

Failing to compute the Gröbner basis over the rational numbers, let us try to replace $\mathbb{Q}$ by a finite field $\mathbb{F}_p$. The idea, classical in computer algebra, is to limit the cost of operations on coefficients: those on elements of $\mathbb{F}_p$ take a constant cost, whereas the number of digits of rational numbers tends to increase quite rapidly during computations. We choose $p$ small enough such that computations in $\mathbb{F}_p$ can be done directly with machine integers. It must not however be too small, so that the Gröbner basis on $\mathbb{F}_p$ can share a large part of the structure of that on $\mathbb{Q}$.

For example, with a convenient $p$, the Gröbner basis of $C_6(\mathbb{F}_p)$ has the same number of elements as that of $C_6(\mathbb{Q})$:

```sage
sage: p = previous_prime(2^30)
sage: len(C(GF(p), 6).groebner_basis())
45
```

By increasing the size of the system to solve, we see that the influence of the coefficient field on the computing time is far from negligible: the cases $n = 7$ and $n = 8$ become easy to solve.

```sage
sage: %time len(C(GF(p), 7).groebner_basis())
CPU times: user 1.44 s, sys: 4 ms, total: 1.44 s
Wall time: 1.46 s
209
sage: %time len(C(GF(p), 8).groebner_basis())
CPU times: user 40.7 s, sys: 24 ms, total: 40.7 s
Wall time: 40.9 s
372
```

These examples illustrate also another important phenomenon: the output of a Gröbner basis computation might be much larger than the input. For example, the last computation above shows that any Gröbner basis, reduced or not, of $C_8(\mathbb{F}_p)$ (with this value of $p$) for the degrevlex order counts at least 372 elements, whereas $C_8$ is generated by only 8 polynomials.

### Change of order

The most interesting Gröbner bases are not the easiest to compute: often, the `degrevlex` order is the cheapest, but more useful information can be read on a lexicographic Gröbner basis. Besides, we sometimes need Gröbner bases of the same ideal for different monomial orders.

This motivates the introduction, in addition to general algorithms computing Gröbner bases, of algorithms of “change of order.” These algorithms compute a Gröbner basis for a given monomial order from a Gröbner basis of the same ideal for a different order. They are often more efficient than algorithms computing directly a basis for the target order. Thus, a strategy which often wins to compute a lexicographic Gröbner basis is the following: first compute a basis for the `degrevlex` order, then apply an algorithm of change of order. Sage does it automatically in some cases.

The `transformed_basis` method allows us to compute “by hand” Gröbner bases by change of order, when the ideal is zero-dimensional, or when the target order is `lex`. If needed, it first computes a Gröbner basis for the monomial order attached to the polynomial ring.

> In order to solve this differential equation you look at it till a solution occurs to you.
>
> George Pólya (1887 - 1985)

## 10 Differential Equations and Recurrences

### 10.1 Differential Equations

### 10.1.1 Introduction

If George Pólya’s method does not seem very effective, one can appeal to Sage even if the domain of formal resolution of differential equations remains a weakness of many symbolic computation systems. Sage is evolving however by expanding its spectrum of resolution.

One can, if desired, invoke Sage in order to obtain a qualitative study: indeed, its numerical and graphical tools will guide the intuition. This is the subject of Section 14.2 from the chapter on numerical integration. Tools for the graphical study of the solutions are given in Section 4.1.6. Solving methods using series can be found in Section 7.5.2.

One may prefer to solve differential equations exactly. Sage can sometimes help by directly giving a formal answer as we will see in this chapter.

In most cases, it will be necessary to go through a tricky manipulation of these equations to help Sage. It should be kept in mind that the expected solution of a differential equation is a *function* differentiable over a certain interval, but that Sage manipulates *expressions* without a definition domain. The machine will therefore require human intervention to move towards a rigorous solution.

We shall first study generalities on ordinary differential equations of order 1 and some special cases such as linear equations, separable equations, homogeneous equations, a parameter dependent equation (§10.1.2); then more briefly the equations of order 2 and an example of a partial differential equation (§10.1.3). We will end with the use of the Laplace transform (§10.1.4) and finally the resolution of some differential systems (§10.1.5).
