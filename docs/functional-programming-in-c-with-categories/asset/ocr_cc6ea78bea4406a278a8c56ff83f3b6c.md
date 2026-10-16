# 3.7 Practical Structural Induction

> "Informal proofs are algorithms; formal proofs are code."
> -Logical Foundations

This section aims to convey the general idea behind Structural induction and how we can use it when we want to formulate methods from Recursive Algebraic Data structures.

Structural induction is used to prove that some proposition P(x) holds for all x of some sort of recursively defined structure, such as formulas, lists, or trees.

![](bbox=[0.25, 0.34, 0.72, 0.5])

The structural induction generalizes the simple mathematical induction on Natural numbers, can be generalized within the context of Inductive types. Mathematicians are obsessed with the Natural numbers and it is of no surprise, that Gödel started with his System T Recusor from the Naturals. Nonetheless it soon became clear that from the point of view of Computer Science the Natural numbers is simple a recursive structure 0, S0, SS0..., which does not have any difference from other recursive structures like the lists and trees.

For the structural induction there is a generalized form of the induction that says : If x is a Type of a Recursive Type T and P(y) is true for all substructures y, then P(x) must also be true.

```
[∀x: T [∀y: T [ y <: x → P(y)] ] → P(x)
```

Structural induction is a more general version of the Mathematical induction on the naturals. The nice thing with programming is that you can actually test your "proof" immediately by seeing that the types "fit" using the type-checking of the compiler and also that some example cases have the expected result at runtime.