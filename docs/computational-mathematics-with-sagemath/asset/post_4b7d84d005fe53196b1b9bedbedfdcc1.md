
```
sage: R.<x,y,z> = QQ[]
sage: J = R.ideal(x^2 * y * z - 18,
....:               x * y^3 * z - 24,
....:               x * y * z^4 - 6)
```

As we will see in Section 9.2.3, the following command enables us to check the ideal J is of dimension zero, i.e., the system (9.1) has a finite number of solutions in $\mathbb{C}^3$:

```
sage: J.dimension()
0
```

Once this is established, the first reflex should be to call the method variety, which computes all solutions of the system. Without any parameter, it gives the solutions in the base field of the polynomial ring:

```
sage: J.variety()
[{y: 2, z: 1, x: 3}]
```

The solution (3,2,1) already found is thus the unique rational solution.

The next step is to enumerate the complex solutions. To perform this exactly, we work in the field of algebraic numbers. We find again the 17 solutions:

```
sage: V = J.variety(QQbar)
sage: len(V)
17
```

Explicitly, the last three have the following form:

```
sage: V[-3:]
[{z: 0.9324722294043558? - 0.3612416661871530?*I,
  y: -1.700434271459229? + 1.0528634325754712?*I,
  x: 1.337215067329615? - 2.685489874065187?*I},
 {z: 0.9324722294043558? + 0.3612416661871530?*I,
  y: -1.700434271459229? - 1.0528634325754712?*I,
  x: 1.337215067329615? + 2.685489874065187?*I},
 {z: 1, y: 2, x: 3}]
```

Each solution point is given by a dictionary whose keys are the generators of QQbar['x,y,z'] (and not of QQ['x,y,z'], which explains the short detour below), and the associated coordinates of the point. Except for the rational solution already identified, the first coordinates are all algebraic numbers of degree 16:

```
sage: (xx, yy, zz) = QQbar['x,y,z'].gens()
sage: [ pt[xx].degree() for pt in V ]
[16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 1]
```

### Computing with the Solutions and Identifying Their Structure.

We have obtained an exact representation of the complex solutions from the system (9.1), however this representation is not really explicit. This is not a problem: having the coordinates as elements of QQbar is enough to pursue exact computations on these solutions.

For example, it is not difficult to see that if \((x,y,z)\) is solution of the system (9.1), then so is \((|x|,|y|,|z|)\). Let us build the set of \((|x|,|y|,|z|)\) for \((x,y,z)\) solution:

```
sage: Set(tuple(abs(pt[i]) for i in (xx,yy,zz)) for pt in V)
{(3, 2, 1)}
```

All the values of \(x\) (resp. \(y, z\)) have thus the same modulus. Even more, we can check that the substitution

\((x,y,z)\mapsto(\omega x,\omega^9 y,\omega^6 z)\qquad\text{where}\qquad \omega=e^{2\pi i/17}\qquad (9.2)\)

leaves the system invariant. In particular, the last coordinates of the solutions are exactly the seventeenth roots of unity, which we check again thanks to the possibility to compute exactly with algebraic numbers:

```
sage: w = QQbar.zeta(17); w  # primitive root of 1
0.93247222940435587 + 0.36124166618715303*I
sage: Set(pt[zz] for pt in V) == Set(w^i for i in range(17))
True
```

The solutions of the system are therefore the triples \((3\omega, 2\omega^9, \omega^6)\) for \(\omega^{17}=1\). This is much more explicit!

**Exercise 35.** Look for real solutions (and not only rational ones) of (9.1), to check directly there is only \((x=3,y=2,z=1)\). Find again the substitution (9.2), including the value 17 for the order of \(\omega\) as root of unity, by a computation with Sage.

We could have reached the same result by examining the minimal polynomials of the coordinates of points of \(V\). We see indeed that a given coordinate has the same minimal polynomial for all solution points, apart from \((3,2,1)\). The common minimal polynomial of the third coordinates is nothing else than the cyclotomic polynomial \(\Phi_{17}\):

```
sage: set(pt[zz].minpoly() for pt in V[:-1])
{x^16 + x^15 + x^14 + x^13 + x^12 + x^11 + x^10 + x^9 + x^8 + x^7 + x^6
    + x^5 + x^4 + x^3 + x^2 + x + 1}
```

Those of the first and second coordinate are respectively \(3^{16}\cdot\Phi_{17}(x/3)\) and \(2^{16}\cdot\Phi_{17}(x/2)\).

## Closed-Form Expressions.

Getting an explicit form of the solutions is thus possible using the exponential notation of complex numbers:

```
sage: def polar_form(z):
....:     rho = z.abs(); rho.simplify()
....:     theta = 2 * pi * z.rational_argument()
....:     return (SR(rho) * exp(I*theta))
sage: [tuple(polar_form(pt[i]) for i in (xx,yy,zz)) for pt in V[-3:]]
[(3*e^(-6/17*I*pi), 2*e^(-14/17*I*pi), e^(-2/17*I*pi)),
 (3*e^(6/17*I*pi), 2*e^(-14/17*I*pi), e^(2/17*I*pi)), (3, 2, 1)]
```

Naturally, if we had the idea of writing the elements of \(V\) in exponential notation, this would have been enough to conclude.

### Simplifying the System.

A different approach is possible. Instead of looking for solutions, let us try to compute a simpler form of the system itself. The fundamental tools offered by Sage for this purpose are the triangular decomposition and Gröbner bases. We will see later exactly what they compute; let us first use them on this example:

```
sage: J.triangular_decomposition()
[Ideal (z^17 - 1, y - 2*z^10, x - 3*z^3) of Multivariate
Polynomial Ring in x, y, z over Rational Field]
sage: J.transformed_basis()
[z^17 - 1, -2*z^10 + y, -3/4*y^2 + x]
```

We obtain in both cases the equivalent system

$z^{17}=1\qquad y=2z^{10}\qquad x=3z^3,$

or $x=3y^2/4$ for the last equation with transformed_basis, i.e., \(V=\{(3\omega^3,2\omega^{10},\omega)\mid \omega^{17}=1\}\). This is an immediate parametrisation of the compact form of solutions found manually above.

## 9.2.2 What Does Solving Mean?

A polynomial system that has solutions often has an infinite number of solutions. The simple equation $x^2-y=0$ has an infinite number of solutions in $\mathbb{Q}^2$, not even considering $\mathbb{R}^2$ or $\mathbb{C}^2$. It is therefore not possible to enumerate them. The best we can do is to describe the set of solutions “as explicitly as possible”, i.e., compute a representation of it from which we can easily extract useful information. The situation is analogous to linear systems, for which (in the homogeneous case) a basis of the system kernel is a good description of the set of solutions.

In the particular case where the number of solutions is finite, it becomes possible to “compute them”. However, even in that case, do we want to enumerate the solutions in $\mathbb{Q}$, or in a finite field $\mathbb{F}_q$? To find real or complex numerical approximations? Or even, as in the example of last section, to represent them using algebraic numbers, i.e., to compute for example minimal polynomials of their coordinates?

This very example illustrates the fact that other representations of the set of solutions might be much more useful than a list of points, more so when the solutions are numerous. Therefore, enumerating the solutions is not always the best thing to do, even when possible. In the end, we do not really want to compute the solutions, but we want to compute *with* them, to deduce afterwards, according to the given problem, the information we are really interested in. The rest of this chapter investigates several useful tools for this purpose.

## 9.2.3 Ideals and Systems

If $s$ polynomials $p_1,\ldots,p_s\in K[x]$ vanish at a point $x$ with coordinates in $K$ or an extension of $K$, any element of the ideal they generate also vanishes at $x$. It is thus natural to associate to the polynomial system

\(p_1(x)=p_2(x)=\cdots=p_s(x)=0\)

with elements of these quotient rings. The ideal \(J_1\) associated to \((S_1)\) is built with:

```
sage: R.<x,y> = QQ[]
sage: J = R.ideal(x^2 + y^2 - 1, 16*x^2*y^2 - 1)
```

We can then form the quotient of \(K[x]\) by \(J_1\), and project polynomials on it, compute with equivalence classes modulo \(J_1\), and “lift” them into representatives:

```
sage: ybar2 = R.quo(J)(y^2)
sage: [ybar2^i for i in range(3)]
[1, ybar2, ybar2 - 1/16]
sage: ((ybar2 + 1)^2).lift()
3*y^2 + 15/16
```

There is a theoretical issue here. The elements of \(K[x]/J\) are represented in normal form, which is necessary to be able to check the equality between two elements. However, this normal form is not easy to define, for the reason already mentioned in §9.1.4: the division of a representative of an equivalence class \(p + J\) by a principal generator of \(J\), used to compute in \(K[x]/J\), has no direct analogue in several variables. Let us admit for now that a normal form nevertheless exists, which depends on the order on the elements chosen at the ring construction, and builds on a particular system of generators of \(J\) called Gröbner basis. Section 9.3 at the end of this chapter defines Gröbner bases and shows how to use them in computations. Sage automatically computes Gröbner bases when required; however, these computations are sometimes very expensive, in particular when the number of variables is large, which might make computations in a quotient ring somewhat difficult.

Let us go back to playing with Sage. When \(p \in J\), the command `p.lift(J)` rewrites \(p\) as a linear combination of generators of \(J\) with polynomial coefficients:

```
sage: u = (16*y^4 - 16*x^2*y^2 + 1).lift(J); u
[16*y^2, -1]
sage: u[0]*J.0 + u[1]*J.1
16*y^4 - 16*x^2*y^2 + 1
```

For any polynomial \(p\), the expression `p.mod(J)` gives the normal form of \(p\) modulo \(J\), seen as element of \(K[x]\):

```
sage: (y^4).mod(J)
y^2 - 1/16
```

Beware: while `J.reduce(p)` is equivalent to `p.mod(J)`, the variant `p.reduce([p1, p2, ...])` returns a representative of \(p + J\) which is not necessarily the normal form (see §9.3.2):

```
sage: (y^4).reduce([x^2 + y^2 - 1, 16*x^2*y^2 - 1])
y^4
```

By combining `p.mod(J)` and `p.lift(J)`, we can decompose a polynomial \(p\) into a linear combination of generators of \(J\) with polynomial coefficients, plus a remainder which is zero if and only if \(p \in J\).

to be finitely generated!) The rest of the chapter does not apply to these objects.
