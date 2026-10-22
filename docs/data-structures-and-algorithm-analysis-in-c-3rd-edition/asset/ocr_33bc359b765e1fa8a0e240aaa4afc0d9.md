+   2. if a = b then b = a, and
+   3. if a = b and b = c, then a = c.

Of course, for distinct integers a, b, and c there are never cases where a = b, b = a, or b = c. So the claims that = is symmetric and transitive are vacuously true (there are never examples in the relation where these events occur). But because the requirements for symmetry and transitivity are not violated, the relation is symmetric and transitive.

# Example 2.2 If we clarify the definition of sibling to mean that a person is a sibling of him- or herself, then the sibling relation is an equivalence relation that partitions the set of people.

# Example 2.3 We can use the modulus function (defined in the next section) to define an equivalence relation. For the set of integers, use the modulus function to define a binary relation such that two numbers x and y are in the relation if and only if x mod m = y mod m. Thus, for m = 4, ⟨1, 5⟩ is in the relation because 1 mod 4 = 5 mod 4. We see that modulus used in this way defines an equivalence relation on the integers, and this relation can be used to partition the integers into m equivalence classes. This relation is an equivalence relation because

+   1. x mod m = x mod m for all x;
+   2. if x mod m = y mod m, then y mod m = x mod m; and
+   3. if x mod m = y mod m and y mod m = z mod m, then x mod m = z mod m.

A binary relation is called a partial order if it is antisymmetric and transitive.² The set on which the partial order is defined is called a partially ordered set or a poset. Elements x and y of a set are comparable under a given relation if either xRy or yRx. If every pair of distinct elements in a partial order are comparable, then the order is called a total order or linear order.

# Example 2.4 For the integers, relations < and ≤ define partial orders. Operation < is a total order because, for every pair of integers x and y such that x ≠ y, either x < y or y < x. Likewise, ≤ is a total order because, for every pair of integers x and y such that x ≠ y, either x ≤ y or y ≤ x.