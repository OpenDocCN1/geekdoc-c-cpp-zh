# 2.2 Monoids

> "Alternatively, the fundamental notion of category theory is that of a Monoid"
> – Categories for the Working Mathematician

Monoids are one of those profound ideas that are easy to understand and are everywhere. Monoids belong to the category of Algebras. There are a couple of particularly important ways to organize different structures that appear in functional programming. Algebras is one of them. Fantasy land has some of the most important algebras in its specification.

Wikipedia says a monoid is an algebraic structure with a single associative binary operation and an identity element. Any structure that has those two elements is a monoid.

Suppose that S is a structure and ⊗ is some binary operation S ⊗ S → S, then S with ⊗ is a monoid if it satisfies the following two axioms:

+   1. Associativity: For all a, b and c in S, the equation (x ⊗ y) ⊗ z = x ⊗ (y ⊗ z) holds.

![](bbox=[0.16, 0.44, 0.84, 0.56])

+   2. Identity element: There exists an element e in S such that for every element a in S, the equations e ⊗ a = a ⊗ e = a hold.

![](bbox=[0.26, 0.64, 0.78, 0.72])

Let us take the integers we can take addition as a binary operation between two integers. The addition is associative. This means there is no importance on the order of the addition.

```
(x+(y+z)) = ((x+y) +z)
```

And 0 is the identity element for addition since:

```
x + 0 = x
```

For those reasons, the pair (0, +) forms a monoid over the integers. However, we can form different other monoids over the integers. For example, multiplication * also can be viewed as a monoid with its respective identity element the 1. In this way the pair (1, *) is another