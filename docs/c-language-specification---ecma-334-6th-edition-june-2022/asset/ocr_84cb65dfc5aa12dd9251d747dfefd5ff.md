The binding-time processing of an indexer access of the form P[A], where P is a primary_no_array_creation_expression of a class, struct, or interface type T, and A is an argument_list, consists of the following steps:

+   - The set of indexers provided by T is constructed. The set consists of all indexers declared in T or a base type of T that are not override declarations and are accessible in the current context (§7.5).
+   - The set is reduced to those indexers that are applicable and not hidden by other indexers. The following rules are applied to each indexer S.I in the set, where S is the type in which the indexer I is declared:
+     - If I is not applicable with respect to A (§11.6.4.2), then I is removed from the set.
+     - If I is applicable with respect to A (§11.6.4.2), then all indexers declared in a base type of S are removed from the set.
+     - If I is applicable with respect to A (§11.6.4.2) and S is a class type other than object, all indexers declared in an interface are removed from the set.
+   - If the resulting set of candidate indexers is empty, then no applicable indexers exist, and a binding-time error occurs.
+   - The best indexer of the set of candidate indexers is identified using the overload resolution rules of §11.6.4. If a single best indexer cannot be identified, the indexer access is ambiguous, and a binding-time error occurs.
+   - The index expressions of the argument_list are evaluated in order, from left to right. The result of processing the indexer access is an expression classified as an indexer access. The indexer access expression references the indexer determined in the step above, and has an associated instance expression of P and an associated argument list of A, and an associated type that is the type of the indexer. If T is a class type, the associated type is picked from the first declaration or override of the indexer found when starting with T and searching through its base classes.

Depending on the context in which it is used, an indexer access causes invocation of either the get_accessor or the set_accessor of the indexer. If the indexer access is the target of an assignment, the set_accessor is invoked to assign a new value (§11.18.2). In all other cases, the get_accessor is invoked to obtain the current value (§11.2.2).

# 11.7.11 Null Conditional Element Access

A null_conditional_element_access consists of a primary_no_array_creation_expression followed by the two tokens “?” and “[”, followed by an argument_list, followed by a “]” token, followed by zero or more dependent_accesses.

```
null_conditional_element_access
  : primary_no_array_creation_expression '?' '[' argument_list ']'
    dependent_access*
  ;
```

A null_conditional_element_access is a conditional version of element_access (§11.7.10) and it is a binding time error if the result type is void. For a null conditional expression where the result type may be void see (§11.7.9).

A null_conditional_element_access expression E is of the form P?[A]B; where B are the dependent_accesses, if any. Let T be the type of the expression P[A]B. The meaning of E is determined as follows: