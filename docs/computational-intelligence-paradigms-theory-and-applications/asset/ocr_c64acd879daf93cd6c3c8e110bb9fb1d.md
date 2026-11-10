Some authors refer to |A| as the “sigma count” of A.
For any pair of fuzzy sets defined on a finite universal set X, the “degree of subset hood”, S(A,B), of A in B is defined by

S(A,B) = (|A| − Σₓ max[0, A(x) − B(x)]) / |A|
= |A ∩ B| / |A|

Properties: A and B are fuzzy sets. The following properties hold for a,b in the range [0,1].

+   (i) a+A is a subset of aA
+   (ii) a ≤ b implies that bA is a subset of aA and b+A is a subset of a+A
+   (iii) a(A ∩ B) = aA ∩ aB and a(A ∪ B) = aA ∪ aB
+   (iv) a+(A ∩ B) = a+A ∩ a+B and a+(A ∪ B) = a+A ∪ a+B
+   (v) a(A^~) = (1−a)+A^~

This means that the alpha-cut of the complement of A is the
(1-a) strong alpha-cut of A complemented.

a(A^~) is not equal to aA^~
a+(A^~) is not equal to a+A^~

# 6.9.1 Fuzzy Complements

A(x) defines the degree to which x belongs to A. Let cA denote a fuzzy complement of A of type c. cA(x) is the degree that x belongs to cA.
(A(x) is therefore the degree to which x does not belong to cA.)

c(A(x)) = cA(x)

# Axioms for fuzzy complements

> > Axiom c1. c(0)=1 and c(1)=0 (boundary conditions)
> > Axiom c2. for all a,b in [0,1], if a ≤ b then c(a) ≥ c(b) (monotonicity)
> > Axiom c3. c is a continuous function (continuity)
> > Axiom c4. c is “involutive,” which means that c(c(a))=a for all a in [0,1] (involution)

These axioms are not independent since it can be shown that if a complement function c obeys Axioms c2 and c4, then it also must obey