This says if you give me a function (A→B→C) that takes an A and then a B and produces a C then if you give me something of a Product type AxB i could give you a C. This is the definition of un-currying. And its easy to implement in C#:

```
Funcn<(A, B), C> Rec(Func<A, Func<B, C>> f) => ((A, B) p) => f(p.Item1)(p.Item2);
```

Having this Recursor we can define everything else. For example, we can define the projections using the Rec AxB

```
Funcn<(A, B), A> Pr1<A, B> (Func<A, Func<B, A>> f) => Rec<A, B, A>(x => y => x);
```

```
Funcn<(A, B), B> Pr2<A, B> (Func<A, Func<B, B>> f) => Rec<A, B, B>(x => y => y);
```

We will use this product Recursor very often in practice, in the form of Pattern matching on objects that contain compositions.

# Curry-Howard correspondence

The Product is the equivalent to a logical AND or a conjunction A ∧ B of two propositions A and B. In order to conclude that the proposition A ∧ B holds we must know that both A and B are true. Or equivalently if we can prove A and prove B then we can Prove A ∧ B. This rule is commonly named introduction in mathematical logic because it introduces a conjunction ∧ out of the previous propositions.

> A / A∧B ^I

In the same spirit, in order to create a product of a type A and a type B then we must have an instance of both types in order to call the constructor of product var product = (x, y) => _. This equivalence originates from the Curry-Howard isomorphism, which is probably the most profound connection of computer programs and mathematical proofs. If we have an A ∧ B then we can deduce any of the A or B. This is called conjunction elimination. From A ∧ B the following hold

> A∧B / A ^E1

> A∧B / B ^E2

or the propositions A ∧ B → A , A ∧ B → B are tautologies.

A product is "costly to construct" since we need all components but easy to use since by taking any of the components through a projection (first, second...) would be valid.