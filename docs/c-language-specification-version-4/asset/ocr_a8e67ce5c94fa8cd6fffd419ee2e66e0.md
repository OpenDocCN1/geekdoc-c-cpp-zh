The run-time processing of an array access of the form P[A], where P is a primary-no-array-creation-expression of an array-type and A is an argument-list, consists of the following steps:

+   - P is evaluated. If this evaluation causes an exception, no further steps are executed.
+   - The index expressions of the argument-list are evaluated in order, from left to right. Following evaluation of each index expression, an implicit conversion (§6.1) to one of the following types is performed: int, uint, long, ulong. The first type in this list for which an implicit conversion exists is chosen. For instance, if the index expression is of type short then an implicit conversion to int is performed, since implicit conversions from short to int and from short to long are possible. If evaluation of an index expression or the subsequent implicit conversion causes an exception, then no further index expressions are evaluated and no further steps are executed.
+   - The value of P is checked to be valid. If the value of P is null, a System.NullReferenceException is thrown and no further steps are executed.
+   - The value of each expression in the argument-list is checked against the actual bounds of each dimension of the array instance referenced by P. If one or more values are out of range, a System.IndexOutOfRangeException is thrown and no further steps are executed.
+   - The location of the array element given by the index expression(s) is computed, and this location becomes the result of the array access.

# 7.6.6.2 Indexer access

For an indexer access, the primary-no-array-creation-expression of the element-access must be a variable or value of a class, struct, or interface type, and this type must implement one or more indexers that are applicable with respect to the argument-list of the element-access.

The binding-time processing of an indexer access of the form P[A], where P is a primary-no-array-creation-expression of a class, struct, or interface type T, and A is an argument-list, consists of the following steps:

+   - The set of indexers provided by T is constructed. The set consists of all indexers declared in T or a base type of T that are not override declarations and are accessible in the current context (§3.5).
+   - The set is reduced to those indexers that are applicable and not hidden by other indexers. The following rules are applied to each indexer S.I in the set, where S is the type in which the indexer I is declared:
+     - If I is not applicable with respect to A (§7.5.3.1), then I is removed from the set.
+     - If I is applicable with respect to A (§7.5.3.1), then all indexers declared in a base type of S are removed from the set.
+     - If I is applicable with respect to A (§7.5.3.1) and S is a class type other than object, all indexers declared in an interface are removed from the set.
+   - If the resulting set of candidate indexers is empty, then no applicable indexers exist, and a binding-time error occurs.
+   - The best indexer of the set of candidate indexers is identified using the overload resolution rules of §7.5.3. If a single best indexer cannot be identified, the indexer access is ambiguous, and a binding-time error occurs.
+   - The index expressions of the argument-list are evaluated in order, from left to right. The result of processing the indexer access is an expression classified as an indexer access. The indexer access expression references the indexer determined in the step above, and has an associated instance expression of P and an associated argument list of A.

Depending on the context in which it is used, an indexer access causes invocation of either the get-accessor or the set-accessor of the indexer. If the indexer access is the target of an assignment, the set-accessor is invoked