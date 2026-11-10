# ### 6.9.2  Fuzzy Intersections: t-norms

The intersection of two fuzzy sets, A and B, is specified by a binary operation on the unit interval; that is, a function of the form

$$i : [0,1] \times [0,1] \longrightarrow [0,1]$$

every element x in the universal set is assigned the membership grade of x in the fuzzy sets A and B, and yields the membership grade of the element in the set constituting the intersection of A and B.

$$(A \cap B)(x) = i[A(x),B(x)]$$

The operator, i, in the above equation obeys a few specific properties in order to ensure that fuzzy sets produced by i are intuitively acceptable as meaningful fuzzy intersections of a given pair of fuzzy sets. The class of t-norms is now generally accepted as equivalent to the class of fuzzy intersections. Therefore, “t-norms” and “fuzzy intersections” may be used interchangeably.

Note that the function i is independent of x; it depends only upon the values if A(x) and B(x) (or a and b that are in [0,1], respectively).

A “fuzzy intersection/t-norm” is a binary operation on the unit interval that satisfies at least the following axions for all a, b, and d in the range [0,1].

+   **Axioms for fuzzy intersections:**
+   
+   - **Axiom i1:** i(a,1) = a (boundary condition)
+   - **Axiom i2:** if b ≤ d implies i(a,b) ≤ i(a,d) (monotonicity)
+   - **Axiom i3:** i(a,b) = i(b,a) (commutativity)
+   - **Axiom i4:** i(i(a,b),d) = i(a,i(b,d)) (associativity)

The above four axioms are called the “axiomatic skeleton for fuzzy intersections/t-norms”.

It is often desired to restrict the class of fuzzy intersections (t-norms) by considering additional requirements. Three of the most important are:

+   - **Axiom i5:** i is a continuous function (continuity)
+   - **Axiom i6:** i(a,a) ≤ a (subidempotency)
+   - **Axiom i7:** a₁ < a₂ and b₁ < b₂ implies i(a₁,b₁) < i(a₂,b₂) (strict monotonicity)

Since the requirement in Axiom i6 is weaker than “idempotency”, the requirement that i(a,a)=a, it is called “subidempotency”.