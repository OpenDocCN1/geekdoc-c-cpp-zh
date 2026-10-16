# 1.4 Essential Typed Lambda calculus and C#

Lambda calculus is the original functional language. Lambda calculus is a formal system in mathematical logic, that was used to express computations. It was created by the great Alonzo Church in the 1930s.

In this section we are going to see the simply typed lambda calculus (the usual symbol is λ→) and how this relates to the C# lambdas. In order to do that we will keep only for this section a subset of C# equivalent to the λ→. Simple typed lambda calculus is a very simple system that does not support Generics but allows for simple types.

# Terms

The formulation of the lambda expressions is constructed bottom up-in an inductive manner using as its base the term Term. A Term can be one of three things:

+   1. A Variable: x is a Term
+   2. An Abstraction: λx:A.M is a Term, where M is a Term and x is a variable.
+   3. An Application: (M N) is a Term, where M and N are Terms
+   4. A Constant c is a Term

From those the peculiar ones are the (2), and (3) which correspond in C# loosely to the following (we are going to elaborate on this):

+   1. The lambda abstraction λx:A.M corresponds to a C# function
+   Func<A, B> f = (A x) => ...
+   2. And the application (M N) corresponds to the trivial function call f(x)

Of course, only with those expressions you cannot expect to do any meaningful computation because you must introduce syntax related with the Natural Numbers (+, -, ...), Booleans (if, then... ). Nonetheless, one could go down the road of defining Numerals using the Church encoding (we will skip this part in this book) which are typable in λ→ using only one type:

```
Func<Func<_, _>, Func<_, _>> zero = (Func<_, _> f) => (_ x) => x;
Func<Func<_, _>, Func<_, _>> one = (Func<_, _> f) => (_ x) => f(x);
Func<Func<_, _>, Func<_, _>> two = (Func<_, _> f) => (_ x) => f(f(x));
```

For some single arbitrary empty type class _ { }.