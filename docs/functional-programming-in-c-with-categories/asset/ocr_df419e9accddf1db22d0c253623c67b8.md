This formulation is nice in the sense that allows for fluent chaining var total = new Sum(0) .concat(new Sum(1)) .concat(new Sum(2)) because of the fact that empty and concat both return a result of the same type. This also is more congruent with the mathematical definition that says that if S is a structure (in a programming language, this translates to a Type), then S × S → S, means that the operation returns a structure of the same kind.

In practice we do not care about strict definitions as long as we are aware that we are dealing with a monoid.

# 2.2.1 Folding monoids

Monoids have this very desirable property that if we keep applying this binary operation ⊗, we can always reduce the computation to a single element of the same type:

(M⊗...(M⊗(M⊗M)))→M

this is called folding.

(((v:M ⊗ u:M) ⊗ w:M ) ⊗ ... ⊗ z:M) =a:M

![](bbox=[0.25, 0.48, 0.7, 0.59])

Let us say we have some sequence of integers 2,4,5,6 and we want to add them this a beginner level problem:

```
var list = new[] { 1, 2, 3, 4 };
var accumulation = 0;
foreach (var current in list)
    accumulation = accumulation + current;
(0,+) monoid
```

What I highlighted there are just an initial element 0 and the addition which is an operation between two integers that return an integer

What if we wanted to multiply them?

```
var accumulation = 1;
foreach (var current in list)
    accumulation = accumulation * current;
(1,*) monoid
```