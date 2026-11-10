might be a problem when a parameter represents a quantity in a restricted domain (for example, a positive real number).

A typical case is the simplification of the expression √x². The proper way consists of using the `assume` function, which enables us to define the properties of a variable, which can in turn be reverted by the `forget` instruction:

```
~~~
sage: assume(x > 0); bool(sqrt(x^2) == x)
True
sage: forget(x > 0); bool(sqrt(x^2) == x)
False
sage: n = var('n'); assume(n, 'integer'); sin(n*pi)
0
~~~
```

# 2.1.5 Some Pitfalls

> > **The Simplification Problem**
> >
> > The examples of §2.1.5 demonstrate how important normal forms are, and in particular the *test of zero*.
> >
> > Some families of expressions, like polynomials, have a decision procedure for the equality to zero. As a consequence, for those families, a program is able to decide whether a given expression is zero or not. In most cases, this test is done via the reduction to the normal form: the expression is zero if and only if its normal form is 0.
> >
> > Unfortunately, not all classes of expressions have a normal form, moreover for some classes it is possible to show that no general method is able to decide in a finite amount of time whether an expression is zero. An example of such a class is made of the rational numbers, the constants π, log 2 and a variable, together with additions, subtractions, multiplications, exponentials and the sine function. The repeated use of *numerical_approx*, while increasing the precision, succeeds in most cases to conjecture if a given expression is zero or not; however, it has been proven impossible to write a computer program taking as input an expression of this class, and returning *true* if this expression is zero, and *false* otherwise.
> >
> > The simplification problem is much harder in those classes. Without any normal form, computer algebra systems can only provide some rewriting functions that the user must play with to obtain some result. Some hope is however possible, if we can identify sub-classes of expressions which have a normal form, and if we know which methods should be applied to compute those normal forms. The Sage approach to handle those issues is presented in more details in Chapter 5.

Let c be a slightly complex expression:

```
~~~
sage: a = var('a')
sage: c = (a+1)^2 - (a^2+2*a+1)
~~~
```