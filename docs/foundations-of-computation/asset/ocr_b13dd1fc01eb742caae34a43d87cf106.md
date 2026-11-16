equal to N. (This follows from two facts: The path shown in T1 from its root to its base has length less than or equal to N, because we chose the two occurrences of A to be among the N bottommost non-terminal symbols along the path in T from its root to its base. We know that there is no longer path from the root of T1 to its base, since we chose the path in T to be the longest possible path from the root of T to its base.) Since any parse tree with height less than or equal to N has yield of length less than K, we see that |xy^2z| < K.

If we remove T1 from T and replace it with a copy of T2, the result is a parse tree with yield uvy, so we see that the string uvy is in the language L. Now, suppose that both x and z are equal to the empty string. In that case, w = uvy, so the tree we have created would be another parse tree for w. But this tree is smaller than T, so this would contradict the fact that T is the smallest parse tree for w. We see that x and z cannot both be the empty string.

If we remove T2 from T and replace it with a copy of T1, the result is a parse tree with yield ux^2y^2z v, so we see that ux^2y^2z v ∈ L. The two parse trees that we have created look like this:

![](bbox=[0.05, 0.45, 0.95, 0.75])

Furthermore, we can apply the process of replacing T2 with a copy of T1 to the tree on the right above to create a parse tree with yield ux^3y^3z v. Continuing in this way, we see that ux^n y^n z v ∈ L for all n ∈ N. This completes the proof of the theorem.

Since this theorem guarantees that all context-free languages have a certain property, it can be used to show that specific languages are not context-free. The method is to show that the language in question does not