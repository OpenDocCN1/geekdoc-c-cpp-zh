```
Full MatrixSpace of 3 by 3 dense matrices over
Univariate Polynomial Ring in x over Finite Field of size 5
```

and draw a random element from this domain:

```
sage: M.random_element()
[2*x^2 + 3*x + 4 + 4*x^2 + 2*x + 2    4*x^2 + 2*x]
[              3*x   2*x^2 + x + 3    3*x^2 + 4*x]
[    4*x^2 + 3*x^2 + 2*x + 4          2*x + 4]
```

# 5.2.3 Further Reading: Categories

In general, a parent does not itself have a parent, but a *category* that indicates its properties:

```
sage: QQ.category()
Join of Category of number fields and Category of quotient fields and
    Category of metric spaces
```

Sage knows that ℚ is a field:

```
sage: QQ in Fields()
True
```

and thus, for instance, an additive and commutative group (see Figure 5.1):

```
sage: QQ in CommutativeAdditiveGroups()
True
```

Since ℚ is a field, ℚ[x] is a Euclidean ring:

```
sage: QQ['x'] in EuclideanDomains()
True
```

All these properties are used to provide rigorous and efficient computations on elements of these sets.

# 5.3 Domains with a Normal Form

Let us now browse some of the parents we will encounter in Sage.

We have seen in §2.1 how important normal forms² can be in computer algebra, since they allow to determine if two objects are mathematically equal in comparing their normal form representations. Each of the fundamental parents presented in this section corresponds to a *domain with normal form*, i.e., a set of mathematical objects having a normal form. This allows Sage to represent without any ambiguity the elements of each of these parents³.

²In this book we use both *canonical form* and *normal form* to mean that two objects are mathematically identical if their canonical (or normal) forms are equal. Sometimes *normal form* is meant as a weaker notion, where only zero is assumed to have a unique representation.

³Most of the other parents available in Sage correspond to domains with a normal form, but not all of them. It also happens that, for efficiency reasons, Sage represents elements in normal form only when explicitly requested.