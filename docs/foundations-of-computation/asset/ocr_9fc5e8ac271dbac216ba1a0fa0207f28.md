figurations of the cube to be equivalent if it's possible to manipulate one configuration into the other by a sequence of twists. This is, in fact, an equivalence relation on the set of possible configurations. (Symmetry follows from the fact that each move is reversible.) It has been shown that this equivalence relation has exactly twelve equivalence classes. The interesting fact is that it has more than one equivalence class: If the configuration that the cube is in and the configuration that you want to achieve are not in the same equivalence class, then you are doomed to failure.

Suppose that R is a binary relation on a set A. Even though R might not be transitive, it is always possible to construct a transitive relation from R in a natural way. If we think of aRb as meaning that a is related to R to b "in one step," then we consider the relationship that holds between two elements x and y when x is related by R to y "in one or more steps." This relationship defines a binary relation on A that is called the *transitive closure* of R. The transitive closure of R is denoted R*. Formally, R* is defined as follows: For a and b in A, a R* b if there is a sequence x0, x1, ... , xn of elements of A, where n > 0 and x0 = a and xn = b, such that x0 R x1, x1 R x2, ... , and xn-1 R xn.

For example, if a R c, c R d, and d R b, then we would have that a R* b. Of course, we would also have that a R* c, and a R* d.

For a practical example, suppose that C is the set of all cities and let A be the binary relation on C such that for x and y in C, x A y if there is a regularly scheduled airline flight from x to y. Then the transitive closure A* has a natural interpretation: x A* y if it's possible to get from x to y by a sequence of one or more regularly scheduled airline flights. You'll find a few more examples of transitive closures in the exercises.

# Exercises

+   1. For a finite set, it is possible to define a binary relation on the set by listing the elements of the relation, considered as a set of ordered pairs. Let A be the set {a, b, c, d}, where a, b, c, and d are distinct. Consider each of the following binary relations on A. Is the relation reflexive? Symmetric? Antisymmetric? Transitive? Is it a partial order? An equivalence relation?

+   a) R = {(a, b), (a, c), (a, d)}.
+   b) R = {(a, a), (b, b), (c, c), (d, d), (a, b), (b, a)}.
+   c) R = {(b, b), (c, c), (d, d)}.
+   d) R = {(a, b), (b, c), (a, c), (d, d)}.
+   e) R = {(a, b), (b, a), (c, d), (d, c)}.

+   2. Let A be the set {1, 2, 3, 4, 5, 6}. Consider the partition of A into the subsets {1, 4, 5}, {3}, and {2, 6}. Write out the associated equivalence relation on A as a set of ordered pairs.