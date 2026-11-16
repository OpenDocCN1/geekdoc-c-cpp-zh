Oleksandr et al. [42] discuss the challenges in automatic differentiation of higher-order functions, for example functions in curried form.

# Nagata numbers.

As far as we know, our use of Nagata's idealization of a module ("Nagata numbers") in the context of AD is novel. Most works in the AD literature use the standard homogenous dual numbers. Some, like those of Krawiec et al. [12] and Smeding and Vákár [34], do feature various heterogeneous dual numbers, but they do not observe that these are instances of a general structure. Nagata originally defined his idealization of a module over a ring. Our weakening to consider only semiring structure is just cosmetic, and the extension of our methods to consider a (commutative) ring d of coefficients is straightforward, and we appeal to it without comment in Section 6. See also [43] for a comprehensive survey.

# Leibniz vs. Newton

One way to understand our contribution, in contrast to those of Elliott and others, is that while they take a 'Newtonian' view of AD as an algebraic operation on spaces of (abstract) functions, we take the 'Leibnizian' approach of understanding both AD and symbolic differentiation as an algebraic operation on a language Expr v of '(concrete) symbolic expressions'. This in particular contrasts with Baydin et al.'s assertion [2, Section 2.2, under 'What AD Is Not'] that AD is 'not symbolic differentiation', but echoes their observation, following Griewank [44], that it has a 'two-sided nature that is partly symbolic and partly numerical'.

# 8. Conclusion

Having identified three algebraic abstractions, we can write symbolic differentiation, forward-mode and reverse-mode AD as different instances of one and the same abstract algorithm. A significant contribution is the observation that we can generalize the well-known dual numbers into the Nagata idealization abstraction d κ ε for any d-module ε, which allows the ε parameter to vary independently of the semiring d of coefficients, and that we can use abstract Kronecker deltas to represent partial derivatives. Furthermore, guided by structure-preserving maps in the form of Kronecker isomorphisms, we have taken successive steps in optimising the representation, in a correct-by-construction manner, from basic symbolic differentiation via forward-mode AD to the (typically) much more efficient reverse-mode AD.

Future work includes further exploring matrix differentiation with this framework. Square matrices form a (non-commutative) semiring but matrices of arbitrary dimensions form an extra challenge, in particular when reflecting these dimensions in the types.

# CRediT authorship contribution statement

Birthe van den Berg: Conceptualization, Formal analysis, Investigation, Methodology, Project administration, Software, Writing – original draft, Writing – review & editing. Tom Schrijvers: Conceptualization, Formal analysis, Funding acquisition, Investigation, Methodology, Software, Writing – original draft, Writing – review & editing. James McKinna: Conceptualization, Formal analysis, Investigation, Methodology, Software, Writing – review & editing. Alexander Vandenbroucke: Conceptualization, Formal analysis, Investigation, Methodology, Software, Writing – original draft, Writing – review & editing.

# Declaration of competing interest

Co-author currently employed by Standard Chartered, UK.

# Acknowledgements

This work has been funded by KU Leuven's BOF grant number C14/20/079, and by the Flemish Fund for Scientific Research (FWO) grant number G0A9423N. The third author would like to thank Bernhard Rybkowicz for background insight into Nagata's construction.

# Appendix A. Derivation of the second-order derivative

This appendix expands on Section 6.4's claim that we can derive from the specification

```
derive_e2nd :: (Eq v, Smering d) => (v -> d) -> Expr v -> Dense v (Dense v d)
derive_e2nd var y x = eval var (tan^n (forwardAD_Dense Var
(tan^n (forwardAD_Dense Var e) y)) x)
```

that consists of three successive appeals to eval, an equivalent version that is an instance of abstractD (which consists of a single eval):